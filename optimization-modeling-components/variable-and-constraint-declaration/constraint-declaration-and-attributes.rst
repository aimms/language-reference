.. _sec:var.constr:

``Constraint`` Declaration and Attributes
=========================================

.. rubric:: Definitions

Constraints form the major mechanism for specifying a mathematical
program in AIMMS. They are used to restrict the values of variables with
interlocking relationships. *Constraints* are numerical relations
containing expressions in terms of variables, parameters and constants.

.. _constraint:

.. rubric:: Constraint attributes

The possible attributes of constraints are given in
:numref:`table:var.attr-constraint`.

.. _table:var.attr-constraint:

.. table:: 

	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| Attribute               | Value-type                                              | See also page                                                                                                                   |
	+=========================+=========================================================+=================================================================================================================================+
	| ``IndexDomain``         | *index-domain*                                          | :ref:`here <attr:par.index-domain>`                                                                                             |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Unit``                | *unit-valued expression*                                | :ref:`here <attr:par.unit>`, :ref:`chap:units`                                                                                  |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Text``                | *string*                                                | :ref:`here <attr:prelim.text>`                                                                                                  |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Comment``             | *comment string*                                        | :ref:`here <attr:prelim.comment>`                                                                                               |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Definition``          | *expression*                                            | :ref:`The Parameter Definition attribute <attr:par.definition>`, :ref:`The Variable Definition attribute <attr:var.definition>` |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Property``            | ``NoSave``, ``Sos1``, ``Sos2``, ``IndicatorConstraint`` | :ref:`The Set Property attribute <attr:set.property>`, :ref:`The Parameter Property attribute <attr:par.property>`              |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	|                         | ``Level``, ``Bound``, ``Basic``, ``ShadowPrice``,       | :ref:`here <attr:var.property>`                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	|                         | ``RightHandSideRange``, ``ShadowPriceRange``,           |                                                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	|                         | ``IsDiversificationFilter``, ``IsRangeFilter``,         |                                                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	|                         | ``IncludeInLazyConstraintPool``,                        |                                                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	|                         | ``IncludeInCutPool``, ``Chance``                        |                                                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``SosWeight``           | *sos-weights*                                           |                                                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``ActivatingCondition`` | *expression*                                            |                                                                                                                                 |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Probability``         | *expression*                                            | :ref:`sec:var.constr.chance`, :ref:`The Chance Constraint Probability attribute <attr:robust.chance.probability>`               |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	| ``Aproximation``        | *element-expression*                                    | :ref:`sec:var.constr.chance`, :ref:`The Chance Constraint Approximation attribute <attr:robust.chance.approximation>`           |
	+-------------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Domain restriction for constraints
   :name: attr:var.constr.index-domain

.. _constraint.index_domain:

Restricting the domain of constraints through the ``IndexDomain``
attribute influences the matrix generation process. Constraints are
generated only for those tuples in the index domain that satisfy the
domain restriction.

.. rubric:: The ``Definition`` attribute
   :name: attr:var.constr.definition

.. _constraint.definition:

With the ``Definition`` attribute of a constraint you specify a
numerical relationship between variables in your model. Without a
definition a constraint is indeterminate. Constraint definitions consist
of two or three expressions separated by one of the relational operators
``=``, ``>=`` or ``<=``.

.. rubric:: Example

The following constraints express the simultaneous requirements that the
sum of all transports from a city ``i`` must not exceed ``Supply(i)``,
and that for each city ``j`` the ``Demand(j)`` must be met.

.. code-block:: aimms

	Constraint SupplyConstraint {
	    IndexDomain  : i;
	    Unit         : kton;
	    Definition   : sum( j, Transport(i,j) ) <= Supply(i);
	}
	Constraint DemandConstraint {
	    IndexDomain  : j;
	    Unit         : kton;
	    Definition   : sum( i, Transport(i,j) ) >= Demand(j);
	}

.. rubric:: Allowed relationships

If :math:`a` and :math:`b` are expressions consisting of only parameters
and :math:`f(x,\dots)` and :math:`g(x,\dots)` are expressions containing
parameters and variables, the following two kinds of relationships are
allowed.

.. math::

   a \leq f(x,\dots) \leq b \qquad \mbox{or} \qquad
           f(x,\dots) \gtrless g(x,\dots)

