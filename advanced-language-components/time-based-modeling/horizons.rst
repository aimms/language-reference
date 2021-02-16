.. _sec:time.horizon:

Horizons
========

.. rubric:: Horizons

A horizon in AIMMS is basically a set of planning periods. The elements
in a horizon are divided into three groups, also referred to as time
blocks. The main group of elements comprise the *planning interval*.
Periods prior to the planning interval form the *past*, while periods
following the planning interval form the *beyond*. When variables and
constraints are indexed over a horizon, AIMMS automatically restricts
the generation of these constraints and variables to periods within the
planning interval.

.. rubric:: Effect on constraints and assignments

Whenever you use a horizon to construct a time-dependent model, AIMMS
has the following features:

-  constraints are excluded from the past and beyond periods,

-  variables are assumed to be fixed for these periods, and

-  assignments and definitions to variables and parameters are, by
   default, only executed for the periods in the planning interval.

.. _horizon:

.. rubric:: Horizon attributes

Horizons, like calendars, have a number of associated attributes, some
of which are inherited from sets. They are summarized in
:ref:`this table <table:time.attr-horizon>`.

.. _horizon.parameter:

.. _horizon.index:

.. _horizon.subset_of:

.. _table:time.attr-horizon:

.. table:: Horizon attributes

   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | Attribute          | Value-type          | See also page                                         | Mandatory |
   +====================+=====================+=======================================================+===========+
   | ``SubsetOf``       | *subset-domain*     | :ref:`The SubsetOf attribute <attr:set.subset-of>`    |           |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``Index``          | *identifier-list*   | :ref:`The Index attribute <attr:set.index>`           | yes       |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``Parameter``      | *identifier-list*   | :ref:`The Parameter attribute <attr:set.parameter>`   |           |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``Text``           | *string*            | :ref:`The Text attribute <attr:prelim.text>`          |           |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``Comment``        | *comment string*    | :ref:`The Comment attribute <attr:prelim.comment>`    |           |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``Definition``     | *set-expression*    | :ref:`The Definition attribute <attr:set.definition>` | yes       |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``CurrentPeriod``  | *element*           |                                                       | yes       |
   +--------------------+---------------------+-------------------------------------------------------+-----------+
   | ``IntervalLength`` | *integer-reference* |                                                       |           |
   +--------------------+---------------------+-------------------------------------------------------+-----------+

.. _horizon.current_period:

.. _horizon.interval_length:

.. rubric:: Horizon attributes explained

The ``CurrentPeriod`` attribute denotes the first period of the planning
interval. The periods prior to the current period belong to the past.
The integer value associated with the attribute ``IntervalLength``
determines the number of periods in the planning interval (including the
current period). Without an input value, all periods from the current
period onwards are part of the planning interval.

.. _horizon.definition:

.. rubric:: Definition is mandatory

AIMMS requires you to specify the contents of a ``Horizon`` uniquely
through its ``Definition`` attribute. The ordering of the periods in the
horizon is fully determined by the set expression in its definition. You
still have the freedom, however, to specify the ``Horizon`` as a subset
of another set.

.. rubric:: Example

Given a scalar parameter ``MaxPeriods``, the following example
illustrates the declaration of a horizon.

.. code-block:: aimms

	Horizon ModelPeriods {
	    Index          : h;
	    Parameter      : IntervalStart;
	    CurrentPeriod  : IntervalStart;
	    Definition     : ElementRange( 1, MaxPeriods, prefix: "p-" );
	}

If, for instance, the scalar ``MaxPeriods`` equals 10, this will result
in the creation of a period set containing the elements
``'p-01'``,...,\ ``'p-10'``. The start of the planning interval is fully
determined by the value of the element parameter ``IntervalStart``,
which for instance could be equal to ``'p-02'``. This will result in a
planning interval consisting of the periods ``'p-02'``,...,\ ``'p-10'``.

