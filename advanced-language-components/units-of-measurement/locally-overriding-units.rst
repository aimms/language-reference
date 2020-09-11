.. _sec:units.local-override:

Locally Overriding Units
========================

.. rubric:: Locally overriding units

In some rare occasions the unit specified in the declaration of a
particular identifier does not necessarily have to match with the unit
of the data for that identifier. In that case, AIMMS allows you just to
override the unit of a particular expression locally. Such a local unit
override of an expression always takes the simple form

   *(*\ expression\ *) [*\ simple-unit-expression\ *]*

where *expression* is some AIMMS expression, and
*simple-unit-expression* is a simple unit expression as explained in
:ref:`sec:units.expr`. If *expression* solely consists of a numeric
constant, AIMMS allows you to omit the parentheses around it.

.. rubric:: Where to use

You can use local unit overrides in a variety of data I/O related
situations.

-  In a ``WRITE``, ``DISPLAY`` or ``PUT`` statement, you can use a local
   unit override to specify the particular unit in which data must be
   written to a file, database table or window.

-  In the :any:`FormatString` function, you can use a local unit override
   to specify the unit in which a numeric argument corresponding to a
   ``%n`` format specifier must be formatted.

-  On the left side of a data assignment, in the header of a composite
   table, or in a ``READ`` statement, you can use a local unit override
   to specify the unit in which the supplied data to be provided.

.. rubric:: Commensurate requirement

In all these data I/O statements and expressions, AIMMS requires that
the unit provided in the override is commensurate with the original unit
that can be associated with the expression.

.. rubric:: Example

Given the declarations of the examples in the :ref:`sec:units.analysis`,
the following data I/O statements locally override the default unit
``[km/h]`` of the identifier ``VelocityOfItem`` with the commensurate
unit ``[mph]``.

-  Override per identifier:

   .. code-block:: aimms
   
   	(VelocityOfItem) [mph] := DATA { car: 55, truck: 45 };
   	read (VelocityOfItem) [mph] from table VelocityTable;
   	display (VelocityOfItem) [mph];

-  Override per individual entry:

   .. code-block:: aimms
   
   	put (VelocityOfItem('car')) [mph];
   	StringVal := FormatString("Speed in [mph]: %n", (VelocityOfItem('car')) [mph]);

Recall that parentheses are always required when you want to override
the default unit in expressions and statements, unless the overridden
expression is a simple numeric constant.

.. rubric:: Override for consistency

In addition to overriding units during a data exchange, you can also
override the unit of a (sub)expression in an assignment with the purpose
of enforcing unit consistency of all terms in the assignment. This is
especially useful when there are numeric constants inside your
expressions. AIMMS will add the appropriate scale factor if the
specified unit override does not match with the corresponding atomic
unit expression.

.. rubric:: Examples

The following examples illustrate unit overrides with the purpose of
enforcing unit consistency.

-  Consider the assignment

   .. code-block:: aimms
   
   	SoundIntensity := (10 * log10( SoundLevel / ReferenceLevel )) [dB];

   If ``SoundIntensity`` has an associated unit of ``[dB]``, the right
   hand side of the assignment, which by itself is unitless, must be
   locally overridden to make the entire assignment unit consistent.

-  Consider the assignment

   .. code-block:: aimms
   
   	a := b + 10 [km];

   where both ``a`` and ``b`` are measured in terms of length. As
   discussed in :ref:`sec:units.analysis`, AIMMS will make no assumption
   about the unit associated with the numerical constant ``10`` in the
   expression on the right-hand side of the assignment. In order to make
   the assignment unit consistent, an explicit unit override of the
   constant term is required. If the associated base unit is ``[m]``,
   AIMMS will automatically add a scale factor of 1000, whence the
   assignment will numerically evaluate to ``a := b + 10*1000``.

.. rubric:: Caution is needed

If you explicitly associate a unit with an expression which already
contains one or more identifiers *with* associated units, the numerical
result can be unexpected. This is due to fact that AIMMS, during
expression evaluation, uses the unscaled numerical values with respect
to the associated atomic units of each identifier. To illustrate,
reconsider the assignment

.. code-block:: aimms

	a := (b * c) [km];

but now assume that the identifiers ``a``, ``b``, and ``c`` have units
``[km]``, ``[km]``, and ``[10*m]``. If the values of ``b`` and ``c`` are
``1 [km]``\ (``=1000 [m]``) and ``50 [10*m]``\ (``=500 [m]``),
respectively, the numerical result of ``a`` after the assignment will
amount to ``(500 * 1000)*1000 [m]= 500000 [km]``, which may not be the
result that you intended.