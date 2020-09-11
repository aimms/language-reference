.. _sec:units.analysis:

Unit Analysis
=============

.. rubric:: Unit consistency

By associating a unit with every relevant identifier in your model, you
enable AIMMS to automatically verify whether all terms in the
assignments and constraints of your model are unit consistent. When
AIMMS detects unit inconsistencies, this may help you to solve
conceptual problems in your model, which could otherwise have remained
undetected for a long time.

.. rubric:: ...always in atomic units

With every derived unit or compound unit symbol, it is possible to
associate a unique unit expression consisting of a constant scale factor
and atomic units only. *All assignments and definitions in AIMMS are
interpreted as formulas expressed in terms of these atomic unit
expressions, and unit consistency checking is based on this
interpretation*. While ignoring the constant scale factors, AIMMS will
verify that the atomic unit expression for every term in either an
assignment statement or a constraint is identical. If the resulting unit
check identifies an inconsistency, an error or warning will be
generated.

.. rubric:: Example

Consider the identifiers ``a``, ``b``, and ``c`` having units ``[m]``,
``[km]``, and ``[10*m]`` respectively, all with ``[m]`` as their
corresponding associated atomic unit expression, and scale factors 1,
1000 and 10, respectively. Then the assignment

.. code-block:: aimms

	c := a + b ;

is *unit consistent*, because all terms share the same atomic unit
expression ``[m]``.

.. rubric:: Constant expressions

If an expression on the right-hand side of an assignment consists of a
constant scalar term or a data expression (preceded by the keyword
``DATA``), AIMMS will assume by default that such expressions have the
same unit as the identifier on the left-hand side. If the intended unit
of the right-hand side is different than the declared unit of the
identifier on the left, you should explicitly specify the appropriate
unit for this term, by locally overriding the unit as explained in
:ref:`sec:units.local-override`.

.. rubric:: Constant terms in expressions

On the other hand, if a non-constant expression contains a constant
term, then AIMMS will make no assumption about the intended unit of the
constant term. In fact, it is considered unitless. If a unit
inconsistency occurs for that reason, you should explicitly add a unit
to the constant term to resolve the inconsistency, as explained in
:ref:`sec:units.local-override`.

.. rubric:: Example

