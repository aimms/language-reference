.. _sec:benders.modern.impl:

Implementation of the Modern Algorithm
======================================

.. rubric:: Single MIP

When solving a MIP problem, the classic Benders' decomposition algorithm
often spends a large amount of time in solving the master MIP problems
in which a significant amount of rework is done. In the modern approach
only one single master MIP problem is solved. Whenever the solver finds
a feasible integer solution for the master problem, the subproblem
:math:`PS(x^*)` is solved after fixing the master problem variable
:math:`x^*` according to this integer solution.

.. rubric:: Callbacks

Modern MIP solvers like CPLEX and Gurobi allow the user control over the
solution process by so-called *callbacks*. Callbacks allow user code in
AIMMS to be executed regularly during an optimization process. If the
solver finds a new candidate integer solution then the user has the
possibility to let the solver call one or more callback procedures. One
of these callbacks is the callback for lazy constraints; that callback
is used in the modern Benders' decomposition algorithm.

.. rubric:: Feasible solutions

If no violated Benders' cut can be generated, after solving the
subproblem, then we have found a feasible solution for the original
problem and we can accept the current feasible integer solution as a
"correct" solution for the master MIP problem. In the classic algorithm
we would now be finished because we would know that no better solution
of the original problem exists. In the modern algorithm we have to
continue solving the master MIP problem because there might still exist
a solution to the master MIP problem that results in a better solution
for the original problem.

.. rubric:: Lazy constraints

If a Benders' optimality or feasibility cut is found then this will be
added as a so-called *lazy constraint* to the master MIP problem. Lazy
constraints are constraints that represent one part of the model;
without them the model would be incomplete. In this case the actual
model that we want to solve is the original problem but we are solving
the master MIP problem instead. The Benders' cuts represent the
subproblem part of the model and we add them whenever we find one that
is violated.

.. rubric:: Implementation of ``DoBendersDecompositionSingleMIP``

In the remainder of this section we show the implementation of the
modern Benders' decomposition algorithm as implemented by the procedure
``DoBendersDecompositionSingleMIP`` which was introduced in
:ref:`sec:benders.quickstart`. Similar to the procedure
``DoBendersDecompositionClassic``, the procedure
``DoBendersDecompositionSingleMIP`` starts by making copies of its input
arguments. Next the master problem and the subproblem are created. The
parameters for the number of optimality and feasibility cuts are reset.
Finally, the procedure calls another procedure, namely
``BendersAlgorithmSingleMIP``, and finishes by deleting the master
problem and the subproblem. As before we leave out parts of the code
that handle details like creating a status file, for the sake of brevity
and clarity.

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
	BendersAlgorithmSingleMIP;

	GMP::Instance::Delete( gmpM );
	GMP::Instance::Delete( gmpS );

.. rubric:: The procedure ``BendersAlgorithmSingleMIP``

The ``BendersAlgorithmSingleMIP`` procedure initializes the algorithm by
resetting the parameters for the number of iterations, etc. Then it
calls the procedure ``SolveMasterMIP`` which does the actual work.

.. code-block:: aimms

	InitializeAlgorithmSingleMIP;

	SolveMasterMIP;

.. rubric:: The procedure ``SolveMasterMIP``

The ``SolveMasterMIP`` procedure implements the actual Benders'
decomposition algorithm using the modern approach. It first installs a
lazy constraint callback for which the module implements four different
versions. We assume that the control parameters have their default
settings (see :ref:`this table <table:benders.controlparam>`) in which case the
procedure ``BendersCallbackLazyFeasOnlySingleMIP`` is installed. Next
the master problem is solved and if a feasible solution is found, the
subproblem is solved one last time to obtain a combined optimal solution
for the original problem. Finally the algorithm terminates.

