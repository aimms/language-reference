Modeling, Solving and Searching
===============================

.. rubric:: Introduction

In this section we explain how constraint programming models are
formulated and solved in AIMMS. We start by explaining how constraint
programming formulations are fit into the paradigms of AIMMS like the
free objective and units of measurement. We then explain the different
mathematical programming types associated to constraint programming, and
finally we discuss how a user can modify the search procedure in AIMMS.

.. rubric:: The free objective

By design, the objective of any mathematical program in AIMMS is a
*free* variable, even when it can be deduced that the objective function
is always integer valued for a feasible solution. However, for an
infeasible solution, AIMMS will assign the special value ``NA`` to the
objective variable, in order to emphasize that a feasible solution is
not available. Having a single variable for the objective function is
convenient when communicating its value in the progress window and other
places of AIMMS.

Constraint Programming and Units of Measurement
-----------------------------------------------

.. rubric:: Integer coefficients only

Constraint programming solvers require the coefficients used in
constraints to be integer; fractional values or special values such as
``-inf``, ``zero``, ``na``, ``undf``, or ``inf`` are not allowed. In
applications where the choice of base units is free, fractional values
are easily avoided by choosing the base unit of quantities, and the
units of variables and constraints such that all amounts to be
considered are integer multiples of those base units, as detailed in
:ref:`sec:units.scaling.mp`. As an example, consider a simple constraint
stating that the integer variable ``y`` is 0.9[m] away from the integer
variable ``x``. Both variables are multiples of the derived unit dm,
i.e., 0.1[m]. The variables and constraints are declared as follows:

.. code-block:: aimms

	Variable x {
	    Range       :  integer;
	    Unit        :  dm;
	}
	Variable y {
	    Range       :  integer;
	    Unit        :  dm;
	}
	Constraint y_away_from_x {
	    Unit        :  dm;
	    Definition  :  y = abs( x - 0.9[m] );
	}

Using the unit ``m`` as a base unit, this will lead to fractional
values, as can be seen in the constraint listing:

.. code-block:: aimms

	y_away_from_x .. [ 1 | 1 | before ]

	    y =
	    abs((x-0.9))  ****

	    name            lower           level           upper           scale
	    x                   0               0 21474836470.000           0.100
	    y                   0               0 21474836470.000           0.100

The coefficient for distance, 0.9[m], is in meters and the variables
``x`` and ``y`` have the same units inside the row. This row is scaled
back to ``dm`` afterwards. As a result of all this scaling, the
computations go from the domain of integer arithmetic into the domain of
floating point arithmetic. For constraint programming, we need to avoid
the domain of floating point arithmetic.

.. rubric:: Adapted base unit

We will continue the above example, by adapting the base unit such that
all amounts are integral multiples of that base unit; we select ``dm``
as a base unit. This will lead to the following row communicated to the
solver:

.. code-block:: aimms

	y_away_from_x .. [ 1 | 1 | before ]

	    y =
	    abs((x-9))  ****

	    name       lower      level      upper
	    x              0          0 2147483647
	    y              0          0 2147483647

Observe that scaling is not needed anymore. Using the scaling based on
``dm`` instead of ``m`` will keep all computations during the solution
process in the domain of integer arithmetic.

.. rubric:: Quantity based scaling

In the example of the previous paragraph, the base unit was adapted to
the needs of constraint programming; namely to stay within the domain of
integer arithmetic. For multi-purpose applications, freedom of choosing
the base units of quantities according to the needs of a constraint
programming problem is not always available. In order to stay within the
domain of integer arithmetic, we can associate a convention with the
mathematical program and filling in the ``per quantity`` attribute, see
also :ref:`sec:units.convention`. By filling in the ``per quantity``
attribute, AIMMS will generate the mathematical program where all
coefficients are scaled with respect to the units specified in the
``per quantity`` attribute. Let us continue the example of the previous
paragraph using ``m`` as the base unit and adding a convention to the
mathematical program.

.. code-block:: aimms

	Quantity SI_Length {
	    BaseUnit     :  m;
	    Conversions  : {
	        dm -> m : # -> # / 10,
	        cm -> m : # -> # / 100
	    }
	    Comment      :  "Expresses the value of a distance.";
	}
	Parameter LengthGranul {
	    InitialData  :  10;
	}
	Convention solveConv {
	    PerQuantity  :  SI_Length : LengthGranul * cm;
	}
	MathematicalProgram myCP {
	    Direction    :  minimize;
	    Constraints  :  AllConstraints;
	    Variables    :  AllVariables;
	    Type         :  Automatic;
	    Convention   :  solveConv;
	}