where :math:`\gtrless` denotes any of the relational operators ``=``,
``>=`` or ``<=``. Either :math:`a` or :math:`b` can be omitted if
there is no lower or upper bound on the expression :math:`f(x,\dots)`,
respectively. When both :math:`a` and :math:`b` are present, the
constraint is referred to as a *ranged* constraint. The expressions may
have linear and nonlinear terms, and may utilize the full range of
intrinsic functions of AIMMS except for the random number functions.

.. rubric:: Conditional expressions in constraints

You must take extreme care to ensure continuity when the constraints in
your model contain logical conditions that include references to
variables. Such constraints are viewed by AIMMS as nonlinear
constraints, and thus can only be passed to a solver that can handle
nonlinearities. It is possible that the outcome of a logical condition,
and thus the form of the constraint, changes each time the underlying
solver asks AIMMS for function values and gradients. For example, if
``x(i)`` is a decision variable, and a constraint contains the
expression

.. code-block:: aimms

	sum[ i, if ( x(i) > 0 ) then  x(i)^2 endif ]

it may or may not contain the term ``x(i)``\ ``^2``, depending on the
current value of ``x(i)``. In this example, both the expression and its
gradient are continuous functions at ``x(i) = 0``.

.. _sec:var.constr.property:

Constraint Properties
---------------------

.. rubric:: The ``Property`` attribute
   :name: attr:var.constr.property

.. _constraint.property:

With the ``Property`` attribute you can specify further characteristics
of the constraint at hand. The possible properties of a constraint are
``NoSave``, ``Sos1``, ``Sos2``, ``Level``, ``Bound``, ``Basic``,
``ShadowPrice``, ``RightHandSideRange``, and ``ShadowPriceRange``.

.. rubric:: The ``NoSave`` property

When you specify the ``NoSave`` property you indicate that you do not
want AIMMS to store data associated with the constraint in a case,
regardless of the specified case identifier selection.

.. _sec:var.constr.sos:

SOS Properties
--------------

.. rubric:: The SOS properties

The constraint types ``Sos1`` and ``Sos2`` are used in mixed integer
programming, and mutually exclusive. In the context of mathematical
programming SOS is an acronym for Special Ordered Sets. A SOS set is
associated with every (individual) constraint of type ``Sos1`` or
``Sos2``.

.. rubric:: Additional SOS attribute

When you specify that a constraint is of type ``Sos1`` or ``Sos2``, an
additional SOS-specific attributes becomes available, namely the
``SosWeight`` attributes. With this attributes, you can provide further
information to the solver about the contents and ordering of the SOS set
to be associated with the constraint.

.. rubric:: ``Sos1`` constraints

A type ``Sos1`` constraint specifies to the solver that at most one of
the variables within the SOS set associated with the constraint is
allowed to be nonzero, while all other variables in the SOS set must be
zero. Inside a ``Sos1`` constraint all variables in the SOS set must
have a lower bound of zero and an upper bound greater than zero.

.. rubric:: ``Sos2`` constraints

A type ``Sos2`` constraint specifies to the solver that at most two
consecutive variables within the SOS set associated with the constraint
are allowed to be nonzero, while all other variables within the SOS set
must be zero. All individual variables within the SOS set must have a
lower bound of zero and an upper bound greater than zero. The order of
the individual variables within the SOS set is determined by their
weights (as specified in the ``SosWeight`` attribute), where the
ordering is from low to high weight.

.. _constraint.sos_weight:

.. rubric:: The ``SosWeight`` attribute

With the ``SosWeight`` attribute you must specify the contents of the
SOS set to be associated with a ``Sos1`` or ``Sos2`` constraint, as well
the ordering of its elements. Section 7.5 of the AIMMS `Modeling Guide <https://documentation.aimms.com/_downloads/AIMMS_modeling.pdf>`__ 
describes how these weights are used during the
branch-and- bound process. The syntax of the ``SosWeight`` attribute is
as follows.

.. _sos-weights:

.. rubric:: Syntax

