.. _sec:time.timetable:

Creating Timetables
===================

.. _timetable:

.. rubric:: Timetables

A *timetable* in AIMMS is an indexed set, which, for every period in a
``Horizon``, lists the corresponding time slots in the associated
``Calendar``. Timetables play a central role during the conversion from
calendar data to horizon data and vice versa.

.. _createtimetable-LR:

.. rubric:: The procedure :any:`CreateTimeTable`

Through the predefined procedure :any:`CreateTimeTable`, you can request
AIMMS to flexibly construct a *timetable* on the basis of

-  a *time slot* in the calendar and a *period* in the horizon that
   should be aligned at the beginning of the planning interval,

-  the desired *length* of each period in the horizon expressed as a
   number of time slots in the calendar,

-  an indication, for every period in the horizon, whether the *length
   dominates* over any specified delimiter slots,

-  a set of *inactive time slots*, which should be excluded from the
   timetable and, consequently, from the period length computation, and

-  a set of *delimiter time slots*, at which new horizon periods should
   begin.

.. rubric:: Syntax

The syntax of the procedure :any:`CreateTimeTable` is as follows:

-  :any:`CreateTimeTable`\ (*timetable*, *current-timeslot*,
   *current-period*, *period-length*, *length-dominates*,
   *inactive-slots*, *delimiter-slots*)

The (output) *timetable* argument of the procedure :any:`CreateTimeTable`
must, in general, be an indexed set in a calendar and defined over the
horizon to be linked to the calendar. Its contents is completely
determined by AIMMS on the basis of the other arguments. The
*current-timeslot* and *current-period* arguments must be elements of
the appropriate calendar and horizon, respectively.

.. rubric:: Element parameter as timetable

In the special case that you know a priori that each period in the
timetable is associated with exactly one time slot in the calendar,
AIMMS also allows the *timetable* argument of the :any:`CreateTimeTable`
procedure to be an element parameter (instead of an indexed set). When
you specify an element parameter, however, a runtime error will result
if the input arguments of the call to :any:`CreateTimeTable` give rise to
periods consisting of multiple time slots.

.. rubric:: Several possibilities

You have several possibilities of specifying your input data which
influence the way in which the timetable is created. You can:

-  only specify the length of each period to be created,

-  only specify delimiter slots at which a new period must begin, or

-  flexibly combine both of the above two methods.

.. rubric:: Period length

The *period-length* argument must be a positive integer-valued
one-dimensional parameter defined over the horizon. It specifies the
desired length of each period in the horizon in terms of the number of
time slots to be contained in it. If you do not provide delimiter slots
(explained below), AIMMS will create a timetable solely on the basis of
the indicated period lengths.

.. rubric:: Inactive slots

The *inactive-slots* argument must be a subset of the calendar that is
specified as the range of the *timetable* argument. Through this
argument you can specify a set of time slots that are always to be
excluded from the timetable. You can use this argument, for instance, to
indicate that weekend days or holidays are not to be part of a planning
period. Inactive time slots are excluded from the timetable, and are not
accounted for in the computation of the desired period length.

.. rubric:: Delimiter slots

The *delimiter-slots* argument must be a subset of the calendar that is
specified as the range of the *timetable* argument. AIMMS will begin a
new period in the horizon whenever it encounters a delimiter slot in the
calendar provided no (offending) period length has been specified for
the period that is terminated at the delimiter slot.

.. rubric:: Combining period length and delimiters

In addition to using either of the above methods to create a timetable,
you can also combine them to create timetables in an even more flexible
manner by specifying the *length-dominates* argument, which must be a
one-dimensional parameter defined over the horizon. The following rules
apply.

-  If the *length-dominates* argument is nonzero for a particular
   period, meeting the specified period length prevails over any
   delimiter slots that are possibly contained in that period.

-  If the *length-dominates* argument is zero for a particular period
   and the specified period length is 0, AIMMS will not restrict that
   period on the basis of length, but only on the basis of delimiter
   slots.

