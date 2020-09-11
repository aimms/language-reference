.. _sec:time.convert:

Converting Time Slots and Periods to Strings
============================================

.. rubric:: Converting time slots to strings

The following functions enable conversion between calendar slots and
free format strings using the conversion specifiers discussed in the
previous section. Their syntax is

-  :any:`TimeSlotToString`\ (*format-string, calendar, time-slot*)

-  :any:`StringToTimeSlot`\ (*format-string, calendar, moment-string*).

The result of the function :any:`TimeSlotToString` is a description of the
specified *time-slot* according to *format-string*. The result of
:any:`StringToTimeSlot` is the time slot in *calendar* in which the string
*moment-string*, specified according to *format-string*, is contained.

.. rubric:: Converting timetable periods to strings

With the function :any:`PeriodToString` you can obtain a description of a
period in a timetable that consists of multiple calendar slots.

-  :any:`PeriodToString`\ (*format-string, timetable, period*)

The result of the function is a description of the time span covered by
a *period* in a horizon according to the specified *timetable* and
*format-string*. The *format-string* argument can use period-specific
conversion specifiers to generate a description referring to both the
beginning and end of the period.

.. rubric:: Obtaining the current time

The functions :any:`CurrentToString` and :any:`CurrentToTimeSlot` can be used
to obtain the current time. Their syntax is

-  :any:`CurrentToString`\ (*format-string*)

-  :any:`CurrentToTimeSlot`\ (*calendar*)

The function :any:`CurrentToString` will return the current time according
to the specified format string. If you do not use the ``%TZ`` specifier
in the format string of the :any:`CurrentToString` function, AIMMS assumes
daylight saving time by default. You can change this default behavior by
setting the global option ``current_time_in_LocalDST`` to 0. The
function :any:`CurrentToTimeSlot` returns the time slot in *calendar*
containing the current moment.