.. _sec:time.conversion:

Data Conversion of Time-Dependent Identifiers
=============================================

.. rubric:: Time-dependent data

When you are working with time-dependent data, it is usually not
sufficient to provide and work with a single fixed-time scale. The
following examples serve as an illustration.

-  Demand data is available in a database on a day-by-day basis, but is
   needed in a mathematical program for each horizon period.

-  Production quantities are computed per horizon period, but are needed
   on a day-by-day basis.

-  For all of the above data weekly or monthly overviews are also
   required.

.. _aggregate-LR:

.. _disaggregate-LR:

.. rubric:: The procedures :any:`Aggregate` and ``Disaggregate``

With the procedures :any:`Aggregate` and ``Disaggregate`` you can instruct
AIMMS to perform an aggregation or disaggregation step from one time
scale to another. Both procedures perform the aggregation or
disaggregation of a single identifier in one time scale to another
identifier in a second time scale, given a timetable linking both time
scales and a predefined aggregation type. The syntax is as follows.

-  :any:`Aggregate`\ (*timeslot-data*, *period-data*, *timetable*,
   *type*\ [, *locus*])

-  ``Disaggregate``\ (*period-data*, *timeslot-data*, *timetable*,
   *type*\ [, *locus*])

.. rubric:: Time slot and period data

The identifiers (or identifier slices) passed to the :any:`Aggregate` and
``Disaggregate`` procedures holding the time-dependent data must be of
equal dimension. All domain sets in the index domains must coincide,
except for the time domains. These must be consistent with the domain
and range of the specified timetable.

.. rubric:: Different conversions

As was mentioned in :ref:`sec:time.intro`, time-dependent data can be
interpreted as taking place *during* a period or *at a given moment* in
the period. Calendar data, which takes place *during* a period, needs to
be converted into a period-based representation by allocating the data
values in proportion to the overlap between time slots and horizon
periods. On the other hand, calendar data which takes place *at a given
moment*, needs to be converted to a period-based representation by
linearly interpolating the original data values.

.. _conversion:

.. rubric:: Aggregation types

The possible values for the *type* argument of the :any:`Aggregate` and
``Disaggregate`` procedures are the elements of the predefined set
:any:`AggregationTypes` given by:

-  ``summation``,

-  ``average``,

-  ``maximum``,

-  ``minimum``, and

-  ``interpolation``.

.. rubric:: Reverse conversion

All of the above predefined conversion rules are characterized by the
following property.

   The disaggregation of period data into time slot data, followed by
   immediate aggregation, will reproduce identical values of the period
   data.

Aggregation followed by disaggregation does not have this property.
Fortunately, as the horizon rolls along, disaggregation followed by
aggregation is the essential conversion.

.. rubric:: The ``summation`` rule

The conversion rule ``summation`` is the most commonly used
aggregation/disaggregation rule for quantities that take place *during*
a period. It is appropriate for such typical quantities as production
and arrivals. Data values from a number of consecutive time slots in the
calendar are summed together to form a single value for a multi-unit
period in the horizon. The reverse conversion takes place by dividing
the single value equally between the consecutive time slots.

.. rubric:: The ``average``, ``maximum``, and ``minimum`` rules

The conversion rules ``average``, ``maximum``, and ``minimum`` are less
frequently used aggregation/disaggregation rules for quantities that
take place *during* a period. These rules are appropriate for such
typical quantities as temperature or capacity. Aggregation of data from
a number of consecutive time slots to a single period in the horizon
takes place by considering the average or the maximum or minimum value
over all time slots contained in the period. The reverse conversion
consists of assigning the single value to each time slot contained in
the period.

.. rubric:: Illustration of aggregation

:numref:`table:time.conv-during` demonstrates the aggregation and
disaggregation taking place for each conversion rule. The conversion
operates on a single period consisting of 3 time slots in the calendar.

.. _table:time.conv-during:

.. table:: Conversion rules for "during" quantities

   +---------------------+--------------------------+--------------------------+
   | **Conversion rule** | **Calendar to horizon**  | **Horizon to calendar**  |
   |                     +--------+--------+--------+--------------------------+
   |                     | 3      | 1      | 2      | 3                        |
   +=====================+========+========+========+========+========+========+
   | ``summation``       | 6                        | 1      | 1      | 1      |
   +---------------------+--------------------------+--------+--------+--------+
   | ``average``         | 2                        | 3      | 3      | 3      |
   +---------------------+--------------------------+--------+--------+--------+
   | ``maximum``         | 3                        | 3      | 3      | 3      |
   +---------------------+--------------------------+--------+--------+--------+
   | ``minimum``         | 1                        | 3      | 3      | 3      |
   +---------------------+--------------------------+--------+--------+--------+

