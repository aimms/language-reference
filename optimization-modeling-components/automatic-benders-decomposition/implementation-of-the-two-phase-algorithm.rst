.. _sec:benders.twophase.impl:

Implementation of the Two Phase Algorithm
=========================================

.. rubric:: First phase

The Benders' module also implements a two phase algorithm for MIP
problems. In the first phase it solves the relaxed problem in which the
integer variables become continuous. The resulting relaxed MIP problem
is then solved using the classic Benders' decomposition algorithm in
order to find Benders' cuts.

.. rubric:: Second phase

The second phase solves the original MIP problem. The master problem
created in the first phase is also used in the second phase but without
relaxing the integer variables. The Benders' cuts that were added during
the first phase are not removed; these cuts are still valid. In general
the relaxed MIP problem can be solved more efficiently than the MIP
problem using Benders' decomposition, and the hope is that by adding the
Benders' cuts found during the first phase, the Benders' decomposition
algorithm needs considerably less iterations in the second phase to
solve the original MIP problem.

.. rubric:: Implementation of ``DoBendersDecompositionTwoPhase``

The procedure ``DoBendersDecompositionTwoPhase`` implements the two
phase algorithm. It starts by making copies of its first two input
arguments. Next the master problem and the subproblem are created. The
parameters for the number of optimality and feasibility cuts are reset.
The problem type of the master problem is changed from 'MIP' to 'RMIP'
which basically changes the integer variables into continuous variables.
The procedure ``BendersAlgorithm`` then solves the relaxed problem using
the classic Benders' decomposition algorithm; see
:ref:`sec:benders.classic.impl` for its implementation. After checking
the program status of the relaxed master problem the algorithm continues
by switching the problem type of the master problem back to 'MIP'. Next
the original problem is solved using either procedure
``BendersAlgorithmSingleMIP`` (:ref:`sec:benders.modern.impl`) or
``BendersAlgorithm`` (:ref:`sec:benders.classic.impl`). The algorithm
ends by deleting the master problem and the subproblem. As before we
leave out parts of the code that handle details like creating a status
file, for the sake of brevity and clarity.

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

	! Start the classic Benders' decomposition algorithm for the relaxed Master
	! MIP problem.
	GMP::Instance::SetMathematicalProgrammingType( gmpM, 'RMIP' );

	IterationLimit := IterationLimitPhaseSingle;

	BendersAlgorithm;

	ProgramStatus := GMP::Solution::GetProgramStatus( OriginalGMP, 1 );

	if ( ProgramStatus = 'Infeasible' or
	     ProgramStatus = 'Unbounded'  ) then
	    DoPhaseTwo := 0;
	endif;

	if ( DoPhaseTwo ) then
	    ! Switch back math program type.
	    GMP::Instance::SetMathematicalProgrammingType( gmpM, 'MIP' );

	    if ( UseSingleMIP ) then
	        ! Start the Single MIP Tree Benders' decomposition algorithm.
	        BendersAlgorithmSingleMIP;
	    else
	        IterationLimit := IterationLimitPhaseTwo;

	        BendersAlgorithm;
	    endif;
	endif;

	GMP::Instance::Delete( gmpM );
	GMP::Instance::Delete( gmpS );

.. rubric:: Iteration and time limit

The section in the Benders' module for the two phase algorithm contains
two extra control parameters for setting the iteration and time limit
used by the classic Benders' decomposition algorithm in the second
phase. These parameters are ``IterationLimitPhaseTwo`` and
``TimeLimitPhaseTwo`` respectively. The parameters ``IterationLimit``
and ``TimeLimit`` are used in the first phase. In some cases it might be
a good strategy to limit the number of iterations (or the running time)
during the first phase. The two phase algorithm will then still find a
global optimal solution of the original problem as long as the second
phase terminates normally. If the modern approach (with a single MIP
tree) is used in the second phase then the general solver options
``iteration_limit`` and ``time_limit`` are used for the second phase.