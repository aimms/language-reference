.. _sec:matrix.examples:

Examples of Use
===============

.. rubric:: This section

In this section there are five examples to illustrate the use of the GMP
library. Each example consists of two paragraphs. The first paragraph
explains the basic problem and an algorithmic approach, while the second
paragraph provides the corresponding implementation in AIMMS using the
GMP procedures. Note that these algorithms could also have been
implemented using AIMMS' regular ``SOLVE`` statement, but at the cost of
one or more structure recognition steps during every iteration.

.. _sec:gmp.examples.indexed:

Indexed Mathematical Program Instances
--------------------------------------

.. rubric:: Indexed mathematical program instances

AIMMS does not support indexed mathematical program declarations, which
would result in a different mathematical program for every index value
when generated. Using the GMP library, however, it is straightforward to
generate indexed mathematical program *instances*

.. rubric:: Declarations in AIMMS

Consider the following declarations

.. code-block:: aimms

	Set Cities {
	    Index        : c, j;
	}
	Set  SelectedCities {
	    SubsetOf     : Cities;
	    Index        : i;
	}

together with a mathematical program declaration ``TransportModel``
defining a standard transportation problem determining transports from
cities ``i`` to ``j``. When ``SelectedCities`` equals ``Cities`` we
would solve the mathematical program for all possible combinations of
cities.

.. rubric:: Procedure in AIMMS

Further assume that we have an element parameter
``IndexedTransportModel(c)`` into the set
:any:`AllGeneratedMathematicalPrograms`. The following procedure
illustrates how indexed mathematical program instances for every city
``c`` which restricts the transports from ``c`` to all cities ``j``.

.. code-block:: aimms

	for ( c ) do
	    SelectedCities := {c};

	    IndexedTransportModel(c) := GMP::Instance::Generate( TransportModel,
	                         "TransportModel-" + FormatString("%e", c) );
	endfor;

Sensitivity Analysis
--------------------

.. rubric:: Parametric changes

Sensitivity analysis considers how the optimal solution, and the
corresponding objective function value, change as a result of changes in
input data. Using the GMP library, it is straightforward to write a
procedure to determine these sensitivities for a discrete set of input
values.

.. rubric:: Procedure in AIMMS

The following procedure illustrates how parametric changes can be
implemented using matrix manipulation functions. The resulting objective
function values are stored in a separate identifier.

.. code-block:: aimms

	myGMP := GMP::Instance::Generate( MathProgramOfInterest );

	for ( n ) do
	   GMP::Coefficient::Set( myGMP,
	                          ResourceConstraint(SelectedResource),
	                          ActivityVariable(SelectedActivity),
	                          OriginalCoefficient + Delta(n) );

	   GMP::Instance::Solve( myGMP );

	   ObjectiveValue(n) := GMP::Solution::GetObjective(myGMP, 1);
	endfor;

Finding a Feasible Solution for a Binary Program
------------------------------------------------

.. rubric:: Fixing one variable at a time

There have been instances in which the following simple but greedy
heuristic was used successfully to solve a binary program. The algorithm
considers linear programming solutions in sequence. During each
iteration, the algorithm

-  selects the single variable that, of all the variables, is nearest
   but not equal to one of its bounds, and

-  fixes the value of this variable to that of the nearest bound.

As soon as such variables can no longer be found (and the last linear
programming solution is optimal), a feasible integer solution to the
binary program has been found.

.. rubric:: Procedure in AIMMS

The following procedure illustrates how fixing one variable at a time
can be implemented using matrix manipulation functions. The procedure
terminates as soon as there is no solution, or all variables have been
fixed.

.. code-block:: aimms

	relaxedGMP := GMP::Instance::Generate( RelaxedBinaryProgram );
	GMP::Instance::Solve( relaxedGMP );

	repeat
	    LargestLessThanOne      := ArgMax( j | x(j) <= 1 - Tolerance, x(j) );
	    SmallestGreaterThanZero := ArgMin( j | x(j) >= Tolerance,     x(j) );

	    break when ( RelaxedBinaryProgram.ProgramStatus = 'Infeasible' or
	                 not ( LargestLessThanOne or SmallestGreaterThanZero ) );

	    if ( x(SmallestGreaterThanZero) < 1 - x(LargestLessThanOne) )
	    then GMP::Column::Freeze( relaxedGMP, x(SmallestGreaterThanZero), 0 );
	    else GMP::Column::Freeze( relaxedGMP, x(LargestLessThanOne), 1 );
	    endif;

	    GMP::Instance::Solve( relaxedGMP );
	endrepeat;