.. code-block:: aimms

	if ( UseDual ) then
	    if ( FeasibilityOnly ) then
	        GMP::Instance::SetCallbackAddLazyConstraint( gmpM,
	                         'GMPBenders::BendersCallbackLazyFeasOnlyDualSingleMIP' );
	    else
	        GMP::Instance::SetCallbackAddLazyConstraint( gmpM,
	                         'GMPBenders::BendersCallbackLazyOptAndFeasDualSingleMIP' );
	    endif;
	else
	    if ( FeasibilityOnly ) then
	        GMP::Instance::SetCallbackAddLazyConstraint( gmpM,
	                         'GMPBenders::BendersCallbackLazyFeasOnlySingleMIP' );
	    else
	        GMP::Instance::SetCallbackAddLazyConstraint( gmpM,
	                         'GMPBenders::BendersCallbackLazyOptAndFeasSingleMIP' );
	    endif;
	endif;

	GMP::Instance::Solve( gmpM );

	ProgramStatus := GMP::Solution::GetProgramStatus( gmpM, 1 ) ;

	if ( ProgramStatus = 'Infeasible' ) then
	    AlgorithmTerminateSingleMIP( 'Infeasible' );
	else
	    if ( FeasibilityOnly and not UseDual ) then
	        ! Solve feasibility problem fixing the optimal solution of the
	        ! Master problem.
	        GMP::Solution::SendToModel( gmpM, 1 );

	        ! Update feasibility problem and solve it.
	        GMP::Benders::UpdateSubProblem( gmpF, gmpM, 1, round : 1 );
	        GMP::Instance::Solve( gmpF );
	    else
	        ! Solve Subproblem fixing the optimal solution of the Master problem.
	        GMP::Solution::SendToModel( gmpM, 1 );

	        ! Update Subproblem and solve it.
	        GMP::Benders::UpdateSubProblem( gmpS, gmpM, 1, round : 1 );
	        GMP::Instance::Solve( gmpS );
	    endif;

	    AlgorithmTerminateSingleMIP( 'Optimal' );
	endif;

.. rubric:: The procedure ``BendersCallbackLazyFeasOnlySingleMIP``

The callback procedure ``BendersCallbackLazyFeasOnlySingleMIP`` is
called by the MIP solver whenever it finds a candidate integer solution
for the master problem. This procedure retrieves the candidate integer
solution from the MIP solver. Then it creates the feasibility problem
for the (primal) subproblem if it does not exist yet. The feasibility
problem is updated and solved. If its optimal objective value is larger
than 0, indicating that the subproblem would have been infeasible, we
add a feasibility cut as a lazy constraint to the master MIP. The MIP
solver will not treat this candidate integer solution as a real
solution. If the optimal objective value equals 0 (or is negative) then
we do not add a lazy constraint in which case the MIP solver accepts the
candidate solution as a real solution. Finally, the callback procedure
returns 1 such that the solution process of the master MIP problem
continues.

.. code-block:: aimms

	! Get MIP incumbent solution.
	GMP::Solution::RetrieveFromSolverSession( ThisSession, 1 );
	GMP::Solution::SendToModel( gmpM, 1 );

	! Create feasibility problem corresponding to Subproblem (if it does not exist yet).
	if ( not FeasibilityProblemCreated ) then
	    gmpF := GMP::Instance::CreateFeasibility( gmpS, "FeasProb",
	                             useMinMax : UseMinMaxForFeasibilityProblem );
	    solsesF := GMP::Instance::CreateSolverSession( gmpF ) ;
	    FeasibilityProblemCreated := 1;
	endif;

	! Update feasibility problem corresponding to Subproblem and solve it.
	GMP::Benders::UpdateSubProblem( gmpF, gmpM, 1, round : 1 );

	GMP::SolverSession::Execute( solsesF ) ;
	GMP::Solution::RetrieveFromSolverSession( solsesF, 1 ) ;

	! Check whether objective is 0 in which case optimality condition is satisfied.
	ObjectiveFeasProblem := GMP::SolverSession::GetObjective( solsesF );

	if ( ObjectiveFeasProblem <= BendersOptimalityTolerance ) then
	    return 1;
	endif;

	! Add feasibility cut to the Master problem.
	NumberOfFeasibilityCuts += 1;
	GMP::SolverSession::AddBendersFeasibilityCut( ThisSession, gmpF, 1 );

	return 1;

.. rubric:: The procedure ``AlgorithmTerminateSingleMIP``

The procedure ``AlgorithmTerminateSingleMIP`` is called to finish the
Benders' decomposition algorithm. This procedure is called directly
after the master MIP problem is solved. Its implementation is similar to
that of the procedure ``AlgorithmTerminate`` of
:ref:`sec:benders.classic.impl` and therefore omitted.