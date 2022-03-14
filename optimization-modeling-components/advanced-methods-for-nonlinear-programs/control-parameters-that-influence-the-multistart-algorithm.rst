.. _sec:multistart.control.par:

Control Parameters That Influence the Multistart Algorithm
==========================================================

.. rubric:: Control parameters

The multistart module defines several parameters that influence the
multistart algorithm. These parameters have a similar functionality as
options of a solver, e.g., CPLEX. The most important parameters, with
their default setting, are shown in
:ref:`this table <table:multistart.controlparam>`.

.. _table:multistart.controlparam:

.. table:: Control parameters in the multistart module

   +----------------------------------+---------+------------+------------------------------------------+
   | Parameter                        | Default | Range      | Subsection                               |
   +==================================+=========+============+==========================================+
   | ``IterationLimit``               | 5       | {1,maxint} | :ref:`sec:multistart.iteration.limit`    |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``TimeLimit``                    | 0       | {0,maxint} | :ref:`sec:multistart.time.limit`         |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``TimeLimitSingleSolve``         | 0       | {0,maxint} | :ref:`sec:multistart.time.limit`         |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``ThreadLimit``                  | 0       | {0,maxint} | :ref:`sec:multistart.thread.limit`       |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``UseOpportunisticAlgorithm``    | 0       | {0,1}      | :ref:`sec:multistart.oppor.mode`         |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``NumberOfBestSolutions``        | 1       | {1,1000}   | :ref:`sec:multistart.multiple.solutions` |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``ShrinkFactor``                 | 0.95    | [0,1]      | :ref:`sec:multistart.shrink.factor`      |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``UsePresolver``                 | 1       | {0,1}      | :ref:`sec:multistart.aimms.presolver`    |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``UseInitialPoint``              | 1       | {0,1}      | :ref:`sec:multistart.starting.point`     |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``UseConstraintConsensusMethod`` | 0       | {-1,1}     | :ref:`sec:multistart.improve.sample`     |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``MaximalVariableBound``         | 1000    | [0,inf)    | :ref:`sec:multistart.unbounded.vars`     |
   +----------------------------------+---------+------------+------------------------------------------+
   | ``ShowSolverProgress``           | 0       | {0,1}      | :ref:`sec:multistart.solver.progress`    |
   +----------------------------------+---------+------------+------------------------------------------+

The parameters that are not self-explanatory are explained in this
section; the last column in the table refers to the subsection that
discusses the corresponding parameter.

.. _sec:multistart.iteration.limit:

Specifying an Iteration Limit
-----------------------------

.. rubric:: Parameter ``IterationLimit``

The parameter ``IterationLimit`` can be used to set a limit on the
number of iterations used by the multistart algorithm. This limit is used
in the basic algorithm and in the first phase of the dynamic algorithm.

.. _sec:multistart.time.limit:

Specifying a Time Limit
-----------------------

.. rubric:: Parameter ``TimeLimit``

The parameter ``TimeLimit`` can be used to set a limit on the total
elapsed time (in seconds) used by the multistart algorithm. The default
value of 0 has a special meaning; in that case there is no time limit.

.. rubric:: Parameter ``TimeLimitSingleSolve``

It is also possible to set a time limit for every single solve started
by the multistart algorithm by using the parameter
``TimeLimitSingleSolve``. Also the default value of 0 of this parameter
has a special meaning; in that case there is no time limit.

.. _sec:multistart.thread.limit:

Using Multiple Threads
----------------------

.. rubric:: Parameter ``ThreadLimit``

The parameter ``ThreadLimit`` controls the number of threads that should
be used by the multistart algorithm. Each thread will be used to solve
one NLP using an asynchronous solver session. At its default setting of
0, the algorithm will automatically use the maximum number of threads,
which is limited by the number of cores on the machine and the amount of
solver sessions allowed by the AIMMS license.

.. _sec:multistart.oppor.mode:

Deterministic Versus Opportunistic
----------------------------------

.. rubric:: Parameter ``UseOpportunisticAlgorithm``

