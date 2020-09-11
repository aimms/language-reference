.. _sec:var.var:

``Variable`` Declaration and Attributes
=======================================

.. _variable:

.. rubric:: Declaration and attributes

Variables have some additional attributes above those of parameters.
These extra attributes are used to steer a solver, or to hold additional
information about solution values provided by the solver. The possible
attributes of variables are given in :numref:`table:var.attr-variable`.

.. _table:var.attr-variable:

.. table:: 

	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| Attribute        | Value-type                                                    | See also page                                                                                                              |
	+==================+===============================================================+============================================================================================================================+
	| ``IndexDomain``  | *index-domain*                                                | :ref:`here <attr:par.index-domain>`                                                                                        |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Range``        | *range*                                                       | :ref:`here <attr:par.range>`                                                                                               |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Default``      | *constant-expression*                                         | :ref:`here <attr:par.default>`                                                                                             |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| :any:`Unit`      | *unit-expression*                                             | :ref:`The Parameter Unit attribute <attr:par.unit>`, :ref:`chap:units`                                                     |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Priority``     | *expression*                                                  |                                                                                                                            |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``NonvarStatus`` | *expression*                                                  |                                                                                                                            |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``RelaxStatus``  | *expression*                                                  |                                                                                                                            |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Property``     | ``NoSave``, *numeric-storage-property*, ``Inline``            | :ref:`The Set Property attribute <attr:set.property>`, :ref:`The Parameter Property attribute <attr:par.property>`         |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	|                  | ``SemiContinuous``, ``Basic``, ``Stochastic``, ``Adjustable`` |                                                                                                                            |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	|                  | ``ReducedCost``, ``ValueRange``, ``CoefficientRange``,        |                                                                                                                            |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	|                  | *constraint-related-sensitivity-property*                     |                                                                                                                            |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Text``         | *string*                                                      | :ref:`here <attr:prelim.text>`                                                                                             |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Comment``      | *comment string*                                              | :ref:`here <attr:prelim.comment>`                                                                                          |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Definition``   | *expression*                                                  | :ref:`The Set Definition attribute <attr:set.definition>`, :ref:`The Parameter Definition attribute <attr:par.definition>` |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Stage``        | *expression*                                                  | :ref:`sec:var.uncertainty`, :ref:`sec:stoch.stoch`                                                                         |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	| ``Dependency``   | *expression*                                                  | :ref:`sec:var.uncertainty`, :ref:`The Robust Dependency attribute <attr:robust.dependency>`                                |
	+------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Index domain for variables
   :name: attr:var.index-domain

.. _variable.index_domain:

By specifying the ``IndexDomain`` attribute you can restrict the domain
of a variable in the same way as that of a parameter. For variables,
however, the domain restriction has an additional effect. During the
generation of individual constraints AIMMS will reduce the size of the
generated mathematical program by including only those variables that
satisfy all domain restrictions.

.. rubric:: The ``Range`` attribute
   :name: attr:var.range

.. _variable.range:

The values of the ``Range`` attribute of variables determine the bounds
that are passed on to the solver. In addition, during an assignment, the
``Range`` attribute restricts the range of allowed values that can be
assigned to a particular interval (as for parameters). The possible
values for the ``Range`` attribute are:

-  one of the predefined ranges ``Real``, ``Nonnegative``,
   ``Nonpositive``, ``Integer`` or ``Binary``,

-  any one of the interval expressions ``[``\ :math:`a,b`\ ``]``,
   ``[``\ :math:`a,b`\ ``)``, ``(``\ :math:`a,b`\ ``]`` or
   ``(``\ :math:`a,b`\ ``)``, where :math:`a` and :math:`b` can be a
   constant number, ``inf``, ``-inf``, or a parameter reference
   involving some or all of the indices on the index list of the
   declared variable,

-  any enumerated integer set expression, e.g. ``{``\ :math:`a` ``..``
   :math:`b`\ ``}`` with :math:`a` and :math:`b` as above, or

-  an integer set identifier.

If you specify ``Real``, ``Nonnegative``, ``Nonpositive``, or an
interval expression, AIMMS will interpret the variable as a continuous
variable. If you specify ``Integer``, ``Binary`` or an integer set
expression, AIMMS will interpret the variable as a binary or integer
variable.

.. rubric:: Example

The following example illustrates a simple variable declaration.

