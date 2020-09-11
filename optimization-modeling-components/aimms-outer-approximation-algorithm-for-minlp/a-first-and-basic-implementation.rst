.. _sec:aoa.impl:

A First and Basic Implementation
================================

.. rubric:: Calling the AOA algorithm

To call the AOA algorithm, the GMP library is used to generate a number
of math program instances, and associated solver sessions, where
``SymbolicMP`` is the symbolic mathematical program containing the MINLP
model.

.. code-block:: aimms

	! Generate the MINLP model.
	GMINLP := GMP::Instance::Generate(SymbolicMP, FormatString("%e", SymbolicMP)) ;

	! Create NLP subproblem.
	GNLP := GMP::Instance::Copy( GMINLP, 'OA_NLP' ) ;
	GMP::Instance::SetMathematicalProgrammingType( GNLP, 'RMINLP' ) ;
	ssNLP := GMP::Instance::CreateSolverSession( GNLP ) ;

	! Create Master MIP problem.
	GMIP := GMP::Instance::CreateMasterMip( GMINLP, 'OA_MasterMIP' ) ;
	ssMIP := GMP::Instance::CreateSolverSession( GMIP ) ;

	BasicAlgorithm;

The basic algorithm outlined above is available in the GMP Outer
Approximation module as the procedure ``DoOuterApproximation``.

.. rubric:: The basic algorithm

The basic algorithm is straightforward, and makes a call to five other
procedures that execute the various algorithm steps. The naming
convention is self-explanatory, and the following lines make up this
first example of a main procedure. For the sake of brevity and clarity,
the parts of the code used to create a status file and to customize the
contents of the progress window have been left out. They can be found in
the basic implementation of the AOA algorithm in the AOA module.

.. code-block:: aimms

	InitializeAlgorithm;
	SolveRelaxedMINLP;

	while ( not MINLPAlgorithmHasFinished ) do
	    AddLinearizationsAndSolveMasterMIP;
	    FixIntegerVariablesAndSolveNLP;
	    TerminateOrPrepareForNextIteration;
	endwhile;

Note that the scalar parameter ``MINLPAlgorithmHasFinished`` must be
initially set to zero, and should only get a nonzero value when the
algorithm is ready to terminate.

.. rubric:: ``InitializeAlgorithm``

The following procedure is used to set all algorithmic parameters and
options, and to prepare the status file and progress window output.

.. code-block:: aimms

	IterationCount                := 0 ;
	LinearizationCount            := 1 ;
	EliminationCount              := 1 ;
	IncumbentSolutionHasBeenFound := 0 ;
	MINLPAlgorithmHasFinished     := 0 ;

	if ( NLPUseInitialValues ) then
	    GMP::Solution::RetrieveFromModel( GNLP, SolNumbInitialValues ) ;
	endif;

	if ( GMP::Instance::GetDirection( GMINLP ) = 'maximize' ) then
	    MINLPOptimizationDirection := 1;
	else
	    MINLPOptimizationDirection := -1;
	endif;

	GMP::Solution::SetProgramStatus( GMINLP, SolNumb, 'ProgramNotSolved' ) ;
	GMP::Solution::SetSolverStatus( GMINLP, SolNumb, 'Unknown' ) ;

	! The marginals of the NLP solver are needed.
	option always_store_marginals := 'On';

The algorithmic parameters are initially set such that the AOA algorithm
will always select the original initial values (i.e. the values of the
variables prior to starting the AOA algorithm) as the starting values
for each NLP subproblem to be solved. This setting has found to work
quite well in extensive tests performed using this algorithm.

.. rubric:: ``MINLPTerminate``

The following termination procedure is used in several of the procedures
that are described later.

.. code-block:: aimms

	if ( IncumbentSolutionHasBeenFound ) then
	    GMP::Solution::SetProgramStatus( GMINLP, SolNumb, 'LocallyOptimal' ) ;
	    GMP::Solution::SetSolverStatus( GMINLP, SolNumb, 'NormalCompletion' ) ;
	else
	    GMP::Solution::SetProgramStatus( GMINLP, SolNumb, 'LocallyInfeasible' ) ;
	    GMP::Solution::SetSolverStatus( GMINLP, SolNumb, 'NormalCompletion' ) ;
	endif;

	GMP::Solution::SendToModel( GMINLP, SolNumb ) ;
	MINLPAlgorithmHasFinished := 1 ;

