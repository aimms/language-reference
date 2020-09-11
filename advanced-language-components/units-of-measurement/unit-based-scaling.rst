.. _sec:units.scaling:

Unit-based Scaling
==================

.. rubric:: Scaled versus unscaled values

With each identifier for which you have specified a :any:`Unit` attribute,
AIMMS associates two values:

-  the *scaled* value (i.e. expressed in terms of the unit specified),
   and

-  the *unscaled* value (i.e. expressed in terms of the associated
   atomic unit expression).

The transformation between scaled and nonscaled values is completely
determined by the product of explicit and implicit scale factors
associated with the various quantity and unit definitions.

.. rubric:: When used

As mentioned in :ref:`sec:units.analysis`, AIMMS uses internally
unscaled values for all storage and arithmetic computations. This
guarantees automatic scale consistency. However, for external use,
scaled values are more natural when exchanging data with components
outside the AIMMS execution system. Specifically, AIMMS uses scaled
values when

-  displaying the data of an identifier in the (end-)user interface,

-  exchanging data for a particular identifier with files and databases
   using the ``READ`` and ``WRITE`` statements,

-  passing arguments to external procedures and functions,

-  storing the result value(s) of an external function, and

-  communicating the variables and constraints of a mathematical program
   to a solver.

.. rubric:: Units in displays

When displaying data in either the graphical user interface or in
``PUT`` and ``DISPLAY`` statements, AIMMS will transfer data using the
scaled unit specified in the definition of the identifier. For example,
if you have specified ``kton`` as the unit attribute of an identifier
while the underlying atomic unit is ``kg``, AIMMS will still display the
identifier values in ``kton``.

.. rubric:: ...and data entry

Similarly, when reading data from or writing data to scalar numerical
constants, lists, tables, composite tables (either graphical or in data
files), or tables (in databases) using the ``READ`` and ``WRITE``
statements, AIMMS assumes that this data is provided in the (scaled)
units that you have specified in the identifier declarations in your
model, and will transform all data to the corresponding unscaled values
for internal storage.

.. rubric:: Override default scaling

You can override the default scaling based on the content of the
:any:`Unit` attribute either locally within the graphical end-user
interface or model source, or globally using ``Conventions``. Local and
global overrides are discussed in complete detail in
:ref:`sec:units.local-override` and :ref:`sec:units.convention`.

.. _sec:units.scaling.mp:

Unit-based Scaling of Mathematical Programs
-------------------------------------------

.. rubric:: Automatic scaling for solvers

During communications with a solver, AIMMS will scale all variables and
constraints (including variable definitions) in accordance with the
scale factor associated with the :any:`Unit` attribute in their
declaration. This choice is based on the assumption that the specified
units reflect the expected order of magnitude of the numbers associated
with the variables, parameters and constraints, and that these numbers
will neither be very large nor very small. As a result, the values of
all rows and columns in the generated mathematical program are expected
to be of the same, reasonable, order of magnitude. Especially nonlinear
solvers may greatly benefit from this choice.

.. rubric:: Main example revisited

In the main example of :ref:`sec:units.analysis`, the scale factors are
:math:`10^3` for the identifier ``WeightOfItem(i)``, :math:`1/3.6` for
``VelocityOfItem(i)``, and :math:`10^6` for ``KineticEnergyOfItem(i)``.
The entire constraint associated with the defined variable is then
scaled according to the scale factor of the unit of the definition
variable ``KineticEnergyOfItem(i)``, ``MJ``. This corresponds with
dividing the left- and right-hand side of the constraint by
:math:`10^6`. Thus, the resulting expression communicated to the solver
by AIMMS will be:

.. code-block:: aimms

	KineticEnergyOfItemColumn(i) =
	    1/2 * (1/10^3) * WeightofItemColumn(i) * ((1/3.6) * VelocityOfItemColumn(i))^2 ;

Notice that each variable shown in this expression has a suffix
``Column`` to indicate that it corresponds to a column in the matrix
underlying the mathematical program.

.. rubric:: Units of reduced cost and shadow price

Some care is needed when you have requested sensitivity information
associated with a mathematical program, such as the reduced costs of
variables and shadow prices of constraints. The basic rules with respect
to retrieving sensitivity information are as follows:

-  All sensitivity suffices in AIMMS, such as the :ref:`.ReducedCost` and
   :ref:`.ShadowPrice` suffix, are unitless.