.. rubric:: Interpolation

The ``interpolation`` rule should be used for all quantities that take
place *at a given moment* in a period. For the ``interpolation`` rule
you have to specify one additional argument in the :any:`Aggregate` and
``Disaggregate`` procedures, the *locus*. The *locus* of the
``interpolation`` defines at which moment in a period-as a value between
0 and 1-the quantity at hand is to be measured. Thus, a *locus* of 0
means that the quantity is measured at the beginning of every period, a
*locus* of 1 means that the quantity is measured at the end of every
period, while a *locus* of 0.5 means that the quantity is measured
midway through the period.

.. rubric:: Interpolation for disaggregation

When disaggregating data from periods to time slots, AIMMS interpolates
linearly between the respective loci of two subsequent periods. For the
outermost periods, AIMMS assigns the last available interpolated value.

.. rubric:: Interpolation for aggregation

AIMMS applies a simple rule for the seemingly awkward interpolation of
data from unit-length time slots to variable-length horizon periods. It
will simply take the value associated with the time slot in which the
``locus`` is contained, and assign it to the period. This simple rule
works well for loci of 0 and 1, which are the most common values.

.. rubric:: Illustration of interpolation

:numref:`table:time.conv-interpol` demonstrates aggregation and
disaggregation of a horizon of 3 periods, each consisting of 3 time
slots, for loci of 0, 1, and 0.5. The underlined values are the values
determined by the reverse conversion.

.. _table:time.conv-interpol:

.. table:: Conversion rules for interpolated data

	+-----------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| **Locus** | **Horizon data**                                                                                                                                                                                                      |
	|           +-----------------------------------------------------------------------+-----------------------------------------------------------------------+-----------------------------------------------------------------------+
	|           | 0                                                                     | 3                                                                     | 9                                                                     |
	+===========+=======================+=======================+=======================+=======================+=======================+=======================+=======================+=======================+=======================+
	| 0         | :math:`\underline{0}` | 1                     | 2                     | :math:`\underline{3}` | 5                     | 7                     | :math:`\underline{9}` | 9                     | 9                     |
	+-----------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+
	| 1         | 0                     | 0                     | :math:`\underline{0}` | 1                     | 2                     | :math:`\underline{3}` | 5                     | 7                     | :math:`\underline{9}` |
	+-----------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+
	| 0.5       | 0                     | :math:`\underline{0}` | 1                     | 2                     | :math:`\underline{3}` | 5                     | 7                     | :math:`\underline{9}` | 9                     |
	+-----------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+-----------------------+

.. rubric:: Example

Consider the calendar ``DailyCalendar``, the horizon ``ModelPeriods``
and the timetable ``TimeTable`` declared in :ref:`sec:time.calendar`,
:ref:`sec:time.horizon` and :ref:`sec:time.timetable`, along with the
identifiers

-  ``DailyDemand(d)``,

-  ``Demand(h)``,

-  ``DailyStock(d)``, and

-  ``Stock(h)``.

The aggregation of ``DailyDemand`` to ``Demand`` can then be
accomplished by the statement

.. code-block:: aimms

	Aggregate( DailyDemand, Demand, TimeTable, 'summation' );

Assuming that the ``Stock`` is computed at the end of each period, the
disaggregation (by interpolation) to daily values is accomplished by the
statement

.. code-block:: aimms

	Disaggregate( Stock, DailyStock, TimeTable, 'interpolation', locus: 1 );

.. rubric:: User-defined conversions

If your particular aggregation/disaggregation scheme is not covered by
the predefined aggregation types available in AIMMS, it is usually not
too difficult to implement a custom aggregation scheme yourself in
AIMMS. For instance, the aggregation by summation from ``DailyDemand``
to ``Demand`` can be implemented as

.. code-block:: aimms

	Demand(h) := sum( d in TimeTable(h), DailyDemand(d) );

while the associated disaggregation rule becomes the statement

.. code-block:: aimms

	DailyDemand(d) := sum( h | d in TimeTable(h), Demand(h)/Card(TimeTable(per)) );