.. rubric:: Example of use

Consider the parameter ``Demand(h)`` together with the variables
``Production(h)`` and ``Stock(h)``. Then the definition of the variable
``Stock`` can be declared as follows.

.. code-block:: aimms

	Variable Stock {
	    IndexDomain    : h;
	    Range          : NonNegative;
	    Definition     : Stock(h-1) + Production(h) - Demand(h);
	}

When the variable ``Stock`` is included in a mathematical program, AIMMS
will only generate individual variables with their associated definition
for those values of ``h`` that correspond to the current period and
onwards. The reference ``Stock(h-1)`` refers to a fixed value of
``Stock`` from the past whenever the index ``h`` points to the current
period. The values associated with periods from the past (and from the
beyond if they were there) are assumed to be fixed.

.. rubric:: Accessing past and beyond

To provide easy access to periods in the past and the beyond, AIMMS
offers three horizon-specific suffices. They are:

-  the ``Past`` suffix,

-  the ``Planning`` suffix, and

-  the ``Beyond`` suffix.

These suffices provide access to the subsets of the horizon representing
the past, the planning interval and the beyond.

.. rubric:: Horizon binding rules

When you use a horizon index in an index binding operation (see
:ref:`chap:bind`), AIMMS will, by default, perform that operation only
for the periods in the planning interval. You can override this default
behavior by a local binding using the suffices discussed above.

.. rubric:: Example

Consider the horizon ``ModelPeriods`` of the previous example. The
following assignments illustrate the binding behavior of horizons.

.. code-block:: aimms

	Demand(h)                          := 10; ! only periods in planning interval (default)
	Demand(h in ModelPeriods.Planning) := 10; ! only periods in planning interval

	Demand(h in ModelPeriods.Past)     := 10; ! only periods in the past
	Demand(h in ModelPeriods.Beyond)   := 10; ! only periods in the beyond

	Demand(h in ModelPeriods)          := 10; ! all periods in the horizon

.. rubric:: Use of lag and lead operators

When you use one of the lag and lead operators ``+``, ``++``, ``-`` or
``--`` (see also :ref:`sec:set-expr.elem.lag-lead`) in conjunction with
a horizon index, AIMMS will interpret such references with respect to
the *entire* horizon, and not just with respect to the planning period.
If the horizon index is locally re-bound to one of the subsets of
periods in the ``Past`` or ``Beyond``, as illustrated above, the lag or
lead operation will be interpreted with respect to the specified subset.

.. rubric:: Example

Consider the horizon ``ModelPeriods`` of the previous example. The
following assignments illustrate the use of lag and lead operators in
conjuction with horizons.

.. code-block:: aimms

	Stock(h)                              := Stock(h-1) + Supply(h) - Demand(h);
	Stock(h | h in ModelPeriods.Planning) := Stock(h-1) + Supply(h) - Demand(h);

	Stock(h in ModelPeriods.Planning)     := Stock(h-1) + Supply(h) - Demand(h);
	Stock(h in ModelPeriods.Planning)     := Stock(h--1) + Supply(h) - Demand(h);

The first two assignments are completely equivalent (in fact, the second
assignment is precisely the way in which AIMMS interprets the default
binding behavior of a horizon index). For the first element in the
planning interval, the reference ``h-1`` refers to the last element of
the past interval. In the third assignment, ``h-1`` refers to a
non-existing element for the first element in the planning interval,
completely in accordance with the default semantics of lag and lead
operators. In the fourth assignment, ``h-1`` refers to the last element
of the planning interval.

.. rubric:: Data transfer on entire domain

Operations which can be applied to identifiers without references to
their indices (such as the ``READ``, ``WRITE`` or ``DISPLAY``
statements), operate on the entire horizon domain. Thus, for example,
during data transfer with a database, AIMMS will retrieve or store the
data for *all* periods in the horizon, and not just for the periods in
the planning interval.