Column Generation
-----------------

.. rubric:: Adding columns

Chapter 20 of the AIMMS book on Optimization Modeling describes a
cutting stock problem. This problem is modeled as a linear program with
an initial selection of cutting patterns. An auxiliary integer
programming model is introduced to generate a new "best" pattern based
on the current solution of the linear program and the corresponding
shadow prices. Such a pattern is then added to the existing patterns in
the linear program, and the next optimal solution is found. This process
continues until no further improvement in the value of the objective
function can be achieved.

.. rubric:: Procedure in AIMMS

The following procedure illustrates how adding columns can be
implemented using matrix manipulation functions. During each iteration
of the overall process, two different mathematical programs are modified
in turn.

.. code-block:: aimms

	cuttingStockGMP := GMP::Instance::Generate( CuttingStock );
	GMP::Instance::Solve( cuttingStockGMP );

	findPatternGMP := GMP::Instance::Generate( FindPattern );
	GMP::Instance::Solve( findPatternGMP );

	MaxPattern := 0;
	while ( PatternContribution > 1 ) do
	    MaxPattern += 1;
	    AllPatterns += MaxPattern;
	    LastPattern := last(AllPatterns);

	    GMP::Column::Add( GMP: cuttingStockGMP, column: RollsUsed(LastPattern) );

	    for ( width ) do
	        GMP::Coefficient::Set( GMP   : cuttingStockGMP,
	                               row   : MeetCutDemand(width),
	                               column: RollsUsed(LastPattern),
	                               value : CutsInPattern(width)  );
	    endfor;
	    GMP::Instance::Solve( cuttingStockGMP );

	    for ( width ) do
	        GMP::Coefficient::Set( GMP   : findPatternGMP,
	                               row   : PatternContribution,
	                               column: CutsInPattern(width),
	                               value : MeetCutDemand(width).ShadowPrice );
	    endfor;
	    GMP::Instance::Solve( findPatternGMP );
	endwhile;

Here ``MaxPattern`` is a parameter of type integer, ``AllPatterns`` a
subset of :any:`Integers`, and ``LastPattern`` an element parameter with
range ``AllPatterns``.

.. _sec:matrix.examples.slp:

Sequential Linear Programming
-----------------------------

.. rubric:: Sequential linear programming

Linear constraints and a nonlinear objective function together form a
special class of nonlinear programs. It is possible to solve a problem
of this class by solving a sequence of linear programs. The main
requirement is that the nonlinear objective function has first-order
derivatives. The objective function can then be linearized around the
solution of a previous linear program. By restricting the linearized
function to an appropriate finite box, a new solution point is found.
The sequence of linear programs terminates when the appropriate box has
become sufficiently small. Upon termination, the optimal solution, as
last found, is considered to be a local optimum of the underlying
nonlinear program.

.. rubric:: Procedure in AIMMS

The following procedure illustrates how sequential linear programming
can be implemented using matrix manipulation functions. The procedure
assumes the existence of finite upper and lower bounds on the variables,
and the presence of a function ``ComputeGradient`` to compute the
required first partial derivatives with respect to the variables in the
objective function. To implement the function ``ComputeGradient`` one
can, for instance, use the built-in GMP function
:any:`GMP::Solution::GetFirstOrderDerivative` (see also
:ref:`sec:gmp.solution`).

.. code-block:: aimms

	linearizedGMP := GMP::Instance::Generate(LinearizedProgram);
	GMP::Instance::Solve(linearizedGMP);

	BoxWidth(j)  := 0.1 * (x.upper(j) - x.lower(j));
	x(j)         := 0.5 * (x.upper(j) + x.lower(j));

	while ( max( j, BoxWidth(j) ) > Tolerance ) do
	   ObjCoeff(j) := ComputeGradient(x)(j);

	   for (j) do
	      GMP::Column::SetLowerBound ( linearizedGMP, x(j),
	                                   max(x.lower(j), x(j) - 0.5*BoxWidth(j)) );
	      GMP::Column::SetUpperBound ( linearizedGMP, x(j),
	                                   min(x.upper(j), x(j) + 0.5*BoxWidth(j)) );
	      GMP::Coefficient::Set( linearizedGMP, ObjectiveRow,
	                             x(j), ObjCoeff(j)            );
	   endfor;
	   GMP::Instance::Solve(linearizedGMP);

	   BoxWidth(j) *= ShrinkFactor;
	endwhile;