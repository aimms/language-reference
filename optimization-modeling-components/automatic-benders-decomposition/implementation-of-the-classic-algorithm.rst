.. _sec:benders.classic.impl:

Implementation of the Classic Algorithm
=======================================

.. rubric:: The procedure ``DoBendersDecomposition``

In this section we show the implementation of the classic Benders'
decomposition algorithm. It follows the classic approach of solving the
master problem and the subproblem in an alternating sequence. The
procedure ``DoBendersDecomposition``, introduced in
:ref:`sec:benders.quickstart`, implements the classic algorithm.

.. rubric:: Focus on textbook algorithm

The Benders' cuts can be generated in several ways; in this section we
focus on the approach used in the textbook algorithm of the previous
section (:ref:`sec:benders.textbook.alg`). The textbook algorithm uses
the dual formulation of the subproblem and can add both Benders'
optimality and feasibility cuts.

.. rubric:: Calling ``DoBendersDecompositionClassic``

We have to change some of the control parameters of
:ref:`this table <table:benders.controlparam>` to let the
``DoBendersDecomposition`` procedure execute the textbook algorithm. The
relevant changes are listed below.

.. code-block:: aimms

	generatedMP := GMP::Instance::Generate( SymbolicMP );

	! Settings needed to run textbook algorithm:
	GMPBenders::FeasibilityOnly := 0;
	GMPBenders::AddTighteningConstraints := 0;
	GMPBenders::UseDual := 1;
	GMPBenders::NormalizationType := 0;

	GMPBenders::DoBendersDecompositionClassic( generatedMP, AllIntegerVariables );

.. rubric:: Implementation of ``DoBendersDecompositionClassic``

The ``DoBendersDecompositionClassic`` procedure starts by making copies
of its input arguments. Next the master problem and the subproblem are
created. For the subproblem we also create a solver session which gives
us more flexibility passing and retrieving subproblem related
information. The parameters for the number of optimality and feasibility
cuts are reset. Finally, the procedure calls another procedure, namely
``BendersAlgorithm``, and finishes by deleting the master problem and
the subproblem. For the sake of brevity and clarity, we leave out parts
of the code that handle details like creating a status file; this will
also be the case for the other pieces of code shown in this chapter.

.. code-block:: aimms

	OriginalGMP := MyGMP ;
	VariablesMasterProblem := MyMasterVariables ;

	! Create (Relaxed) Master problem.
	gmpM := GMP::Benders::CreateMasterProblem( OriginalGMP, VariablesMasterProblem,
	                        'BendersMasterProblem',
	                        feasibilityOnly : FeasibilityOnly,
	                        addConstraints : AddTighteningConstraints ) ;

	! Create Subproblem.
	gmpS := GMP::Benders::CreateSubProblem( OriginalGMP, gmpM, 'BendersSubProblem',
	                        useDual : UseDual,
	                        normalizationType : NormalizationType );

	solsesS := GMP::Instance::CreateSolverSession( gmpS ) ;

	NumberOfOptimalityCuts  := 0;
	NumberOfFeasibilityCuts := 0;

	! Start the actual Benders' decomposition algorithm.
	BendersAlgorithm;

	GMP::Instance::Delete( gmpM );
	GMP::Instance::Delete( gmpS );

.. rubric:: The procedure ``BendersAlgorithm``

The ``BendersAlgorithm`` procedure implements the actual Benders'
decomposition algorithm. It initializes the algorithm by resetting the
parameters for the number of iterations, etc. Next the master problem is
solved. The separation step solves the subproblem and checks whether the
current solution is optimal. If it is not optimal then the algorithm
creates a constraint ("cut") that separates the current solution from
the set of feasible solutions. This constraint is added to the master
problem enforcing that the current solution of the master problem will
not be found again if we solve the master problem once again. This
alternating sequence of solving master problems and subproblems is
repeated until a stopping criterion is met.

.. code-block:: aimms

	InitializeAlgorithm;

	while ( not BendersAlgorithmFinished ) do

	    NumberOfIterations += 1;

	    SolveMasterProblem;

	    if ( UseDual ) then
	        if ( FeasibilityOnly ) then
	            SeparationFeasibilityOnlyDual;
	        else
	            SeparationOptimalityAndFeasibilityDual;
	        endif;
	    else
	        if ( FeasibilityOnly ) then
	            SeparationFeasibilityOnly;
	        else
	            SeparationOptimalityAndFeasibility;
	        endif;
	    endif;

	endwhile;

.. rubric:: Separation

The code above shows four possible ways of performing the separation
step. The textbook algorithm uses the procedure
``SeparationOptimalityAndFeasibilityDual`` which we will discuss below.
The other three separation procedures are discussed in
:ref:`app:bendersseparation`.

.. rubric:: The procedure ``SolveMasterProblem``

The implementation of the ``SolveMasterProblem`` procedure is
straightforward. This procedure solves the Benders' master problem and
retrieves its objective value after checking the program status. If the
program status is infeasible or unbounded then the algorithm terminates.

.. code-block:: aimms

	GMP::Instance::Solve( gmpM );

	ProgramStatus := GMP::Solution::GetProgramStatus( gmpM, 1 ) ;

	if ( ProgramStatus = 'Infeasible' ) then
	    return AlgorithmTerminate( 'Infeasible' );
	elseif ( ProgramStatus = 'Unbounded' ) then
	    return AlgorithmTerminate( 'ProgramNotSolved' );
	endif;

	ObjectiveMaster := GMP::Instance::GetObjective( gmpM );

.. rubric:: The procedure ``SeparationOptimalityAndFeasibilityDual``