Again, AIMMS will generate the constraint such that only integer
arithmetic is needed. The constraint listing of that constraint is
similar to the constraint listing presented in the paragraph *adapted
base unit* above and not repeated. Note also that with conventions, we
can now use parameters to further control the scaling; if we want to
change the model such that we can use multiples of ``20[cm]`` instead of
multiples of ``10[cm]``, we only need to change the value of
``LengthGranul``.

.. rubric:: Calendar used for timeline

Scheduling applications in which the schedule domain is based on a
calendar, the length of a timeslot is equal to the unit of the calendar,
see :ref:`sec:time.calendar`. The time quantity is overridden, as if an
entry in the ``per quantity`` attribute of the associated convention is
given, selecting the calendar unit. Even if no convention was associated
with the mathematical program. In short, for scheduling applications,
AIMMS will scale time based data according to the length of a timeslot.

Solving a Constraint Program
----------------------------

.. rubric:: Mathematical Programming types

AIMMS distinguishes two types of mathematical programs that are
associated with constraint programming models: ``COP`` for constraint
optimization problems, and ``CSP`` for constraint satisfaction problems.
Both ``COP`` and ``CSP`` are exact in that ``COP`` provides a proven
optimal solution while ``CSP`` provides a solution, or proves that none
exist, if time permits.

.. rubric:: Limiting solution time

Constraint programming problems are combinatorial problems and therefore
may take a long time to solve, especially when trying to prove
optimality. In order to avoid unexpectedly long solution times, you can
limit the amount of time allocated to the solver for solving your
problem as follows:

.. code-block:: aimms

	solve myCOP where time_limit := pMaxSolutionTime ; 
	! pMaxSolutionTime is in seconds.

Alternatively, when you are satisfied with the current objective, as
presented in the progress window, and not want to wait on further
improvements, you can interrupt the solution process by using the
key-stroke *ctrl-shift-s*.

Search Heuristics
-----------------

.. rubric:: Search heuristics

During the solving process, constraint programming employs search
heuristics that define the shape of the search tree, and the order in
which the search tree nodes are visited. The shape of the search tree is
typically defined by the order of the variables to branch on, and the
corresponding value assignment. AIMMS allows the user to specify which
variable and value selection heuristics are to be used. For example, to
decide the next variable on which to branch, a commonly used search
heuristic is to choose a non-fixed variable with the minimum domain
size, and assign its minimum domain value.

.. rubric:: Search phases

The first method offered by AIMMS to influence the search process is
through using the ``Priority`` attributes of the variables. AIMMS will
group together all variables that have the same priority value, and each
block of variables will define a *search phase*. That is, the solver
will first assign the variables in the block with the highest priority,
then choose the next block, and so on. As discussed in
:ref:`sec:var.var.solver-attr`, the highest priority is the one with the
highest positive value. Defining search phases can be very useful. For
example, when scheduling activities to various alternative resources, it
is natural to first assign an activity to its resource before assigning
its begin.

.. rubric:: Variable and value selection

The variable and value selection heuristics offered by AIMMS are
presented in :numref:`table:constraint.programming.search.heuristics`.
They can be accessed through the 'solver options' configuration window.
As an example, we can define a 'constructive' scheduling heuristic that
builds up the schedule from the begin of the schedule domain by using
``MinValue`` as the variable selection, and :any:`Min` as the value
selection. Indeed, this heuristic will attempt to greedily schedule the
activities as early as possible. Note that both these variable and value
heuristics apply to the entire search process. If no variable priorities
are specified, the variable selection heuristic will consider all
variables at a time. Otherwise, the variable selection heuristic is
applied to each block individually.

.. _table:constraint.programming.search.heuristics:

.. table:: Search heuristics

   =================== ===================================
   Heuristic           Interpretation
   =================== ===================================
   Variable selection: choose the non-fixed variable with:
   ``Automatic``       use the solver's default heuristic
   ``MinSize``         the smallest domain size
   ``MaxSize``         the largest domain size
   ``MinValue``        the smallest domain value
   ``MaxValue``        the largest domain value
   Value selection:    assign:
   ``Automatic``       use the solver's default heuristic
   :any:`Min`          the smallest domain value
   :any:`Max`          the largest domain value
   ``Random``          a uniform-random domain value
   =================== ===================================