*sos-weights:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 329.84535 67.199997"
	   height="67.199997"
	   width="329.84534"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,186.93333)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,25,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/optimization-modeling-components/variable-and-constraint-declaration/constraint-declaration-and-attributes.html#variable-reference">variable-reference</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1266.96,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1366.96,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,143.096,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1566.96,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1666.96,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,171.696,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#reference">reference</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2273.84,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,1000 20,50 H 80" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1136.92,1300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,120.092,126)"><tspan
	             id="tspan50"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1336.92,1300 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2373.84,1000 20,50 h -40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2473.84,1000 -50,20 v -40" /><path
	         id="path60"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 100 m 0,0 v 0 h 100 v 100 H 1266.93 V 1000 900 H 200 v 100 m 1066.96,0 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.773 -100,100 v 0 m 200,0 h 100 v 100 h 606.87 V 1000 900 h -606.87 v 100 m 606.88,0 h 100 M 100,1000 v 200 c 0,55.23 44.773,100 100,100 h 836.92 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 100 836.92 c 55.23,0 100,-44.77 100,-100 v -200 h 100" /></g></g></svg></div>

.. _variable-reference:

Within the ``SosWeight`` attribute you can (but need not) specify a
weight for every variable occurring in the constraint. Each weight must
be an expression using all the indices in the index domain of the
variable plus some or all of the indices in the index domain of the
constraint. All weights specified for a particular constraint must be
unique, i.e. you cannot specify the same weight for two (individual)
variables. The SOS set to be associated with the constraint will be
constructed from all variables-within the domain of both the constraint
and variable-for which a nonzero weight has been specified in the
``SosWeight`` attribute, i.e. if the value of the specified weight is
``0.0`` for a particular tuple, the corresponding individual variable
will not be included in the SOS set. The ordering of variables within
the SOS set is from low to high weight.

.. rubric:: Consistency

If you do not specify SOS weights, AIMMS will make sure that ordering of
variables in each SOS set is consistent over all SOS sets. If you
specify SOS weights yourself, you have to make sure that the variable
orderings of all SOS sets of type ``Sos2`` are consistent, or your model
might become infeasible if feasibility requires that two adjacent
variables in one SOS set become nonzero, which are ordered
inconsistently in another SOS set. Therefore, AIMMS requires that you
specify the ``SosWeight`` attributes for *all* SOS constraints in your
model, whenever you specify it for *one* SOS constraint.

.. rubric:: Example

The following is specification of ``Sos2`` constraint to determine the
variable ``y`` piece-wise linearly from a variable ``x(i)``.

.. code-block:: aimms

	Constraint DetermineY {
	    Property     : Sos2;
	    Definition   : y = sum[ i, x(i)*c(i) ];
	    SosWeight    : x(i) : XWeight(i);
	}

.. _sec:var.constr.solutionpool:

Solution Pool Filtering
-----------------------

.. rubric:: Solution pool

During the solution process of a MIP problem, the solvers CPLEX and
GUROBI are capable of storing multiple feasible integer solutions in a
solution pool, for instance, to capture solutions with attractive
properties that are hard to express in a linear fashion.

.. rubric:: Filtering

While populating the solution pool, CPLEX offers advanced filtering
capabilities, allowing you to control which solutions end up in the
solution pool. CPLEX provides two predefined ways to filter solutions:

-  if you want to filter solutions based on their difference as compared
   to a reference solution, use a *diversity* filter, or

-  if you want to filter solutions based on their validity in an
   additional linear constraint, use a *range* filter.

To enable filters the CPLEX option ``Do_Populate`` need to be on.

.. rubric:: Diversity filters

A diversity filter allows you to generate solutions that are similar to
(or different from) a set of reference values that you specify for a set
of binary variables. In particular, you can use a diversity filter to
generate more solutions that are similar to an existing solution or to
an existing partial solution. Several diversity filters can be used
simultaneously, for example, to generate solutions that share the
characteristics of several different solutions.

.. rubric:: The ``IsDiversificationFilter`` property

In AIMMS, a constraint is used as a diversity filter if the constraint
property ``IsDiversificationFilter`` has been set. In a diversification
filter, the :any:`Abs` function is used to measure the distance from a
given binary variable, and all variables should only occur as the
argument of an :any:`Abs` function.

.. rubric:: Example

This following diversification filter forces the solutions to have a
distance of at least 1 from variable ``x``.

.. code-block:: aimms

	Constraint filter1 {
	    Property     :  IsDiversificationFilter;
	    Definition   :  Abs(x - 1) >= 1;
	}

.. rubric:: Range filters

A range filter allows you to generate solutions that obey a new
constraint, specified as a linear expression within a range. Range
filters can be used to express diversity constraints that are more
complex than the standard form implemented by diversity filters. In
particular, range filters also apply to general integer variables,
semi-integer variables, continuous variables, and semi-continuous
variables, not just to binary variables.