By default the multistart algorithm runs in deterministic mode.
Deterministic means that multiple runs with the same model using the
same parameter settings and the same solver on the same computer will
reproduce the same results. The number of NLP problems solved by the
multistart algorithm will then also be the same. In contrast,
opportunistic implies that the results, and the number of NLP problems
solved, might be different. Usually the opportunistic mode provides
better performance. The parameter ``UseOpportunisticAlgorithm`` can be
used to switch to the opportunistic mode. Note that the multistart
algorithm will always be deterministic if the algorithm uses only one
thread.

.. _sec:multistart.multiple.solutions:

Getting Multiple Solutions
--------------------------

.. rubric:: Parameter ``NumberOfBestSolutions``

By default the multistart algorithm will return one solution, namely the
best solution that the algorithm finds. By setting the parameter
``NumberOfBestSolutions`` to a value higher than 1, the multistart
algorithm will store the best :math:`n` solutions found in the solution
repository (see :ref:`sec:gmp.solution`). Here :math:`n` denotes the
value of this parameter.

.. _sec:multistart.shrink.factor:

Shrinking the Clusters
----------------------

.. rubric:: Parameter ``ShrinkFactor``

The clusters created by the multistart algorithm would normally grow as
more and more points are assigned to the clusters. As a side effect, a
new sample point is then more likely to be directly assigned to a
cluster, in which case no NLP is solved for that sample point, thereby
increasing the chance that it ends up in the wrong cluster. To overcome
this problem, the multistart algorithm automatically shrinks all
clusters after each iteration by a constant factor which is specified by
the parameter ``ShrinkFactor``.

.. _sec:multistart.aimms.presolver:

Combining Multistart and Presolver
----------------------------------

.. rubric:: Parameter ``UsePresolver``

By default the multistart algorithm starts by applying the AIMMS
Presolver to the NLP problem. By preprocessing the problem, the ranges
of the variables might become smaller which has a positive effect on the
multistart algorithm as then the randomly generated sample points are
more likely to be good starting points. The parameter ``UsePresolver``
can be used to switch off the preprocessing step.

.. _sec:multistart.starting.point:

Using a Starting Point
----------------------

.. rubric:: Parameter ``UseInitialPoint``

Sometimes the level values, assigned to the variables before solving the
NLP problem, provide a good starting point. By default the multistart
algorithm will use this initial point as the first sample point but only
in the first iteration. This behavior is controlled by the parameter
``UseInitialPoint``.

.. _sec:multistart.improve.sample:

Improving the Sample Points
---------------------------

.. rubric:: Parameter ``UseConstraintConsensusMethod``

The sample points are randomly generated by using the intervals defined
by the lower and upper bounds of the variables. Such a sample point is
very likely to be infeasible with respect to the constraints. The
constraint consensus method, which is described in :cite:`bib:Ch04`, tries to
find an approximately feasible point for a sample point. Using this
method might slow down the multistart algorithm but the chance of
generating (almost) feasible sample points increases. The constraint
consensus method can be activated by using the parameter
``UseConstraintConsensusMethod``. If this parameter is set to 1 then the
constraint consensus method will be used whenever possible, and if it is
set to -1 then it will never be used. At its default value of 0, the
algorithm automatically decides when to use the constraint consensus
method.

.. _sec:multistart.unbounded.vars:

Unbounded Variables
-------------------

.. rubric:: Parameter ``MaximalVariableBound``

A multistart algorithm requires that all variable bounds are finite.
Therefore the multistart algorithm in AIMMS will use a fixed value for
all infinite upper and lower variable bounds. This fixed value is
specified by the parameter ``MaximalVariableBound``. The value of this
parameter might be updated automatically in case the dynamic algorithm
is used.

.. _sec:multistart.solver.progress:

Solver Progress
---------------

.. rubric:: Parameter ``ShowSolverProgress``

By default the progress window will only show general progress
information for the multistart algorithm, including the objective value,
the number of iterations, the elapsed time, etc. By switching on the
parameter ``ShowSolverProgress`` also progress information by the NLP
solver will be displayed. If multiple solver sessions are (asynchronous)
executing at the same time then only the progress information of one of
them will be shown.