-  All sensitivity suffices hold the exact numerical value as computed
   by the solver, i.e. expressed with respect to the scaled values that
   are communicated to the solver by AIMMS.

.. rubric:: Motivating the choice of unitless

The reason for not associating units with the sensitivity suffices is
that a single variable or constraint may be used in multiple
mathematical programs, each with its own objective. As each objective
may have a different associated unit, and the reduced costs and shadow
prices express properties of a variable or constraint with respect to
the objective, it is inherently impossible to associate a single unit
with the :ref:`.ReducedCost` and :ref:`.ShadowPrice` suffices.

.. rubric:: Unitand scale consistent sensitivity data

You may encounter scaling problems when you want to perform direct
computations with the sensitivity suffices of variables and constraints.
Using the ``.Unit`` suffix and AIMMS' capabilities to override units of
subexpressions (see :ref:`sec:units.expr` and
:ref:`sec:units.local-override`), however, it is easy to formulate
expressions that

-  result in the correct unscaled numerical values that can be used
   directly in AIMMS computations, and

-  have an associated unit that is consistent with their interpretation.

.. rubric:: Example with unit overrides

Assuming that ``ExampleVariable`` and ``ExampleConstraint`` are part of
a mathematical program, with ``ObjectiveVariable`` as its objective
function, one can obtain the correct values by locally overriding the
units of the :ref:`.ReducedCost` and :ref:`.ShadowPrice` suffices through the
expressions:

.. code-block:: aimms

	(ExampleVariable.ReducedCost  ) [ObjectiveVariable.Unit / ExampleVariable.Unit  ]
	(ExampleConstraint.ShadowPrice) [ObjectiveVariable.Unit / ExampleConstraint.Unit]

.. rubric:: Example with unit functions

Alternatively, you can use the function :any:`EvaluateUnit` (see
:ref:`sec:units.expr.eval`) to obtain the same result

.. code-block:: aimms

	ExampleVariable.ReducedCost *
	        EvaluateUnit( ObjectiveVariable.Unit / ExampleVariable.Unit )
	ExampleConstraint.ShadowPrice *
	        EvaluateUnit( ObjectiveVariable.Unit / ExampleConstraint.Unit )

.. rubric:: Introducing new parameters

If you need to perform multiple computations with these expressions, or
want to display them in the graphical end-user interface, you are
advised to assign these expressions to additional parameters in your
model with the appropriate associated units.

.. rubric:: Example with convention

When you have used a ``Convention`` to override the default scaling
during the ``SOLVE`` statement, the expressions above should be
augmented by applying the functions :any:`ConvertUnit` and :any:`EvaluateUnit`
(see :ref:`sec:units.expr.func`):

.. code-block:: aimms

	ExampleVariable.ReducedCost *
	        EvaluateUnit( ConvertUnit(ObjectiveVariable.Unit, ConventionUsed) /
	                      ConvertUnit(ExampleVariable.Unit, ConventionUsed)    )
	ExampleConstraint.ShadowPrice *
	        EvaluateUnit( ConvertUnit(ObjectiveVariable.Unit, ConventionUsed) /
	                      ConvertUnit(ExampleConstraint.Unit, ConventionUsed)  )

This will result in a scaling factor that is consistent with the
variable and constraint scaling convention passed to the solver. You
cannot obtain the same result by locally overriding the units of the
:ref:`.ReducedCost` and :ref:`.ShadowPrice` suffices, as unit local overrides
only accept simple unit expressions (see :ref:`sec:units.expr`).

.. rubric:: Use of unit parameters

If your model contains multiple computations concerning the
:ref:`.ReducedCost` and :ref:`.ShadowPrice` suffices, each with identical
scale factors, you may consider assigning the unit expressions required
for scaling these suffices to unit parameters (see
:ref:`sec:units.unit-par`). You can then directly use such unit
parameters in a local unit override, rather than having to repeat
possibly complex unit expressions time and again. For instance, if
``ScaledUnit`` is a unit parameter defined by

.. code-block:: aimms

	ScaledUnit := ConvertUnit(ObjectiveVariable.Unit, ConventionUsed) /
	              ConvertUnit(ExampleVariable.Unit, ConventionUsed) ;

then the correctly scaled expression for the reduced cost of
``ExampleVariable`` can be simplified to

.. code-block:: aimms

	(ExampleVariable.ReducedCost) [ScaledUnit]

You can use a local override, because a reference to a scalar unit
parameter again forms a valid simple unit expression (see
:ref:`sec:units.expr`).