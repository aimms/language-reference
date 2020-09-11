.. _sec:intro.model:

Formulation of the Mathematical Program
=======================================

.. rubric:: Constraint-oriented modeling

In programming languages like ``C`` it is customary to solve a
particular problem through the explicit specification of an algorithm to
compute the solution. In AIMMS, however, it is sufficient to specify
only the ``Constraints`` which have to be satisfied by the solution.
Based on these constraints AIMMS generates the input to a specialized
numerical solver, which in turn determines the (optimal) solution
satisfying the constraints.

.. rubric:: Variables as unknowns

In constraint-oriented modeling the unknown quantities to be determined
are referred to as ``variables``. Like parameters, these variables can
either be scalar or indexed, and their values can be restricted in
various ways. In the depot location problem it is necessary to solve for
two groups of variables.

-  There is one variable for each depot ``d`` to indicate whether that
   depot is to be selected from the available depots.

-  There is another variable for each permitted route ``(d,c)``
   representing the level of transport on it.

.. rubric:: Example

In AIMMS, the variables described above can be declared as follows.

.. code-block:: aimms

	Variable DepotSelected {
	    IndexDomain   :  d;
	    Range         :  binary;
	}
	Variable Transport {
	    IndexDomain   :  (d,c) in PermittedRoutes;
	    Range         :  nonnegative;
	}

.. rubric:: The ``Range`` attribute

For unknown variables it is customary to specify their range of values.
Various predefined ranges are available, but you can also specify your
own choice of lower and upper bounds for each variable. In this example
only predefined ranges have been used. The predefined range ``binary``
indicates that the variable can only assume the values 0 and 1, while
the range ``nonnegative`` indicates that the value of the corresponding
variable must lie in the continuous interval :math:`[0,\infty)`.

.. rubric:: Constraints description

As indicated in the problem description in :ref:`sec:intro.decl` a
solution to the depot location problem must satisfy two constraints:

-  the demand of each customer must be met, and

-  the capacity of each selected depot must not be exceeded.

.. rubric:: Example

In AIMMS, these two constraints can be formulated as follows.

.. code-block:: aimms

	Constraint CustomerDemandRestriction {
	    IndexDomain  :  c;
	    Definition   :  Sum[ d, Transport(d,c) ] >= CustomerDemand(c);
	}
	Constraint DepotCapacityRestriction {
	    IndexDomain  :  d;
	    Definition   :  Sum[ c, Transport(d,c) ] <= DepotCapacity(d)*DepotSelected(d);
	}

.. rubric:: Satisfying demand

The constraint ``CustomerDemandRestriction(c)`` specifies that for every
customer ``c`` the sum of transports from every possible depot ``d`` to
this particular customer must exceed his demand. Note that the ``Sum``
operator behaves as the standard summation operator :math:`\sum` found
in mathematical literature. In AIMMS the domain of the summation must be
specified as the first argument of the ``Sum`` operator, while the
second argument is the expression to be accumulated.

.. rubric:: Proper domain

At first glance, it may seem that the (indexed) summation of the
quantities ``Transport(d,c)`` takes place over all tuples
(``d``,\ ``c``). This is not the case. The underlying reason is that the
variable ``Transport`` has been declared with the index domain
``(d,c) in PermittedRoutes``. As a result, the transport from a depot
``d`` to a customer ``c`` not in the set ``PermittedRoutes`` is not
considered (i.e. not generated) by AIMMS. This implies that transport to
``c`` only accumulates along permitted routes.

.. rubric:: Satisfying capacity

The interpretation of the constraint ``DepotCapacityRestriction(d)`` is
twofold.

-  Whenever ``DepotSelected(d)`` assumes the value 1 (the depot is
   selected), the sum of transports leaving depot ``d`` along permitted
   routes may not exceed the capacity of depot ``d``.

-  Whenever ``DepotSelected(d)`` assumes the value 0 (the depot is not
   selected), the sum of transports leaving depot ``d`` must be less
   than or equal to 0. Because the range of all transports has been
   declared nonnegative, this constraint causes each individual
   transport from a nonselected depot to be 0 as expected.

.. rubric:: The objective function

The objective in the depot location problem is to minimize the total
cost resulting from the rental charges of the selected depots together
with the cost of all transports taking place. In AIMMS, this objective
function can be declared as follows.

.. code-block:: aimms

	Variable TotalCost {
	    Definition : {
	        Sum[ d, DepotRentalCost(d)*DepotSelected(d) ] +
	        Sum[ (d,c), UnitTransportCost(d,c)*Transport(d,c) ];
	    }
	}

.. rubric:: Defined variables

The variable ``TotalCost`` is an example of a defined variable. Such a
variable will not only give rise to the introduction of an unknown, but
will also cause AIMMS to introduce an additional constraint in which
this unknown is set equal to its definition. Like in the summation in
the constraint ``DepotCapacityRestriction``, AIMMS will only consider
the tuples ``(d,c) in PermittedRoutes`` in the definition of the
variable ``TotalCost``, without you having to (re-)specify this
restriction again.

.. rubric:: The mathematical program

Using the above, it is now possible to specify a mathematical program to
find an optimal solution of the depot location problem. In AIMMS, this
can be declared as follows.

.. code-block:: aimms

	MathematicalProgram DepotLocationDetermination {
	    Objective    :  TotalCost;
	    Direction    :  minimizing;
	    Constraints  :  AllConstraints;
	    Variables    :  AllVariables;
	    Type         :  mip;
	}

.. rubric:: Explanation

The declaration of ``DepotLocationDetermination`` specifies a
mathematical program in which the defined variable ``TotalCost`` serves
as the objective function to be ``minimized``. All previously declared
constraints and variables are to be part of this mathematical program.
In more advanced applications where there are multiple mathematical
programs it may be necessary to reference subsets of constraints and
variables. The ``Type`` attribute specifies that the mathematical
program is a mixed integer program (``mip``). This reflects the fact
that the variable ``DepotSelected(d)`` is a binary variable, and must
attain either the value 0 or 1.

.. rubric:: Solving the mathematical program

After providing all input data (see :ref:`sec:intro.expressions`) the
mathematical program can be solved using the following simple execution
statement.

.. code-block:: aimms

	Solve DepotLocationDetermination ;

A ``SOLVE`` statement can only be called inside a procedure in your
model. An example of such a procedure is provided in
:ref:`sec:intro.proc`.