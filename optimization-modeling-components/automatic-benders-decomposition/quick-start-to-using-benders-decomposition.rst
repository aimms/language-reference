.. _sec:benders.quickstart:

Quick Start to Using Benders' Decomposition
===========================================

.. rubric:: System module

The system module with the name ``GMP Benders Decomposition`` implements
the Benders' decomposition algorithm. You can add this module to your
project using the **Install System Module** command in the AIMMS
**Settings** menu. This module contains three procedures that can be
called, each implementing a different algorithm.

.. rubric:: Classic algorithm

The procedure ``DoBendersDecompositionClassic`` inside this module
implements the classic version of the Benders' decomposition algorithm,
in which the master problem and the subproblem are solved in an
alternating sequence.

.. rubric:: Modern algorithm

The procedure ``DoBendersDecompositionSingleMIP`` inside the module
implements the modern approach for MIP problems which solves only a
single MIP problem; the subproblem is solved whenever the MIP solver
finds a solution for the master problem (using callbacks).

.. rubric:: Two phase algorithm

The procedure ``DoBendersDecompositionTwoPhase`` inside the module
implements a two phase algorithm for MIP problems. In the first phase it
solves the relaxed problem (in which the integer variables become
continuous) using the classic Benders decomposition algorithm. The
Benders' cuts found in the first phase are then added to the master
problem in the second phase after which the MIP problem is solved using
either the classic or modern approach of the Benders decomposition
algorithm.

.. rubric:: The procedure ``DoBendersDecompositionClassic``

The procedure ``DoBendersDecompositionClassic`` has two input arguments:

#. ``MyGMP``, an element parameter with range
   :any:`AllGeneratedMathematicalPrograms`, and

#. ``MyMasterVariables``, a subset of the predefined set
   :any:`AllVariables` defining the variables in the master problem.

For a MIP problem, the integer variables typically become the variables
of the master problem, although it is possible to also include
continuous variables in the set of master problem variables. The
``DoBendersDecompositionClassic`` procedure is called as follows:

.. code-block:: aimms

	generatedMP := GMP::Instance::Generate( SymbolicMP );

	GMPBenders::DoBendersDecompositionClassic( generatedMP, AllIntegerVariables );

Here ``SymbolicMP`` is the symbolic mathematical program containing the
MIP model, and ``generatedMP`` is an element parameter in the predefined
set :any:`AllGeneratedMathematicalPrograms`. ``GMPBenders`` is the prefix
of the Benders' module. The implementation of this procedure will be
discussed in :ref:`sec:benders.textbook.alg`.

.. rubric:: The procedure ``DoBendersDecompositionSingleMIP``

The procedure ``DoBendersDecompositionSingleMIP`` has the same input
arguments as the procedure ``DoBendersDecompositionClassic``. The
``DoBendersDecompositionSingleMIP`` procedure is called as follows:

.. code-block:: aimms

	generatedMP := GMP::Instance::Generate( SymbolicMP );

	GMPBenders::DoBendersDecompositionSingleMIP( generatedMP, AllIntegerVariables );

This procedure can only be used if the original problem contains some
integer variables. The implementation of this procedure will be
discussed in :ref:`sec:benders.modern.impl`.

.. rubric:: The procedure ``DoBendersDecompositionTwoPhase``

The procedure ``DoBendersDecompositionTwoPhase`` has one additional
argument compared to the procedure ``DoBendersDecompositionClassic``.
Namely, the third argument ``UseSingleMIP`` is used to indicate whether
the second phase should use the classic algorithm (value 0) or the
modern algorithm (value 1). The procedure is called as follows if the
modern algorithm should be used:

.. code-block:: aimms

	generatedMP := GMP::Instance::Generate( SymbolicMP );

	GMPBenders::DoBendersDecompositionTwoPhase( generatedMP, AllIntegerVariables, 1 );

This procedure should only be used if the original problem contains some
integer variables. The implementation of this procedure will be
discussed in :ref:`sec:benders.twophase.impl`.

