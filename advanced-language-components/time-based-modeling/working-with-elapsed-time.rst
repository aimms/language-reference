.. _sec:time.continuous:

Working with Elapsed Time
=========================

.. rubric:: Use of elapsed time

Sometimes you may find it easier to formulate your model in terms of
(continuous) elapsed time with respect to some reference date rather
than in terms of discrete time periods. For example, for a task in a
schedule it is often more natural to store just the start and end time
rather than to specify all of the time slots in a calendar during which
the task will be executed. In addition, working with elapsed time allows
you to store time references to any desired accuracy.

.. rubric:: Input-output conversion

For data entry or for the generation of reports, however, elapsed time
may not be your preferred format. In this event AIMMS offers a number of
functions for the conversion of elapsed time to calendar strings (or set
elements) and vice versa, using the conversion specifiers described in
:ref:`sec:time.format`.

.. rubric:: Conversion to calendar elements

The following functions allow conversion between elapsed time and time
slots in an existing calendar. Their syntax is

-  :any:`MomentToTimeSlot`\ (*calendar, reference-date, elapsed-time*)

-  :any:`TimeSlotToMoment`\ (*calendar, reference-date, time-slot*).

The *reference-date* argument must be a time slot in the specified
calendar. The *elapsed-time* argument is the elapsed time from the
*reference-date* measured in terms of the calendar's unit. The result of
the function :any:`MomentToTimeSlot` is the time slot containing the moment
represented by the reference date plus the elapsed time. The result of
the function :any:`TimeSlotToMoment` is the elapsed time from the reference
date to the value of the *time-slot* argument (measured in the
calendar's unit).

.. rubric:: Conversion to calendar strings

The following functions enable conversion between elapsed time and free
format strings. Their syntax is

-  :any:`MomentToString`\ (*format-string, unit, reference-date,
   elapsed-time*)

-  :any:`StringToMoment`\ (*format-string, unit, reference-date,
   moment-string*).

The *reference-date* argument must be provided in the fixed format for
reference dates, as described in :ref:`sec:time.calendar`. The
*moment-string* argument must be a period in the format given by
*format-string*. The *elapsed-time* argument is the elapsed time in
*unit* with respect to the *reference-date* argument. The result of the
function :any:`MomentToString` is a description of the corresponding moment
according to *format-string*. Strictly spoken, the *unit* argument in
:any:`MomentToString` is only required when the option
``elapsed_time_is_unitless`` (see below) is set to ``on``, and,
consequently, *elapsed-time* is unitless. In the case that
``elapsed_time_is_unitless`` is set to ``off`` (the default), you are
advised to set the *unit* argument equal to the associated unit of the
*elapsed-time* argument. The result of the function :any:`StringToMoment`
is the elapsed time in *unit* between *reference-date* and
*moment-string*.

.. rubric:: Example

.. code-block:: aimms

	moment := MomentToString("%c%y-%Am|AllAbbrMonths|-%d (%sAw|AllWeekdays|) %H:%M",
	                         [hour], "1996-01-01 14:00", 2.2 [hour] );
	          ! result : "1996-Jan-01 (Monday) 16:12"

	elapsed := StringToMoment("%c%y-%Am|AllAbbrMonths|-%d (%sAw|AllWeekdays|) %H:%M",
	                          [hour], "1996-01-01 14:00", "1996-Jan-01 (Monday) 16:12" );
	          ! result : 2.2 [hour]

.. rubric:: Obtaining the current time

The function :any:`CurrentToMoment` can be used to obtain the elapsed time
since *reference-date* in the specified *unit* of the current time. Its
syntax is

-  :any:`CurrentToMoment`\ (*unit*, *reference-date*).

.. rubric:: Unitless result

By default, the result of the functions :any:`TimeSlotToMoment`,
:any:`StringToMoment` and :any:`CurrentToMoment` will have an associated unit,
namely the unit specified in the *unit* argument. In addition, AIMMS
expects the *elapsed-time* argument in the function :any:`MomentToTimeSlot`
and :any:`MomentToString` to be of the same unit as its associated *unit*
argument. If you want the result or arguments of these functions to be
unitless, you can accomplish this by setting the compile time option
``elapsed_time_is_unitless`` to ``on``. Note, however, that any change
to this option affects all calls to these function throughout your
model.