.. rubric:: The ``IsRangeFilter`` property

In AIMMS, a constraint is used as a range filter if the constraint
property ``IsRangeFilter`` has been set for the constraint.

.. rubric:: Example

The following range filter specifies that any solution to be added to
the solution pool should satisfy the following constraint.

.. code-block:: aimms

	Contraint filter2 {
	   Property     :  IsRangeFilter;
	   Definition   :  x + y + z >= 2;
	}

.. _sec:var.constr.indicator:

Indicator Constraints, Lazy Constraints and Cut Pools
-----------------------------------------------------

.. rubric:: Indicator constraints

An indicator constraint is a new way of controlling whether or not a
constraint takes effect, based on the value of a binary variable.
Traditionally, such relationships are expressed by so-called
big-:math:`M` formulations. Big-:math:`M` formulations, however, can
introduce unwanted side-effects and numerical instabilities into a
mathematical program. Using indicator constraints, such relationships
between a constraint and a variable can be directly expressed in the
constraint declaration. Indicator constraints are supported by the
solvers CPLEX, GUROBI and ODH-CPLEX.

.. rubric:: The ``IndicatorConstraint`` property

You can specify that a constraint is an indicator constraint by settings
it ``IndicatorConstraint`` property. For indicator constraints, a new
attribute called ``ActivatingCondition`` will become available in the
constraint declaration.

.. _constraint.activating_condition:

.. rubric:: The ``ActivatingCondition`` attribute

Through the ``ActivatingCondition`` attribute you can specify under
which condition the constraint definition should become active during
the solution process. Its value should be an expression of the form

   binary-variable ``=`` expression

where the *expression* must take one of the values 0 or 1. Note:
stochastic variables and parameters are not allowed inside an activation
condition.

.. rubric:: Example

Consider the following big-:math:`M` constraint

.. code-block:: aimms

	Constraint BigMConstraint {
	    Definition : x1 + x2 <= M*y;
	}

where ``y`` is a binary variable. Using the ``IndicatorConstraint``
property, the constraint can be reformulated as an indicator constraint
as follows

.. code-block:: aimms

	Constraint NonBigMConstraint {
	    Property             : IndicatorConstraint;
	    ActivatingCondition  : y = 0;
	    Definition           : x1 + x2 = 0;
	}

The constraint only becomes effective, whenever the binary variable
``y`` takes the value 0. To solve the model with the indicator
constraint, you need the CPLEX, GUROBI or ODH-CPLEX solver.

.. rubric:: Lazy constraints

Sometimes, for a MIP formulation, a user can already identify a group of
constraints that are unlikely to be violated (lazy constraints). Simply
including these constraints in the original formulation could make the
LP subproblem of a MIP optimization very large or too expensive to
solve. CPLEX, GUROBI and ODH-CPLEX can handle problems with lazy
constraints more efficiently, and therefore AIMMS allows you to identify
lazy constraints in your model.

.. rubric:: The ``IncludeInLazyConstraintPool`` property

You can specify that a constraint should be added to the pool of lazy
constraints considered by CPLEX, GUROBI or ODH-CPLEX by setting the
property ``IncludeInLazyConstraintPool``. You need the CPLEX, GUROBI or
ODH-CPLEX solver to use this constraint property. When solving your MIP
model, CPLEX, GUROBI and ODH-CPLEX will only consider these constraints
when they are violated.

.. rubric:: User cut pools

As discussed in :ref:`sec:mp.suffix`, AIMMS allows you to add cuts to
your mathematical program on the fly during the solution process by
using the ``CallbackAddCut`` callback. However, when the set of cuts you
want to generate is fixed and known upfront, using the
``CallbackAddCut`` may add significant overhead to the solution process
of your model while you don't need its flexibility. For those
situations, CPLEX allows you to specify a fixed pool of user cuts during
the generation of your mathematical program.

.. rubric:: The ``IncludeInCutPool`` property

By setting the constraint property ``IncludeInCutPool`` you can indicate
that this constraint should be included in the pool of user cuts
associated with your mathematical program. You need the CPLEX solver to
use this constraint property. When solving your MIP model, CPLEX will
consider the user cuts added in this manner when appropriate.

.. _sec:constr.values:

Constraint Levels, Bounds and Marginals
---------------------------------------