The parameter ``IncumbentSolutionHasBeenFound`` contains a value of one
or zero depending on whether the AOA algorithm has received an incumbent
solution to the original MINLP model. Such a solution may be found when
solving the NLP subproblem, and this must then be communicated to the
AOA algorithm. Note that you also need to set the program status and
indicate when the MINLP algorithm has finished.

.. rubric:: ``SolveRelaxedMINLP``

The first model that is solved during the algorithm is the relaxed MINLP
model. All integer variables are relaxed to continuous variables. The
following procedure implements this first solution step of the outer
approximation algorithm.

.. code-block:: aimms

	SolveNLPSubProblem( 1 );
	ProgramStatus := GMP::Solution::GetProgramStatus( GNLP, SolNumb ) ;

	if ( ProgramStatus in NLPOptimalityStatus ) then
	    ! Save NLP solution as MINLP solution if an integer solution has been found.

	    if ( GMP::Solution::IsInteger( GNLP, SolNumb ) ) then

	        ! Set incumbent solution for MINLP.
	        GMP::Solution::RetrieveFromModel( GMINLP, SolNumb ) ;
	        IncumbentSolutionHasBeenFound := 1 ;

	        if ( TerminateAfterFirstNLPIsInteger ) then
	            ! Terminate if an integer solution has been found.

	            MINLPTerminate;
	        endif;
	    endif;
	else
	    ! Terminate if no linearization point has been found.

	    SolverStatus := GMP::Solution::GetSolverStatus( GNLP, SolNumb ) ;

	    if not ( SolverStatus in NLPContinuationStatus ) then
	        MINLPTerminate;
	    endif;
	endif ;

	IterationCount += 1 ;
	GMP::Solution::SetIterationCount( GMINLP, SolNumb, IterationCount ) ;

When the procedure ``SolveNLPSubProblem`` has terminated, the AOA
algorithm has typically found a point for the linearization step. The
exception being when the NLP solver does not produce a solution at all
(either feasible or infeasible). In such a situation the outer
approximating algorithm should be terminated. Note that in the special
event that the solution is feasible and has integer values for the
integer variables, a locally optimal solution has been found and the AOA
algorithm is instructed accordingly. Otherwise, the next step of the
outer approximation algorithm can be executed.

.. rubric:: ``AddLinearizationsAndSolveMasterMIP``

If a termination flag has not been set, the following procedure adds
linearizations to the master MIP problem prior to solving it. If this
model becomes infeasible, the outer approximation algorithm will be
terminated.

.. code-block:: aimms

	return when ( MINLPAlgorithmHasFinished );

	GMP::Linearization::Add( GMIP, GNLP, SolNumb, AllNonLinearConstraints,
	                         DeviationsPermitted, PenaltyMultiplier,
	                         LinearizationCount, JacobianTolerance ) ;

	LinearizationCount += 1 ;

	GMP::SolverSession::Execute( ssMIP ) ;

	GMP::Solution::RetrieveFromSolverSession( ssMIP, SolNumb ) ;
	GMP::Solution::SendToModel( GMIP, SolNumb ) ;

	ProgramStatus := GMP::Solution::GetProgramStatus( GMIP, SolNumb ) ;

	if not ( ProgramStatus in MIPOptimalityStatus ) then
	    MINLPTerminate;
	endif ;

The AIMMS parameters ``DeviationsPermitted`` and ``PenaltyMultiplier``
are part of the AOA module. By default, deviations are allowed and are
penalized with the value 1000 in the objective function of the master
MIP.

.. rubric:: ``FixIntegerVariablesAndSolveNLP``

The following procedure implements the next major step of the outer
approximation algorithm. First, the NLP subproblem is solved after
fixing all the integer variables in the MINLP model using the values
found from solving the previous master MIP problem. Then, if the
combination of integer values and feasible NLP solution values improves
the current MINLP incumbent solution, a new incumbent solution is set.
When the NLP subproblem does not produce a solution (either feasible or
infeasible), the outer approximation algorithm will be terminated.