.. rubric:: Combining procedure

To make it easier for you to switch between the three algorithms, the
module also implements the procedure ``DoBendersDecomposition`` that
calls one of the three procedures above based on the Benders' mode. The
first two arguments of this procedure are the same as before, namely
``MyGMP`` and ``MyMasterVariables``. The third argument,
``BendersMode``, is an element parameter that defines the Benders' mode
and can take value ``'Classic'``, ``'Modern'``, ``'TwoPhaseClassic'`` or
``'TwoPhaseModern'``. The procedure is called as follows if the two
phase algorithm should be used with the modern algorithm for the second
phase:

.. code-block:: aimms

	generatedMP := GMP::Instance::Generate( SymbolicMP );

	GMPBenders::DoBendersDecomposition( generatedMP, AllIntegerVariables,
	                                    'TwoPhaseModern' );

If the problem contains no integer variables then only mode
``'Classic'`` can be used.

.. rubric:: Control parameters

The Benders' module defines several parameters that influence the
Benders' decomposition algorithm. These parameters have a similar
functionality as options of a solver, e.g., CPLEX. The most important
parameters, with their default setting, are shown in
:numref:`table:benders.controlparam`.

.. _table:benders.controlparam:

.. table:: Control parameters in the Benders' module

   +------------------------------------+---------+------------+------------------------------------+
   | Parameter                          | Default | Range      | Subsection                         |
   +====================================+=========+============+====================================+
   | ``BendersOptimalityTolerance``     | 1e-6    | [0,1]      |                                    |
   +------------------------------------+---------+------------+------------------------------------+
   | ``IterationLimit``                 | 1e7     | {1,maxint} |                                    |
   +------------------------------------+---------+------------+------------------------------------+
   | ``TimeLimit``                      | 1e9     | [0,inf)    |                                    |
   +------------------------------------+---------+------------+------------------------------------+
   | ``CreateStatusFile``               | 0       | {0,1}      |                                    |
   +------------------------------------+---------+------------+------------------------------------+
   | ``UseDual``                        | 0       | {0,1}      | :ref:`sec:benders.primaldual.sub`  |
   +------------------------------------+---------+------------+------------------------------------+
   | ``FeasibilityOnly``                | 1       | {0,1}      | :ref:`sec:benders.feas.prob`       |
   +------------------------------------+---------+------------+------------------------------------+
   | ``NormalizationType``              | 1       | {0,1}      | :ref:`sec:benders.normalization`   |
   +------------------------------------+---------+------------+------------------------------------+
   | ``UseMinMaxForFeasibilityProblem`` | 1       | {0,1}      | :ref:`sec:benders.feas.mode`       |
   +------------------------------------+---------+------------+------------------------------------+
   | ``AddTighteningConstraints``       | 1       | {0,1}      | :ref:`sec:benders.tight.cons`      |
   +------------------------------------+---------+------------+------------------------------------+
   | ``UseStartingPointForMaster``      | 0       | {0,1}      | :ref:`sec:benders.start.point`     |
   +------------------------------------+---------+------------+------------------------------------+
   | ``UsePresolver``                   | 0       | {0,1}      | :ref:`sec:benders.aimms.presolver` |
   +------------------------------------+---------+------------+------------------------------------+

The parameters that are not self-explanatory are explained in
:ref:`sec:benders.control.par`; the last column in the table refers to
the subsection that discusses the corresponding parameter.

.. rubric:: Optimality tolerance

The optimality tolerance, as controlled by the parameter
``BendersOptimalityTolerance``, guarantees that a solution returned by
the Benders' decomposition algorithm lies within a certain percentage of
the optimal solution.

.. rubric:: Solver options

The parameters ``BendersOptimalityTolerance``, ``IterationLimit`` and
``TimeLimit`` are used by the classic algorithm (and the first phase of
the two phase algorithm). For the modern algorithm, the corresponding
general solver options, ``MIP_relative_optimality_tolerance``,
``iteration_limit`` and ``time_limit`` respectively, are used.