.. rubric:: Constraint levels and bounds

A constraint in AIMMS can conceptually be divided such that one side
consists of all variable terms, whereas the other side consists of all
remaining constant terms. The *level* value of a constraint is the
accumulated value of the variable terms, while the constant terms make
up the *bound* of the constraint.

.. _shadowprice:

.. rubric:: The ``Level``, ``Bound``, ``Basic`` and ``ShadowPrice`` properties

With the ``Level``, ``Bound``, ``Basic`` and ``ShadowPrice`` properties
you indicate whether you want to store (and have access to) particular
parametric data associated with the constraint.

-  When you specify the ``Level`` property AIMMS will retain the level
   values of the constraint as provided by the solver. You can access
   the level values of a constraint by using the constraint name as if
   it were a parameter.

-  By specifying the ``Bound`` property, AIMMS will store the upper and
   lower bound of the constraint as employed by the solver. You get
   access to the bounds by using the :ref:`.Lower` and :ref:`.Upper` suffices
   with the constraint identifier.

-  If the ``Basic`` property has been specified, AIMMS stores basic
   information is available through the :ref:`.Basic` suffix as an element
   in of the predefined AIMMS set :any:`AllBasicValues`. A constraint is
   said to be basic (nonbasic or superbasic) if its associated slack
   variable is basic (nonbasic or superbasic).

-  With the ``ShadowPrice`` property you indicate that you want to store
   the shadow prices as computed by the solver. You can access these
   shadow prices by means of the :ref:`.ShadowPrice` attribute.

.. rubric:: Interpretation of shadow prices
   :name: par:constr.interpr.shadowpr

The shadow price (or dual value) of a constraint is the marginal change
in the objective value with respect to a change in the right-hand side
(i.e. the constant part) of the constraint. This value is determined by
the solver after a ``SOLVE`` statement has been executed. The precise
mathematical interpretation of the shadow price is discussed in detail
in many text books on mathematical programming. Note: if a basic or
superbasic constraint has a shadow price of zero then it will be
displayed as 0.0, but if a nonbasic constraint has a shadow price of
zero then it will be displayed as ``ZERO``.

.. rubric:: Unit of shadow price

When the variables and constraints in your model have an associated unit
(see :ref:`chap:units`), special care is required in interpreting the
values returned through the :ref:`.ShadowPrice` suffix. To obtain the
shadow price in terms of the units specified in the model, the values of
the :ref:`.ShadowPrice` suffix must be scaled as explained in
:ref:`sec:units.scaling.mp`.

.. rubric:: The property ``RightHandSideRange``
   :name: attr:var.constr.bound-ranges

.. _smallestrighthandside:

.. _nominalrighthandside:

.. _largestrighthandside:

By specifying the ``RightHandSideRange`` property you request AIMMS to
conduct a first type of sensitivity analysis on this constraint during a
``SOLVE`` statement of a linear program. The result of this sensitivity
analysis are three parameters defined over the domain of the constraint.
Two of these parameters represent the smallest and largest values of an
interval over which an individual *right-hand side* (or left-hand side)
value can be varied such that the basis remains constant. Consequently,
the shadow prices and the reduced costs remain unchanged for variations
of a single value within the interval. The third parameter specifies the
nominal value for the right-hand side (or left-hand side) of the
constraint.

.. rubric:: Single sided or ranged constraint

There are three cases we have to consider for the ``RightHandSideRange``
property:

-  if the constraint is single sided (i.e. :math:`f(x) \leq a`) then the
   smallest, nominal, and largest value for the constraint side are
   reported (both when constraint is binding and not binding)

-  if the constraint is of range type (i.e. :math:`a \leq f(x) \leq b`)
   and it is binding at one side, then the smallest, nominal, and
   largest value for the binding side of the constraint are reported

-  if the constraint is of range type (i.e. :math:`a \leq f(x) \leq b`)
   and it is not binding at neither side, then the lowest upper bound
   and the highest lower bound are reported.

The values are accessible through the suffices
:ref:`.SmallestRightHandSide`, :ref:`.NominalRightHandSide`, and
:ref:`.LargestRightHandSide`.

.. _smallestshadowprice:

.. _largestshadowprice:

.. rubric:: The property ``ShadowPriceRange``