.. code-block:: aimms

	Variable Transport {
	    IndexDomain  : (i,j) in Connections;
	    Range        : [ MinTransport(i), Capacity(i,j) ];
	}

The declaration of the variable ``Transport(i,j)`` sets its lower bound
equal to ``MinTransport(i)`` and its upper bound to ``Capacity(i,j)``.
When generating the mathematical program, the variable ``Transport``
will only be generated for those tuples (``i``,\ ``j``) that lie in the
set ``Connections``. Note that the specification of the lower bound only
uses a subdomain (``i``) of the full index domain of the variable
(``i,j``).

.. _lower:

.. _upper:

.. rubric:: The :ref:`.Lower` and :ref:`.Upper` suffices

Besides using the ``Range`` attribute to specify the lower and upper
bounds, you can also use the :ref:`.Lower` and :ref:`.Upper` suffices in
assignment statements to accomplish this task. The :ref:`.Lower` and
:ref:`.Upper` suffices are attached to the name of the variable, and, as a
result, the corresponding bounds are defined for the entire index
domain. This may lead to increased memory usage when variables share
their bounds for slices of the domain. For this reason, you are advised
to use the ``Range`` attribute as much as possible when specifying the
lower and upper bounds.

.. rubric:: When allowed

You can only make a bound assignment with either the :ref:`.Lower` or
:ref:`.Upper` suffix when you have not used a parameter reference (or a
non-constant expression) at the corresponding position in the ``Range``
attribute. Bound assignments via the :ref:`.Lower` and :ref:`.Upper` suffices
must always lie within the range specified in the ``Range`` attribute.

.. rubric:: Example

Consider the variable ``Transport`` declared in the previous example.
The following assignment to ``Transport.Lower(i,j)`` is not allowed,
because you have already specified a parameter reference at the
corresponding position in the ``Range`` attribute.

.. code-block:: aimms

	Transport.Lower(i,j) := MinTransport(i) ;

On the other hand, given the following declaration,

.. code-block:: aimms

	Variable Shipment {
	    IndexDomain  : (i,j) in Connections;
	    Range        : Nonnegative;
	}

the following assignment is allowed:

.. code-block:: aimms

	Shipment.Lower(i,j) := MinTransport(i);

AIMMS will produce a run-time error message if any value of
``MinTransport(i)`` is less than zero, because this violates the bound
in the ``Range`` attribute of the variable ``Shipment``.

.. rubric:: The ``Default`` attribute
   :name: attr:var.default

.. _variable.default:

Variables that have not been initialized, evaluate to a default value
automatically. These default values are also passed as initial values to
the solver. You can specify the default value using the ``Default``
attribute. The value of this attribute *must* be a constant expression.
If you do not provide a default value, AIMMS will use a default of 0.

.. rubric:: The :any:`Unit` attribute
   :name: attr:var.unit

.. _variable.unit:

Providing a :any:`Unit` for every variable and constraint in your model
will help you in a number of ways.

-  AIMMS will help you to check the consistency of all your constraints
   and assignments in your model, and

-  AIMMS will use the units to scale the model that is sent to the
   solver.

Proper scaling of a model will generally result in a more accurate and
robust solution process. You can find more information on the definition
and use of units to scale mathematical programs in :ref:`chap:units`.

.. rubric:: The ``Definition`` attribute
   :name: attr:var.definition

.. _variable.definition:

It is not unusual that symbolic constraints in a model are equalities
defining just one variable in terms of others. Under these conditions,
it is preferable to provide the definition of the variable through its
``Definition`` attribute. As a result, you no longer need to specify
extra constraints for just variable definitions. In the constraint
listing, the constraints associated with a defined variable will be
listed with a generated name consisting of the name of the variable with
an additional suffix ``_definition``.

.. rubric:: Example

The following example defines the total cost of transport, based on unit
transport cost and actual transport taking place.

.. code-block:: aimms

	Variable TransportCost {
	    Definition : sum( (i,j), UnitTransportCost(i,j)*Transport(i,j) );
	}

.. _sec:var.var.solver-attr:

The ``Priority``, ``Nonvar`` and ``RelaxStatus`` Attributes
-----------------------------------------------------------

.. rubric:: The ``Priority`` attribute
   :name: attr:var.priority

.. _variable.priority:

With the ``Priority`` attribute you can assign priorities to integer
variables (or continuous variables when using the solver BARON). The
value of this attribute must be an expression using some or all of the
indices in the index domain of the variable, and must be nonnegative and
integer. All variables with priority zero will be considered last by the
branch-and-bound process of the solver. For variables with a positive
priority value, those with the highest priority value will be considered
first.

.. rubric:: The :ref:`.Priority` suffix
   :name: suffix:var.priority

Alternatively, you can specify priorities through assignments to the
:ref:`.Priority` suffix. This is only allowed if you have not specified the
``Priority`` attribute. In both cases, you can use the :ref:`.Priority`
suffix to refer to the priority of a variable in expressions.

.. rubric:: Use of priorities

The solution algorithm (i.e. solver) for integer and mixed-integer
programs initially solves without the integer restriction, and then adds
this restriction one variable at a time according to their priority. By
default, all integer variables have equal priority. Some decisions,
however, have a natural order in time or space. For example, the
decision to build a factory at some site comes before the decision to
purchase production capacity for that factory. Obeying this order
naturally limits the number of subsequent choices, and could speed up
the overall search by the solution algorithm.

.. rubric:: The ``NonvarStatus`` attribute
   :name: attr:var.nonvar

.. _variable.nonvar_status:

You can use the ``NonvarStatus`` attribute to tell AIMMS which variables
should be considered as parameters during the execution of a ``SOLVE``
statement. The value of the ``NonvarStatus`` attribute must be an
expression in some or all of the indices in the index list of the
variable, allowing you to change the nonvariable status of individual
elements or groups of elements at once.

.. rubric:: Positive versus negative values

The sign of the ``NonvarStatus`` value determines whether and how the
variable is passed on to the solver. The following rules apply.

-  If the value is 0 (the default value), the corresponding individual
   variable is generated, along with its specified lower and upper
   bounds.

-  If the value is negative, the corresponding individual variable is
   still generated, but its lower and upper bounds are set equal to the
   current value of the variable.

-  If the value is positive, the corresponding individual variable is no
   longer generated but passed as a constant to the solver.

When you specify a negative value, you will still be able to inspect the
corresponding reduced cost values. In addition, you can modify the
nonvariable status to zero without causing AIMMS to regenerate the
model. When you specify a positive value, the size of the mathematical
program is kept to a minimum, but any subsequent changes to the
nonvariable status will require regeneration of the model constraints.

.. _nonvar:

.. rubric:: The ``.NonVar`` suffix

Alternatively, you can change the nonvariable status through assignments
to the ``.NonVar`` suffix. This is only allowed if you have not
specified the ``NonvarStatus`` attribute. In both cases, you can use the
``.NonVar`` suffix to refer to the variable status of a variable in
expressions.

.. rubric:: When to change the nonvariable status

By altering the nonvariable status of variables you are essentially
reconfiguring your mathematical program. You could, for instance,
reverse the role of an input parameter (declared as a variable with
negative nonvariable status) and an output variable in your model to
observe what input level is required to obtain a desired output level.
Another example of temporary reconfiguration is to solve a smaller
version of a mathematical program by first discarding selected
variables, and then changing their status back to solve the larger
mathematical program using the previous solution as a starting point.

.. rubric:: The ``RelaxStatus`` attribute
   :name: attr:var.relax

.. _variable.relax_status:

With the ``RelaxStatus`` attribute you can tell AIMMS to relax the
integer restriction for those tuples in the domain of an integer
variable for which the value of the relax status is nonzero. AIMMS will
generate continuous variables for such tuples instead, i.e. variables
which may assume any real value between their bounds.

.. _relax:

.. rubric:: The :ref:`.Relax` suffix

Alternatively, you can relax integer variables by making assignments to
the :ref:`.Relax` suffix. This is only allowed if you have not specified
the ``RelaxStatus`` attribute. In both cases, you can use the :ref:`.Relax`
suffix to refer to the relax status of a variable in expressions.

.. rubric:: When to relax variables

When solving large mixed integer programs, the solution times may become
unacceptably high with an increase in the number of integer variables.
You can try to resolve this by relaxing the integer condition of some of
the integer variables. For instance, in a multi-period planning model,
an accurate integer solution for the first few periods and an
approximating continuous solution for the remaining periods may very
well be acceptable, and at the same time reduce solution times
drastically.