.. code-block:: aimms

	return when ( MINLPAlgorithmHasFinished );

	SolveNLPSubProblem( 0 );
	ProgramStatus := GMP::Solution::GetProgramStatus( GNLP, SolNumb ) ;

	if ( ProgramStatus in NLPOptimalityStatus ) then
	    ! Save NLP solution as MINLP solution if no incumbent solution
	    ! has been found yet, or if the NLP solution is better than
	    ! the current incumbent.

	    if ( not IncumbentSolutionHasBeenFound ) then
	        ! Set incumbent solution for MINLP.

	        GMP::Solution::RetrieveFromModel( GMINLP, SolNumb ) ;
	        IncumbentSolutionHasBeenFound := 1 ;
	    else

	        NLPobjectiveValue   := GMP::Solution::GetObjective( GNLP  , SolNumb ) ;
	        MINLPIncumbentValue := GMP::Solution::GetObjective( GMINLP, SolNumb ) ;

	        if ( MINLPSolutionImprovement( NLPobjectiveValue, MINLPIncumbentValue ) ) then
	            ! Set incumbent solution for MINLP.

	            GMP::Solution::RetrieveFromModel( GMINLP, SolNumb ) ;
	            IncumbentSolutionHasBeenFound := 1 ;
	        endif;
	    endif ;
	else
	    ! Terminate if no linearization point has been found.

	    SolverStatus := GMP::Solution::GetSolverStatus( GNLP, SolNumb ) ;

	    if not ( SolverStatus in NLPContinuationStatus ) then
	        MINLPTerminate;
	    endif;
	endif ;

The AOA algorithm maintains the MINLP problem, the master MIP problem,
the NLP subproblem, and the incumbent solution of the MINLP. As a
result, direct access to the corresponding objective function values is
available.

.. rubric:: ``SolveNLPSubProblem``

The procedure ``SolveNLPSubProblem`` solves the NLP subproblem using
various routines from the GMP library. The procedure has a single
argument ``initialSolve`` which indicates whether this is the solve of
the initial relaxed MINLP problem. In that case some steps in the
procedure are not necessary.

.. code-block:: aimms

	if ( NLPUseInitialValues ) then
	    GMP::Solution::SendToModel( GNLP, SolNumbInitialValues ) ;
	elseif ( not initialSolve ) then
	    GMP::Solution::SendToModel( GMIP, SolNumb ) ;
	endif;

	GMP::Solution::RetrieveFromModel( GNLP, SolNumb ) ;
	GMP::Solution::SendToSolverSession( ssNLP, SolNumb ) ;

	if ( not initialSolve ) then
	    GMP::Instance::FixColumns( GNLP, GMIP, SolNumb, AllIntegerVariables ) ;
	endif;

	GMP::SolverSession::Execute( ssNLP ) ;

	GMP::Solution::RetrieveFromSolverSession( ssNLP, SolNumb ) ;
	GMP::Solution::SendToModel( GNLP, SolNumb ) ;

.. rubric:: ``TerminateOrPrepareForNextIteration``

The following procedure implements the final major step of the outer
approximation algorithm. If a termination flag has not been set
previously, and the maximum number of iterations has not yet been
reached, then the previously found integer solution of the master MIP
problem will be eliminated by adding the appropriate cuts. This will
ensure that the next master MIP will have a new integer solution (or
none at all).

.. code-block:: aimms

	return when ( MINLPAlgorithmHasFinished );

	if ( IterationCount = IterationMax ) then
	    MINLPTerminate;
	else
	    ! Prepare for next iteration

	    IterationCount += 1 ;
	    GMP::Solution::SetIterationCount( GMINLP, SolNumb, IterationCount ) ;
	    GMP::Instance::AddIntegerEliminationRows( GMIP, SolNumb, EliminationCount ) ;
	    EliminationCount += 1 ;
	endif ;

Note that you are responsible for determining the appropriate iteration
count for the overall outer approximation algorithm. As you are free to
develop a solution algorithm in any way you desire, it is not always
possible for the AOA algorithm to determine the correct setting of the
MINLP iteration count.