The procedure ``SeparationOptimalityAndFeasibilityDual`` is called by
the Benders' decomposition algorithm in case the dual of the Benders'
subproblem is used and if both optimality and feasibility cuts can be
generated by the algorithm (we will discuss in
:ref:`sec:benders.control.par` the case in which only feasibility cuts
are generated). This procedure updates the dual subproblem and solves
it. If the dual subproblem is unbounded then a feasibility cut is added
to the master problem (using an unbounded extreme ray; see the next
paragraph). If the subproblem is bounded and optimal then the objective
value of the subproblem is compared to the objective value of the master
problem to check whether the algorithm has found an optimal solution for
the original problem. If the solution is not optimal yet then an
optimality cut is added to the master problem, using the level values of
the variables in the solution of the dual subproblem.

.. code-block:: aimms

	return when ( BendersAlgorithmFinished );

	GMP::Benders::UpdateSubProblem( gmpS, gmpM, 1, round : 1 );

	GMP::SolverSession::Execute( solsesS ) ;
	GMP::Solution::RetrieveFromSolverSession( solsesS, 1 ) ;

	ProgramStatus := GMP::Solution::GetProgramStatus( gmpS, 1 ) ;

	if ( ProgramStatus = 'Unbounded' ) then

	    ! Add feasibility cut to the Master problem.
	    NumberOfFeasibilityCuts += 1;
	    GMP::Benders::AddFeasibilityCut( gmpM, gmpS, 1, NumberOfFeasibilityCuts );

	else

	    ! Check whether optimality condition is satisfied.
	    ObjectiveSubProblem := GMP::SolverSession::GetObjective( solsesS );

	    if ( SolutionImprovement( ObjectiveSubProblem, BestObjective ) ) then
	        BestObjective := ObjectiveSubProblem;
	    endif;

	    if ( SolutionIsOptimal( ObjectiveSubProblem, ObjectiveMaster ) ) then
	        return AlgorithmTerminate( 'Optimal' );
	    endif;

	    ! Add optimality cut to the Master problem.
	    NumberOfOptimalityCuts += 1;
	    GMP::Benders::AddOptimalityCut( gmpM, gmpS, 1, NumberOfOptimalityCuts );

	endif;

.. rubric:: Unbounded extreme ray

In textbooks, if the dual subproblem is unbounded then an unbounded
extreme ray is chosen and used to generate a feasibility cut. Choosing
such an unbounded extreme ray is not trivial but luckily modern solvers
like CPLEX and Gurobi can compute an unbounded extreme ray upon request.
It is stored in the :ref:`.Level` suffix of the variables. The downside is
that preprocessing by CPLEX or Gurobi has to be switched off which can
have a negative impact on the performance. So, if the textbook algorithm
is selected in which the dual subproblem is used and both optimality and
feasibility cuts can be generated by the algorithm, the solver options
for switching on the calculation of unbounded extreme ray and for
switching off the preprocessor are set during the initialization of the
Benders' decomposition algorithm:

.. code-block:: aimms

	if ( UseDual and ( not FeasibilityOnly ) ) then
	    rval := GMP::SolverSession::SetOptionValue( solsesS, 'unbounded ray', 1 );
	    if ( rval = 0 ) then
	        halt with "Solver must support unbounded extreme rays.";
	        return;
	    endif;

	    rval := GMP::SolverSession::SetOptionValue( solsesS, 'presolve', 0 );
	    if ( rval = 0 ) then
	        halt with "Switching off the solver option 'presolve' failed.";
	        return;
	    endif;
	endif;

If the solver does not support unbounded extreme rays then the textbook
algorithm cannot be used.

.. rubric:: The procedure ``AlgorithmTerminate``

The procedure ``AlgorithmTerminate`` is called whenever the Benders'
decomposition algorithm is finished. Appropriate values are assigned to
the program and solver status of the original problem. If the algorithm
has found an optimal solution then the solutions of the last master
problem and last subproblem are combined into an optimal solution for
the original problem. In the code below, the uncommon situation in which
the algorithm terminates after hitting the iteration limit has been
omitted.

.. code-block:: aimms

	BendersAlgorithmFinished := 1;

	if ( ProgrStatus = 'Optimal' ) then
	    GMP::Solution::SetProgramStatus( OriginalGMP, 1, 'Optimal' ) ;
	    GMP::Solution::SetSolverStatus( OriginalGMP, 1, 'NormalCompletion' ) ;

	    GMP::Solution::SendToModel( gmpS, 1 ) ;

	    GMP::Solution::SendToModelSelection( gmpM, 1, VariablesMasterProblem,
	                                         AllSuffixNames );
	    GMP::Solution::RetrieveFromModel( OriginalGMP, 1 );

	    GMP::Solution::SetObjective( OriginalGMP, 1, BestObjective );
	    GMP::Solution::SendToModel( OriginalGMP, 1 );
	elseif ( ProgrStatus = 'Infeasible' ) then
	    GMP::Solution::SetProgramStatus( OriginalGMP, 1, 'Infeasible' ) ;
	    GMP::Solution::SetSolverStatus( OriginalGMP, 1, 'NormalCompletion' ) ;
	elseif ( ProgrStatus = 'Unbounded' ) then
	    GMP::Solution::SetProgramStatus( OriginalGMP, 1, 'Unbounded' ) ;
	    GMP::Solution::SetSolverStatus( OriginalGMP, 1, 'NormalCompletion' ) ;
	else
	    GMP::Solution::SetProgramStatus( OriginalGMP, 1, 'ProgramNotSolved' ) ;
	    GMP::Solution::SetSolverStatus( OriginalGMP, 1, 'SetupFailure' ) ;
	endif;