.. rubric:: Effect on mathematical program type

As you will see in :ref:`chap:mp`, there are several types of
mathematical programs. By changing the nonvariable and/or relax status
of variables you may alter the type of your mathematical program. For
instance, if your constraints contains a nonlinear term ``x*y``, then
changing the nonvariable status of either ``x`` or ``y`` will change it
into a linear term. Eventually, this may result in a nonlinear
mathematical program becoming a linear one. Similarly, changing the
nonvariable or relax status of integer variables may at some point
change a mixed integer program into a linear program.

.. _sec:var.properties:

Variable Properties
-------------------

.. rubric:: Properties of variables
   :name: attr:var.property

Variables can have one or more of the following properties: ``NoSave``,
``Inline``, ``SemiContinuous``, ``ReducedCost``, ``CoefficientRange``,
``ValueRange``, ``Stochastic``, and ``Adjustable``. They are described
in the paragraphs below.

.. rubric:: Use of ``PROPERTY`` statement

You can also change the properties of a variable during the execution of
your model by calling the ``PROPERTY`` statement. Identifier properties
are changed by adding the property name as a suffix to the identifier
name in a ``PROPERTY`` statement. When the value is set to ``off``, the
property no longer holds.

.. rubric:: The ``NoSave`` property

With the property ``NoSave`` you indicate that you do not want to store
data associated with this variable in a case. This property is
especially suited for those identifiers that are intermediate quantities
in the model, and that are not used anywhere in the graphical end-user
interface.

.. rubric:: Inline variables

With the property ``Inline`` you can indicate that AIMMS should
substitute all references to the variable at hand by its defining
expression when generating the constraints of a mathematical program.
Setting this property only makes sense for defined variables, and will
result in a mathematical program with less rows and columns but with a
(possibly) larger number of nonzeros. After the mathematical program has
been solved, AIMMS will compute the level values of all inline variables
by evaluating their definition. However, no sensitivity information will
be available.

.. rubric:: Semi-continuous variables

To any continuous or integer variable you can assign the property
``SemiContinuous``. This indicates to the solver that this variable is
either zero, or lies within its specified range. Not all solvers support
semi-continuous variables. In the latter case, AIMMS will automatically
add the necessary constraints to the model.

.. _sec:var.sensitivity:

Sensitivity Related Properties
------------------------------

.. rubric:: Basic, superbasic, and nonbasic variables

With the ``Basic`` property you can instruct AIMMS to retrieve basic
information of a specific variable from the solver. If retrieved, basic
information can be accessed through the :ref:`.Basic` suffix. The basic
information is presented as an element in the predefined AIMMS set
:any:`AllBasicValues` (i.e. *{Basic, Nonbasic, Superbasic}*). In linear
programming a variable will either be basic or nonbasic, while in
nonlinear programming the number of variables with zero reduced cost can
be larger than the number of constraints. The solution algorithm then
divides these variables into so-called *basics* and *superbasics*. The
basic variables define a square system of nonlinear equations which is
solved for fixed values of the remaining variables. The superbasics are
assigned a fixed value between their bounds, while the nonbasics take
their value at a bound.

.. rubric:: The ``ReducedCost`` property
   :name: attr:var.marginal

.. _ReducedCost:

You can use the ``ReducedCost`` property to specify whether you are
interested in the reduced cost values of the variable after each
``SOLVE`` step. Storing the reduced costs of all variables may be very
memory consuming, therefore, the default in AIMMS is not to store these
values. If reduced costs are requested, the stored values can be
accessed through the suffices :ref:`.ReducedCost` or ``.m``.

.. rubric:: Interpretation of reduced cost
   :name: attr:var.reducedcost

The reduced cost indicates by how much the cost coefficient in the
objective function should be reduced before the variable becomes active
(off its bound). By definition, the reduced cost value of a variable
between its bounds is zero. The precise mathematical interpretation of
reduced cost is discussed in most text books on mathematical
programming. Note: if a basic or superbasic variable has a reduced cost
of zero then it will be displayed as 0.0, but if a nonbasic variable has
a reduced cost of zero then it will be displayed as ``ZERO``.

.. rubric:: Unit of reduced cost

When the variables in your model have an associated unit (see
:ref:`chap:units`), special care is required in interpreting the values
returned through the :ref:`.ReducedCost` suffix. To obtain the reduced cost
in terms of the units specified in the model, the values of the
:ref:`.ReducedCost` suffix must be scaled as explained in
:ref:`sec:units.scaling.mp`.