With the ``ShadowPriceRange`` property you request AIMMS to conduct a
second type of sensitivity analysis on this constraint during a
``SOLVE`` statement of a linear program. The result of the sensitivity
analysis are two parameters defined over the domain of the variable. The
values assigned to the parameters will be the smallest and largest
values that the *shadow price* of the constraint can take while holding
the objective value constant. The smallest and largest values of the
constraint marginals are accessible through the suffices
:ref:`.SmallestShadowPrice` and :ref:`.LargestShadowPrice`.

.. rubric:: Linear programs only

As with the advanced sensitivity properties of variables (see
:ref:`sec:var.properties`), AIMMS also supports the advanced sensitivity
analysis conducted through the properties ``RightHandSideRange`` and
``ShadowPriceRange`` for linear mathematical programs only. Again, if
you want to apply these types of analysis to the final solution of a
mixed-integer program, you should fix all integer variables to their
final solution (using the ``.NonVar`` suffix) and re-solve the resulting
mathematical program as a linear program.

.. rubric:: Storage and computational costs

Setting any of the properties ``ShadowPrice``, ``ShadowPriceRange`` or
``RightHandSideRange`` may result in an increase of the memory usage. In
addition, the computations required to compute the ``ShadowPriceRange``
may considerably increase the total solution time of your mathematical
program.

.. _sec:var.constr.glob-suff:

Constraint Suffices for Global Optimization
-------------------------------------------

.. _constraint.globopt:

.. rubric:: Suffices for global optimization

AIMMS provides a number of constraint suffices especially for the global
optimization solver BARON. They are:

-  the :ref:`.Convex` suffix, and

-  the :ref:`.RelaxationOnly` suffix.

By providing additional knowledge, that cannot be determined
automatically by BARON itself, about the constraints in your model
through these suffices, the BARON solver may be able to optimize your
global optimization model in a more efficient manner. For more detailed
information about the specific capabilities of the BARON solver, you are
referred to the BARON website http://www.theoptimizationfirm.com/.

.. rubric:: The :ref:`.Convex` suffix

The algorithm of the BARON solver exploits convexity-either identified
automatically by BARON itself or explicitly supplied in the model
formulation-in order to generate polyhedral cutting planes and
relaxations for multivariate non-convex problems. Through the
:ref:`.Convex` suffix you can explicitly indicate that a particular
constraint is convex if BARON is unable to determine its convexity
automatically.

.. rubric:: The :ref:`.RelaxationOnly` suffix

Using the :ref:`.RelaxationOnly` suffix, you can considerably enhance the
convexification capabilities of BARON. Some nonlinear problem
reformulations can often tighten the relaxation process of BARON's
branch-and-bound algorithm while making local search considerably more
difficult. By assigning a nonzero value to the :ref:`.RelaxationOnly`
suffix, you indicate to BARON that the constraint at hand should only be
included as a relaxation to the branch-and-bound algorithm, while it
should be excluded from the local search.

.. _sec:var.constr.chance:

Chance Constraints
------------------

.. rubric:: Chance constraints

The AIMMS modeling language offers facilities for robust optimization
models, including support for *chance constraints* (see also
:ref:`sec:robust.chance`). By setting the ``Chance`` property of a
constraint, the constraint will become a chance constraint when solving
a mathematical program using robust optimization, using the
distributions specified for the random parameters contained in its
definition. When setting the ``Chance`` property, two new attributes
will become available, the ``Probability`` attribute and the
``Approximation`` attribute.

.. rubric:: Only for robust optimization

Note that setting the ``Chance`` property does not influence the
availability and use of the constraint outside the context of robust
optimization. In that case, AIMMS will just use the original,
deterministic, constraint definition, completely disregarding the
uncertainty of the parameters used in the constraint.

.. rubric:: The ``Probability`` attribute

Through the ``Probability`` attribute, you can specify the probability
with which you want the constraint to be satisfied for any feasible
solution to the robust counterpart of a robust optimization model. Its
value must be a numerical expression in the range :math:`[0,1]`.

.. rubric:: The ``Approximation`` attribute

When constructing the robust counterpart, AIMMS can use several types of
approximations to approximate the chance constraint at hand. You can use
the ``Approximation`` attribute to specify the type of approximation you
want to be applied. The chosen type of approximation may lead to a
robust counterpart which is easier or harder to solve (see also
:ref:`sec:robust.chance`). The value of the attribute must be an element
expression into the predefined set ``AllChanceApproximationTypes``.