-  If the *length-dominates* argument is zero for a particular period
   and the specified period length is positive, AIMMS will try to
   construct a period of the indicated length, but will terminate the
   period earlier if it encounters a delimiter slot first.

.. rubric:: Timetable creation

In creating a timetable, AIMMS will always start by aligning the
*current-timeslot* argument with the beginning of the *current-period*.
Periods beyond *current-period* are determined sequentially by moving
forward time slot by time slot, until a new period must be started due
to hitting the period length criterion of the current period (taking
into account the inactive slots), or by hitting a delimiter slot.
Periods prior to *current-period* are determined sequentially by moving
backwards in time starting at *current-timeslot*.

.. rubric:: Adapting timetables

As a timetable is nothing more than an indexed set, you still have the
opportunity to make manual changes to a timetable after its contents
have been computed by the AIMMS procedure :any:`CreateTimeTable`. This
allows you to make any change to the timetable that you cannot, or do
not want to, implement directly using the procedure :any:`CreateTimeTable`.

.. rubric:: Example

Consider a timetable which links the daily calendar declared in
:ref:`sec:time.calendar` and the horizon of :ref:`sec:time.horizon`,
which consists of 10 periods named ``p-01`` ...\ ``p-10``. The following
conditions should be met:

-  the planning interval starts at period ``p-02``, i.e. period ``p-01``
   is in the past,

-  periods ``p-01``\ ...\ ``p-05`` have a fixed length of 1 day,

-  periods ``p-06``\ ...\ ``p-10`` should have a length of at most a week,
   with new periods starting on every Monday.

To create the corresponding timetable using the procedure
:any:`CreateTimeTable`, the following additional identifiers need to be
added to the model:

-  an indexed subset ``TimeTable(h)`` of ``DailyCalendar``,

-  a subset ``DelimiterDays`` of ``DailyCalendar`` containing all
   Mondays in the calendar (i.e. ``'01-01-96'``, ``'08-01-96'``, etc.),

-  a subset ``InactiveDays`` of ``DailyCalendar`` containing all days
   that you want to exclude from the timetable (e.g. all weekend days),

-  a parameter ``PeriodLength(h)`` assuming the value 1 for the periods
   ``p-01`` ... ``p-05``, and zero otherwise,

-  a parameter ``LengthDominates(h)`` assuming the value 1 for the
   periods ``p-01`` ... ``p-05``, and zero otherwise.

To compute the contents of the timetable, aligning the time slot pointed
at by ``CurrentDay`` and period ``IntervalStart``, one should call

.. code-block:: aimms

	CreateTimeTable( TimeTable, CurrentDay, IntervalStart,
	                 PeriodLength, LengthDominates,
	                 InactiveDays, DelimiterDays );

If all weekend days are inactive, and ``CurrentDay`` equals
``'24/01/96'`` (a Wednesday), then ``TimeTable`` describes the following
mapping.

.. table:: 

	======== ================== ======== =================================
	Period   Calendar slots                 
	Period   Calendar slots                 
	``p-01`` ``23/01/96`` (Tue) ``p-06`` ``30/01/96 - 02/02/96`` (Tue-Fri)
	``p-02`` ``24/01/96`` (Wed) ``p-07`` ``05/01/96 - 09/02/96`` (Mon-Fri)
	``p-03`` ``25/01/96`` (Thu) ``p-08`` ``12/01/96 - 16/02/96`` (Mon-Fri)
	``p-04`` ``26/01/96`` (Fri) ``p-09`` ``19/01/96 - 23/02/96`` (Mon-Fri)
	``p-05`` ``29/01/96`` (Mon) ``p-10`` ``26/01/96 - 01/03/96`` (Mon-Fri)
	======== ================== ======== =================================
	
.. _timeslotcharacteristic-LR:

.. rubric:: The function ``TimeslotCharacteristic``

The process of initializing the sets used in the *delimiter-slots* and
*inactive-slots* arguments can be quite cumbersome when your model
covers a large time span. For that reason AIMMS offers the convenient
function ``TimeslotCharacteristic``. With it, you can obtain a numeric
value which characterizes the time slot, in terms of its day of the
week, its day in the year, etc. The syntax of the function is
straightforward:

-  ``TimeslotCharacteristic``\ (*timeslot*, *characteristic*\ [,
   *timezone*\ [, ignoredst]])

The *characteristic* argument must be an element of the predefined set
``TimeslotCharacteristics``. The elements of this set, as well as the
associated function values are listed in :ref:`this table <table:time.time-char>`.

.. _table:time.time-char:

.. table:: 

	+-----------------------+-----------------------+-----------------------+
	| Characteristic        | Function value range  | First                 |
	+=======================+=======================+=======================+
	| ``century``           | 0, ..., 99            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``year``              | 0, ..., 99            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``quarter``           | 1, ..., 4             |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``month``             | 1, ..., 12            |    January            |
	+-----------------------+-----------------------+-----------------------+
	| ``weekday``           | 1, ..., 7             |    Monday             |
	+-----------------------+-----------------------+-----------------------+
	| ``yearday``           | 1, ..., 366           |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``monthday``          | 1, ..., 31            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``week``              | 1, ..., 53            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``weekyear``          | 0, ..., 99            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``weekcentury``       | 0, ..., 99            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``hour``              | 0, ..., 23            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``minute``            | 0, ..., 59            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``second``            | 0, ..., 59            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``tick``              | 0, ..., 99            |                       |
	+-----------------------+-----------------------+-----------------------+
	| ``dst``               | 0, 1                  |                       |
	+-----------------------+-----------------------+-----------------------+
	
.. rubric:: Day and week numbering
   :name: time:weeknumbering

Internally, AIMMS takes Monday as the first day in a week, and considers
week 1 as the first week that contains at least four days of the new
year. This is equivalent to stating that week 1 contains the first
Thursday of the new year. Through the ``'week'``, ``'weekyear'`` and
``'weekcentury'`` characteristics you obtain the week number
corresponding to a particular date and its corresponding year and
century. For instance, Friday January 1, 1999 is day 5 of week 53 of
year 1998.

.. rubric:: Example

Consider a daily calendar ``DailyCalendar`` with index ``d``. The
following assignment to a subset ``WorkingDays`` of a ``DailyCalendar``
will select all non-weekend days in the calendar.

.. code-block:: aimms

	WorkingDays := { d | TimeslotCharacteristic(d,'weekday') <= 5 } ;

.. rubric:: Calendar-calendar linkage

You can also use the function ``TimeslotCharacteristic`` to create a
timetable linking two calendars (e.g. to create monthly overviews of
daily data). As an example, consider the calendars ``DailyCalendar`` and
``MonthlyCalendar`` declared in :ref:`sec:time.calendar`, as well as an
indexed set ``MonthDays(m)`` of ``DailyCalendar``, which can serve as a
timetable. ``MonthDays`` can be computed as follows.

.. code-block:: aimms

	MonthDays(m) := { d | TimeslotCharacteristic(d,'year') =
	                            TimeslotCharacteristic(m,'year') and
	                      TimeslotCharacteristic(d,'month') =
	                            TimeslotCharacteristic(m,'month')    };

A check on the ``'year'`` characteristic is not necessary if both
calendars are contained within a single calendar year.

.. rubric:: Time zone support

Through the optional *timezone* argument of the function
``TimeslotCharacteristic``, you can specify with respect to which time
zone you want to obtain the specified characteristic. The *timezone*
argument must be an element of the predefined set :any:`AllTimeZones` (see
also :ref:`sec:time.format.dst`). By default, AIMMS assumes the local
time zone without daylight saving time.

.. rubric:: Daylight saving time

When you specify a time zone with daylight saving time, you can retrieve
whether daylight saving time is active through the ``'dst'``
characteristic. With the optional argument *ignoredst* (default 0) of
the function :any:`TimeSlotCharacteristic`, you can specify whether you
want daylight saving time to be ignored. With *ignoredst* set to 1, or
in a time zone without daylight saving time, the outcome for the
``'dst'`` characteristic will always be 0.