.. rubric:: The property ``CoefficientRange``
   :name: attr:var.coeff-ranges

.. _smallestcoefficient:

.. _nominalcoefficient:

.. _largestcoefficient:

With the property ``CoefficientRange`` you request AIMMS to conduct a
first type of sensitivity analysis on this variable during a ``SOLVE``
statement of a linear program. The result of this sensitivity analysis
are three parameters, representing the smallest, nominal, and largest
values for the *objective coefficient* of the variable so that the
optimal basis remains constant. Their values are accessible through the
suffices :ref:`.SmallestCoefficient`, :ref:`.NominalCoefficient` and
:ref:`.LargestCoefficient`.

.. rubric:: The property ``ValueRange``
   :name: attr:var.var-ranges

.. _smallestvalue:

.. _largestvalue:

With the property ``ValueRange`` you request AIMMS to conduct a second
type of sensitivity analysis during a ``SOLVE`` statement of a linear
program. The result of the sensitivity analysis are two parameters,
representing the smallest and largest values that the *variable* can
take while holding the objective value constant. Their values are
accessible through the :ref:`.SmallestValue` and :ref:`.LargestValue`
suffices.

.. rubric:: Linear programs only

AIMMS only supports the sensitivity analysis conducted through the
properties ``CoefficientRange`` and ``ValueRange`` for linear
mathematical programs. If you want to apply these types of analysis to
the final solution of a mixed-integer program, you should fix all
integer variables to their final solution (using the ``.NonVar`` suffix)
and re-solve the resulting mathematical program as a linear program
(e.g. by adding the clause ``WHERE type:='lp'`` to the ``SOLVE``
statement).

.. rubric:: Storage and computational costs

Setting any of the properties ``ReducedCost``, ``CoefficientRange`` or
``ValueRange`` may result in an increase of the memory usage. In
addition, the computations required to compute the ``ValueRange`` may
considerably increase the total solution time of your mathematical
program.

.. rubric:: Constraint related properties

Whenever a defined variable (which is not declared ``Inline``) is part
of a mathematical program, AIMMS implicitly adds a constraint to the
generated model expressing this definition. In addition to the
variable-related sensitivity properties discussed in this section, you
can specify the constraint-related sensitivity properties
``ShadowPrice``, ``RightHandSideRange`` and ``ShadowPriceRange`` (see
also :ref:`sec:var.constr`) for such variables to obtain the sensitivity
information that can be related to these constraint. You can access the
requested sensitivity information by appending the associated suffices
to the name of the defined variable.

.. _sec:var.uncertainty:

Uncertainty Related Properties and Attributes
---------------------------------------------

.. rubric:: Stochastic programming and robust optimization

The AIMMS modeling language offers facilities for both stochastic
programs and robust optimization models. For both types of models you
can specify special ``Variable`` properties and attributes to define
uncertainty-related relationships.

.. rubric:: The ``Stochastic`` property

Through the ``Stochastic`` property you can indicate that, within a
stochastic model, the variable can hold scenario-dependent solutions.
AIMMS will add a ``Stage`` attribute for every variable for which the
``Stochastic`` property has been set.

.. _variable.stage:

.. rubric:: The ``Stage`` attribute

The value of the ``Stage`` attribute must be a numerical expression
evaluating to in integer number indicating the stage at the end of which
the variable takes its value during the solution process of a stochastic
model. Stochastic programming, and the ``Stochastic`` property and
``Stage`` attribute are discussed in full detail in
:ref:`sec:stoch.stoch`.

.. rubric:: The ``Adjustable`` property

By setting the ``Adjustable`` property for a variable, you indicate that
a variable in a robust optimization model has a functional dependency on
some or all of the uncertain parameters in the model. If you declare a
variable to be adjustable, the ``Dependency`` attribute also becomes
available for that variable. 

.. _variable.dependency:

.. rubric:: The ``Dependency`` attribute

Through the ``Dependency`` attribute you specify the precise collection
of uncertain parameters on which the variable at hand depends. At this
moment, AIMMS only supports affine relations between uncertain
parameters and adjustable variables. The precise semantics of the
``Dependency`` attribute is discussed in :ref:`sec:robust.adjustable`.