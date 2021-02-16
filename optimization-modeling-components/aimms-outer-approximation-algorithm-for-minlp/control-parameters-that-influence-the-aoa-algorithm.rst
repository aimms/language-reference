.. _sec:aoa.control.par:

Control Parameters That Influence the AOA Algorithm
===================================================

.. rubric:: Control parameters

The multistart module defines several parameters that influence the
outer approximation algorithm. These parameters have a similar
functionality as options of a solver, e.g., CPLEX. The most important
parameters, with their default setting, are shown in
:ref:`this table <table:aoa.controlparam>`.

.. _table:aoa.controlparam:

.. table:: Control parameters in the outer approximation module

   +-------------------------------------+---------+------------+--------------------------------+
   | Parameter                           | Default | Range      | Subsection                     |
   +=====================================+=========+============+================================+
   | ``IterationMax``                    | 20      | {0,maxint} |                                |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``TimeLimit``                       | 0       | {0,maxint} | :ref:`sec:aoa.time.limit`      |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``CreateStatusFile``                | 0       | {0,1}      |                                |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``UsePresolver``                    | 1       | {0,1}      | :ref:`sec:aoa.presolver`       |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``UseMultistart``                   | 0       | {0,1}      | :ref:`sec:aoa.multistart`      |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``TerminateAfterFirstNLPIsInteger`` | 1       | {0,1}      | :ref:`sec:aoa.terminate.first` |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``IsConvex``                        | 0       | {0,1}      | :ref:`sec:aoa.convex`          |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``RelativeOptimalityTolerance``     | 1e-5    | {0,1}      | :ref:`sec:aoa.convex`          |
   +-------------------------------------+---------+------------+--------------------------------+
   | ``NLPUseInitialValues``             | 1       | {0,1}      | :ref:`sec:aoa.nlp.use.initial` |
   +-------------------------------------+---------+------------+--------------------------------+

The parameters that are not self-explanatory are explained in this
section; the last column in the table refers to the subsection that
discusses the corresponding parameter.

.. _sec:aoa.time.limit:

Specifying a Time Limit
-----------------------

.. rubric:: Parameter ``TimeLimit``

The parameter ``TimeLimit`` can be used to set a limit on the total
elapsed time (in seconds) used by the outer approximation algorithm. The
default value of 0 has a special meaning; in that case there is no time
limit.

.. _sec:aoa.presolver:

Using the AIMMS Presolver
-------------------------

.. rubric:: Parameter ``UsePresolver``

By default the outer approximation algorithm starts by applying the
AIMMS Presolver to the MINLP model. By preprocessing the MINLP model,
the model might become smaller and easier to solve. The parameter
``UsePresolver`` can be used to switch off the preprocessing step.

.. _sec:aoa.multistart:

Combining Outer Approximation with Multistart
---------------------------------------------

.. rubric:: Parameter ``UseMultistart``

If the parameter ``UseMultistart`` is switched on then the outer
approximation algorithm will use the multistart algorithm to solve the
nonlinear subproblems. For non-convex models this can have a positive
effect on the quality of the solution that is returned by the outer
approximation algorithm. The multistart algorithm is described in
section :ref:`sec:nlp.multistart`. The parameters
``MultistartNumberOfSamplePoints`` and
``MultistartNumberOfSelectedSamplePoints`` can be used to specify the
number of sample and selected sample points, respecively, as used by the
multistart algorithm.

.. rubric:: Multistart module

To use the multistart algorithm, the system module ``Multi Start``
should be added to your project. You can install this module using the
**Install System Module** command in the AIMMS **Settings** menu.

.. _sec:aoa.terminate.first:

Terminate If Solution of Relaxed Model Is Integer
-------------------------------------------------

.. rubric:: Parameter ``TerminateAfterFirstNLPIsInteger``

By default the outer approximation algorithm will terminate if it finds
an integer solution for the initial NLP problem, which is obtained from
the MINLP model by relaxing the integer variables. By switching off the
parameter ``TerminateAfterFirstNLPIsInteger`` you can enforce the
algorithm to continue.

.. _sec:aoa.convex:

Solving a Convex Model
----------------------

.. rubric:: Parameter ``IsConvex``

The parameter ``IsConvex`` can be used to indicate that the model is
convex. In that case the outer approximation algorithm will no longer
stop after the iteration limit is hit, as specified by the parameter
``IterationMax``. Instead, the algorithm will stop if the gap between
the objective values of the master MIP problem and the nonlinear
subproblem is sufficiently small, as controlled by the parameter
``RelativeOptimalityTolerance``. Note that AIMMS cannot identify whether
a model is convex or not.

.. _sec:aoa.nlp.use.initial:

Starting Point Strategy for NLP Subproblems
-------------------------------------------

.. rubric:: Parameter ``NLPUseInitialValues``

The parameter ``NLPUseInitialValues`` specifies the starting point
strategy used for solving the NLP subproblems. For nonconvex nonlinear
problems the starting point often has a big influence on the solution
that the NLP solver will find. By default the AOA algorithm will use the
initial values as provided by the user for all NLP subproblems that are
solved. By setting this parameter to 0, the algorithm will use the
solution of the previous master MIP problem as the starting point for
the next NLP subproblem (and for the initial NLP it will use the initial
values provided by the user). Note: if one of the parameters
``UseMultistart`` or ``IsConvex`` equals 1 then ``NLPUseInitialValues``
is automatically set to 0.