Given parameters ``a`` (``[m]`` and ``b`` (``[km]``), as well as a
1-dimensional parameter ``d(i)`` with associated unit ``[m]``, the
following assignments illustrate the interpretation of constant numbers
by AIMMS.

.. code-block:: aimms

	a    := 10;                    ! OK:    constant number 10 interpreted as [m]
	a    := 10 [km];               ! OK:    constant number 10 interpreted as [km]
	d(i) := DATA { 1: 10, 2: 20 }; ! OK:    all data interpreted as [m]
	a    := 10*b;                  ! OK:    constant number 10 considered unitless
	a    := b + 10;                ! ERROR: unit inconsistency, constant term 10 unitless
	a    := b + 10 [km];           ! OK:    unit inconsistency resolved

.. rubric:: Automatic unit checking on or off

By default, the global AIMMS option to perform automatic unit analysis
is on and inconsistencies are detected. AIMMS will produce either
warning messages or error messages (the former is the default). You can
find the full details on all unit-related options in the help file that
comes with your AIMMS system.

.. rubric:: Automatic scale consistency

The assignment ``c := a + b`` of the first example in this section is
unit consistent, but it does not appear to be *scale consistent* since
the units of ``a``, ``b`` and ``c`` have different scales. In AIMMS,
however, a unit consistent assignment is automatically scale consistent,
because AIMMS translates and stores all data in terms of the underlying
atomic unit expression. In the example, this implies that the use of the
values of ``a``, ``b``, and ``c`` as well as the assignment are in the
atomic unit ``[m]``. Consequently, AIMMS can now directly execute the
assignment, and the scale consistency is automatically ensured. Of
course, any *display* of values of ``a``, ``b`` and ``c`` will be again
in terms of the units associated with these identifiers.

.. rubric:: Advanced example...

This example illustrates a number of identifiers with compound unit
definitions. It is based on the SI units for weight, velocity and
energy, and uses the derived units ``ton``, ``km``, ``h`` and ``MJ``.

.. code-block:: aimms

	Variable WeightOfItem {
	    IndexDomain  : i;
	    Unit         : ton;
	}
	Variable VelocityOfItem {
	    IndexDomain  : i;
	    Unit         : Velocity: km/h;
	}
	Variable KineticEnergyOfItem {
	    IndexDomain  : i;
	    Unit         : MJ;
	    Definition   : 1/2 * WeightofItem(i) * VelocityOfItem(i)^2;
	}

Any display of these variables will be in terms of ``ton``, ``km/h`` and
``MJ``, respectively, but internally AIMMS uses the units ``kg``,
``m/s`` and ``kg*m^2/s^2`` for storage. The latter represent the
corresponding unique atomic unit expressions associated with weight,
velocity and energy.

.. rubric:: ...is unit consistent

As a consequence of specifying units, there will be an automatic
consistency check on the defined variable ``KineticEnergyOfItem(i)``.
AIMMS interprets the definition of ``KineticEnergyOfItem(i)`` as a
formula expressed in terms of the atomic units. The relevant unit
components are:

-  ``[ton ] = 10^3    * [kg        ]``,

-  ``[km/h] = (1/3.6) * [m/s       ]``, and

-  ``[MJ  ] = 10^6    * [kg*m^2/s^2]``.

The definition of ``KineticEnergyOfItem(i)`` as expressed in terms of
atomic units is ``kg*(m/s)^2``, while its own unit in terms of atomic
units is ``kg*m^2/``\ ``s^2``. These two unit expressions are
consistent.

.. rubric:: Beware of non-absolute units

If the unit conversion between a derived unit and its corresponding
atomic unit not only consists of a scale factor, but also contains a
constant term, such a derived unit is referred to as a *non-absolute*
unit. If an arithmetic expression in your model refers to identifiers or
constants expressed in a non-absolute unit, you should pay special
attention to make sure that the result of the computation is what you
intended. The following example makes the point.

.. rubric:: Example

Consider the following quantity declaration.

.. code-block:: aimms

	Quantity Temperature {
	    BaseUnit     : K;
	    Conversions  : degC -> K :  # -> # + 273.15;
	}

Given this declaration, what is the result of the assignment

.. code-block:: aimms

	x := 1 [degC] + 2 [degC];

where ``x`` is a scalar parameter with unit ``degC``? Following the
rules explained above-AIMMS stores all data and performs all
computations in terms of atomic units- AIMMS performs the following
computation internally

.. code-block:: aimms

	x := 274.15 [K] + 275.15 [K];

resulting in an assignment to ``x`` of :math:`549.3`
``[K]``\ :math:`{}= 276.15` ``[degC]``, which is probably not the
intended answer. The key observation is that in an addition only one of
the operands should be expressed in a non-absolute unit. Similarly, in a
multiplication or division probably none of the operands should be
expressed in a non-absolute unit. The mistake in the above assignment is
that the second argument in fact should be a temperature difference
(e.g. between 3 ``[degC]`` and 1 ``[degC]``), which precisely yields an
expression in terms of the corresponding absolute unit ``K``:

.. code-block:: aimms

	x := 1 [degC] + (3 [degC] - 1 [degC]);     ! equals 274.15 [K] + 2 [K] = 3 [degC]

Using temperature differences is more common in assignments to
identifiers like ``LengthIncreasePerDegC`` (expressed in ``[m/degC]``),
which probably takes the form of a *difference quotient*, as illustrated
below.

.. code-block:: aimms

	LengthIncreasePerDegC := (Length1 - Length0) / (Temperature1 - Temperature0);

.. rubric:: Units and intrinsic functions

When you use an intrinsic AIMMS function (see
:ref:`sec:expr.num.functions`) inside an expression in your model, the
unit associated with the corresponding function call will in general
depend on its arguments. The unit relationship between the arguments and
the result of the function falls into one of the following function
categories.

-  *Unitless* functions, for which both the arguments and the result are
   dimensionless. Examples are: ``exp``, ``log``, ``log10``, ``errorf``,
   ``atan``, ``cos``, ``sin``, ``tan``, ``degrees``, ``radians``,
   ``atanh``, ``cosh``, ``sinh``, ``tanh``, and the exponential operator
   with a non-constant exponent.

-  *Transparent* functions that do not alter units. Examples are:
   ``abs``, ``max``, ``min``, ``mod``, ``ceil``, ``floor``,
   ``precision``, ``round``, and ``trunc``.

-  *Conversion* functions that convert units in a predictable way.
   Examples are: ``sqr``, ``sqrt``, and the exponential operator with a
   constant integer exponent.

.. rubric:: Explicit units in expressions

In some exceptional cases, one or more terms in an expression may not be
unit consistent with the other terms in the expression. To restore unit
consistency, AIMMS allows you to explicitly specify a unit for the
inconsistent term(s) as an emergency measure. The syntax for such unit
overrides is explained in :ref:`sec:units.local-override`. You should
make sure, however, that these explicit unit overrides do not affect the
scale consistency of the expression (see
:ref:`sec:units.local-override`).

.. _sec:units.analysis.arg:

Unit Analysis of Procedures and Functions
-----------------------------------------

.. rubric:: Unit analysis of procedures and functions

Once you have associated units of measurement with the global
identifiers in your model, you will also need to associate units of
measurement with the arguments, local identifiers and result values of
procedures and functions. When you do so, you enable AIMMS to perform
the common unit analysis on the statements in the bodies of all internal
procedures and functions. For external procedures and functions, AIMMS
cannot perform a unit analysis on the function and procedure bodies, but
will use the assigned units for scaling purposes as explained in
:ref:`sec:units.scaling`.

.. rubric:: Two procedure types

In general, one can distinguish two types of procedures and functions,
namely

-  procedures and functions of a very specific nature, whose arguments
   and result values have associated units of measurement that are
   constant and known a priori, and

-  procedures and functions of a very general nature, whose arguments
   and result values can have any associated unit of measurement.

An example of the latter type is a function with a single
one-dimensional argument to compute the average of all values contained
in its argument. For such a function, the specific units associated with
the argument and the result values are not known a priori, but it is
known that they must be equal.

.. rubric:: Express units in local unit parameters

To let you declare procedure and functions of the second type, AIMMS
allows you to express the units of measurement of its arguments and the
result values in terms of unit parameters (see also
:ref:`sec:units.unit-par`) declared locally within the procedure or
function. At runtime, AIMMS will dynamically determine the value of the
unit parameter, based on the actual arguments passed to the procedure or
function. In addition, AIMMS will verify that the unit of a function
value is commensurate with the remainder of the statement or expression
from which it was called.

.. rubric:: Example

The function ``MyAverage`` in this example computes the average of a
general one-dimensional identifier. It combines AIMMS' ability to define
arguments over local sets (see :ref:`sec:intern.proc`), with a unit
expressed in term of a local unit parameter. Its declaration is given by

.. code-block:: aimms

	Function MyAverage {
	    Arguments : (Ident);
	    Unit      : LocalUnit;
	    Body      : {
	        MyAverage := sum(i, Ident(i)) / Card(LocalSet)
	    }
	}

The single argument ``Ident(i)`` of the function ``MyAverage`` is
defined by

.. code-block:: aimms

	Parameter Ident {
	    IndexDomain  : i;
	    Unit         : LocalUnit;
	}
	Set LocalSet {
	    Index        : i;
	}
	UnitParameter LocalUnit;

Note that ``Ident(i)`` is defined over a local set ``LocalSet`` and that
its unit is expressed in terms of a local unit parameter ``LocalUnit``,
both of which are determined at runtime. Because the unit of the
function ``MyAverage`` itself is also equal to ``LocalUnit``, the
assignment in the body of ``MyAverage`` is unit consistent.