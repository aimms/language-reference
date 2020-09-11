.. _sec:time.format:

Format of Time Slots and Periods
================================

.. _timeslot-format:

.. rubric:: Flexible time slot and period formats

While the ``BeginDate`` and ``EndDate`` attributes have to be specified
using the fixed *reference date* format (see :ref:`sec:time.calendar`),
AIMMS provides much more flexible formatting capabilities to describe

-  time slots in a ``Calendar`` consisting of a single basic time unit
   (e.g. 1-day time slots),

-  time slots in a ``Calendar`` consisting of multiple basic time units
   (e.g. 3-day time slots), and

-  periods in a timetable consisting of multiple time slots.

The formatting capabilities described in this section are quite
extensive, and allow for maximum flexibility.

.. rubric:: Wizard support

In the Model Explorer, AIMMS provides a wizard to support you in
constructing the appropriate formats. Through this wizard, you can not
only select from a number of predefined formats (including some that use
the regional settings of your computer), you also have the possibility
of constructing a custom format, observing the result as you proceed.

.. rubric:: Basic and extended format

AIMMS offers both a *basic* and an *extended format* for the description
of time slots and periods. The basic format only refers to the beginning
of a time slot or period. The extended format allows you to refer to
both the first and last basic time unit contained in a time slot or
period. Both the basic and extended formats are constructed according to
the same rules.

.. rubric:: Care is needed

The ``TimeslotFormat`` used in a ``Calendar`` must contain a reference
to either its beginning, its end, or both. As the specified format is
used to identify calendar elements when reading data from external data
sources such as files and databases, you have to ensure that the
specified format contains sufficient date and time references to
uniquely identify each time slot in a calendar.

.. rubric:: Example

For instance, the description ``January 1`` is sufficient to uniquely
identify a time slot in a calendar with a range of one year. However, in
a two-year calendar, corresponding days in the first and second year are
identified using exactly the same element description. In such a case,
you must make sure that the specified format contains a reference to a
year.

.. rubric:: Building blocks

A format description is a sequence of four types of components. These
are

-  predefined date components,

-  predefined time components,

-  predefined period references (extended format), and

-  ordinary characters.

.. rubric:: Ordinary characters

Predefined components begin with the ``%`` sign. Components that begin
otherwise are interpreted as ordinary characters. To use a percent sign
as an ordinary character, escape it with another percent sign, as in
``%%``.

.. _sec:time.format.date:

Date-specific Components
------------------------

.. rubric:: Date-specific components

The date-specific components act as conversion specifiers to denote
portions of a date description. They may seem rather cryptic at first,
but you will find them useful and constructive when creating customized
references to time. They are summarized in
:numref:`table:time.cal-date`.

.. _table:time.cal-date:

.. table:: Conversion specifiers for date components

   ================================= ============ =====================
   Conversion specifier              Meaning      Possible entries
   ================================= ============ =====================
   ``%d``                            day          :math:`01,\dots,31`
   ``%m``                            month        :math:`01,\dots,12`
   ``%Am|``\ *set-identifier*\ ``|`` month        *element*
   ``%y``                            year         :math:`00,\dots,99`
   ``%q``                            quarter      :math:`01,\dots,04`
   ``%Y``                            weekyear     :math:`00,\dots,99`
   ``%c``                            century      :math:`00,\dots,99`
   ``%C``                            weekcentury  :math:`00,\dots,99`
   ``%w``                            day of week  :math:`1,\dots,7`
   ``%Aw|``\ *set-identifier*\ ``|`` day of week  *element*
   ``%W``                            week of year :math:`01,\dots, 53`
   ``%j``                            day of year  :math:`001,\dots,366`
   ================================= ============ =====================

.. rubric:: Custom date-specific references

All date conversion specifiers allow only predefined numerical values,
except for the specifiers ``%Am`` and ``%Aw``. These allow you to
specify references to sets. You can use ``%Am`` and ``%Aw`` to denote
months and days by the elements in a specified set. These are typically
the names of the months or days in your native language. AIMMS will
interpret the elements by their ordinal number. The predefined
identifiers :any:`AllMonths`, :any:`AllAbbrMonths`, :any:`AllWeekdays` and
:any:`AllAbbrWeekdays` hold the full and abbreviated English names of both
months and days.

.. rubric:: Week year and century

The ``%Y`` and ``%C`` specifiers refer to the weekyear and weekcentury
values of a specific date, as explained on page
:ref:`time:weeknumbering`. You can use these if you want to refer to
weekly calendar periods by their week number and year.

.. rubric:: Omitting leading zeros

AIMMS can interpret numerical date-specific references with or without
leading zeros when reading your input data. When writing data, AIMMS
will insert all leading zeros to ensure a uniform length for date
elements. If you do not want leading zeros for a specific component, you
can insert the '\ ``s``\ ' modifier directly after the ``%`` sign. For
instance, the string ``%sd`` will direct AIMMS to produce single-digit
numbers for the first nine days.

.. rubric:: Omitting trailing blanks

When using the ``%Am`` and ``%Aw`` specifiers, AIMMS will generate
uniform length elements by adding sufficient trailing blanks to the
shorter elements. As with leading zeros, you can use the ``s`` modifier
to override the generation of these trailing blanks.

.. rubric:: Example

The format ``%Am|AllMonths| %sd, %c%y`` will result in the generation
of time slots such as ``'January 1, 1996'``. The date portion of the
fixed reference date format used to specify the ``Begin`` and
``EndDate`` attributes of a calendar can be reproduced using the format
``%c%y-%m-%d``.

.. _sec:time.format.time:

Time-specific Components
------------------------

.. rubric:: Time-specific components

The conversion specifiers for time components are listed in
:numref:`table:time.cal-time`. There are no custom time-specific
references in this table, because the predefined numerical values are
standard throughout the world.

.. _table:time.cal-time:

.. table:: Conversion specifiers for time components

   ==================== ==================== ===================
   Conversion specifier Meaning              Possible entries
   ==================== ==================== ===================
   ``%h``               hour                 :math:`01,\dots,12`
   ``%H``               hour                 :math:`00,\dots,23`
   ``%M``               minute               :math:`00,\dots,59`
   ``%S``               second               :math:`00,\dots,59`
   ``%t``               tick                 :math:`00,\dots,99`
   ``%p``               before or after noon AM, PM
   ==================== ==================== ===================

.. rubric:: Omitting leading zeros

AIMMS can interpret numerical time-specific references with or without
leading zeros when reading your input data. When writing data, AIMMS
will insert leading zeros to ensure a uniform length for time elements.
If you do not want leading zeros for a specific component, you can
insert the '\ ``s``\ ' modifier directly after the ``%`` sign. For
instance, the string ``%sh`` will direct AIMMS to produce single-digit
numbers for the first nine hours.

.. rubric:: Example

The time slot format ``%sAw|WeekDays| %sh:%M %p`` will result in the
generation of time slots such as ``'Friday 11:00 PM'``,
``'Friday 12:00 PM'`` and ``'Saturday 1:00 AM'``. The full reference
date format is given by ``%c%y-%m-%d %H:%M:%S``.

.. _sec:time.format.period:

Period-specific Components
--------------------------

.. rubric:: Use of period references

With period-specific conversion specifiers in either a time slot format
or a period format you can indicate that you want AIMMS to display both
the begin and end date/time of a time slot or period. You only need to
use period-specific references in the following cases.

-  The :any:`Unit` attribute of your calendar consists of a multiple of one
   of the basic time units known to AIMMS (e.g. each time slot in your
   calendar consists of 3 days), and you want to refer to the begin and
   end day of every time slot.

-  You want to provide a description for a period in a timetable
   consisting of multiple time slots in the associated calendar using
   the function :any:`PeriodToString` (see also :ref:`sec:time.convert`),
   referring to both the first and last time slot in the period.

.. rubric:: Period-specific components

By including a period-specific component in a time slot or period
format, you indicate to AIMMS that any date, or time, specific component
following it refers to either the beginning or the end of a time slot or
period. The list of available period-specific conversion specifiers is
given in :numref:`table:time.cal-per-ref`.

.. _table:time.cal-per-ref:

.. table:: Period-specific conversion specifiers.

   +----------------------+----------------------------------------------------------------------+
   | Conversion specifier | Meaning                                                              |
   +======================+======================================================================+
   | ``%B``               | begin of unit period                                                 |
   +----------------------+----------------------------------------------------------------------+
   | ``%b``               | begin of time slot                                                   |
   +----------------------+----------------------------------------------------------------------+
   | ``%I``               | end of period (inclusive)                                            |
   +----------------------+----------------------------------------------------------------------+
   | ``%i``               | end of period (inclusive), but omitted when equal to begin of period |
   +----------------------+----------------------------------------------------------------------+
   | ``%E``               | end of period (exclusive)                                            |
   +----------------------+----------------------------------------------------------------------+
   | ``%e``               | end of time slot                                                     |
   +----------------------+----------------------------------------------------------------------+

.. rubric:: Inclusive or exclusive

Through the ``%I`` and ``%E`` specifiers you can indicate whether
you want any date/ time components used in the description of the end of
a period (or time slot) to be included in that period or excluded from
it. Inclusive behavior is common for date references, e.g. the
description "Monday - Wednesday" usually means the period consisting of
Monday, Tuesday *and* Wednesday. For time references exclusive behavior
is used most commonly, i.e. "1:00 - 3:00 PM" usually means the period
from 1:00 PM *until* 3:00 PM.

.. rubric:: Limited resolution

After a conversion specifier that refers to the end of a period or time
slot (i.e. ``%E``, ``%I`` or ``%i``) you should take care when
using other date, or time, specific specifiers. AIMMS will only be able
to discern time units that are larger than the basic time unit specified
in the :any:`Unit` attribute of the calendar at hand (or, when you use the
function :any:`PeriodToString`, of the calendar associated with the
timetable at hand). For instance, when the time slots of a calendar
consists of periods of 2 months, AIMMS will be able to distinguish the
specific months at the beginning and end of each time slot, but will not
know the specific week number, week day or month day at the end of each
time slot. Thus, in this case you should avoid the use of the ``%W``,
the ``%w`` and the ``%d`` specifiers after a ``%E``, ``%I`` or
``%i`` specifier.

.. rubric:: The ``%i`` specifier

With the ``%i`` specifier you indicate inclusive behavior, and
additionally you indicate that AIMMS must omit the remaining text when
the basic time units (w.r.t. the underlying calendar) of begin and end
slot of the period to which the specifier is applied, coincide. In
practice, the ``%i`` specifier only makes sense when used in the
function :any:`PeriodToString` (see also :ref:`sec:time.convert`), as time
slots in a calendar always have a fixed length.

.. rubric:: First example

The period description ``Monday 12:00-15:00`` contains three logical
references, namely to a day, to the begin time in hours, and to the end
time in hours. The day reference is intended to be shared by the begin
and end times.

-  The day reference is based on the elements of the (predefined) set
   :any:`AllWeekdays`. The corresponding conversion specifier is
   ``%Aw|AllWeekDays|``

-  The descriptions of the begin and end times both use the conversion
   specifier ``%H:%M``. To denote the begin time of the period you
   must use the ``%B`` period reference. For the end time of the
   period, which is not included in the period, you must use ``%E``.

By combining these building blocks with a few ordinary characters you
get the complete format string ``%Aw|AllWeekDays| %B%H:%M-%E%H:%M``.
With this string AIMMS can correctly interpret the element
``Monday 12:00-15:00`` within a calendar covering no more than one
week.

.. rubric:: Second example

Consider the format "``%B%Aw|AllWeekDays|%I`` ``-``
``%Aw|AllWeekDays|``" within a calendar with ``day`` as its basic time
unit, and covering at most a week. Using this format string AIMMS will
interpret the element ``Monday - Wednesday`` as the three-day period
consisting of Monday, Tuesday, and Wednesday.

.. _sec:time.format.dst:

Support for Time Zones and Daylight Saving Time
-----------------------------------------------

.. rubric:: Support for daylight saving time

When your time zone has daylight saving time, and you are working with
time slots or periods on an hourly basis, you may want to include an
indicator into the time slot or period format to indicate whether
daylight saving time is active during a particular time slot or period.
Such an indicator enables you, for instance, to distinguish between the
duplicate hour when the clock is set back at the end of daylight saving
time.

.. rubric:: Support for time zones

In addition, when your application has users located in different time
zones, you may wish to present each user with calendar elements
corresponding to their particular time zone. Or, when time-dependent
data is stored in a database using UTC time (Universal Time Coordinate,
or Greenwich Mean Time), a translation may be required to your own local
time representation.

.. rubric:: AIMMS support

To support you in scenarios as described above, AIMMS provides

-  a special time zone conversion specifier, which can modify the
   representation of calendar elements based on specified time zone and
   daylight saving time, and

-  a ``TimeslotFormat`` attribute in unit ``Conventions`` (see also
   :ref:`sec:units.convention`), which you can use to override the time
   slot format of every calendar when the ``Convention`` is active.

.. rubric:: Time zone specifier

With the conversion specifier ``%TZ``, described in
:numref:`table:time.tz`, you can accomplish the following
``Calendar``-related tasks:

-  create the ``Calendar`` elements between the given ``BeginDate`` and
   ``EndDate`` relative to a specified time zone, and

-  specify the indicators that must be added to the ``Calendar``
   elements when standard or daylight saving time is active.

.. _table:time.tz:

.. table:: Time zone conversion specifier

   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Conversion specifier                                     | Meaning                                                                                                                                   |
   +==========================================================+===========================================================================================================================================+
   | ``%TZ(``\ *TimeZone*\ ``)``                              | translation of calendar element to specified *TimeZone*, ignoring daylight saving time                                                    |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | ``%TZ(``\ *TimeZone*\ ``)|``\ *Std*\ ``|``\ *Dst*\ ``|`` | translation of calendar element to specified *TimeZone*, plus string indicator for standard time (*Std*) and daylight saving time (*Dst*) |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

.. rubric:: Specifying the time zone

The *TimeZone* component of the ``%TZ`` conversion specifier that you
must specify, is a time zone corresponding to the elements in your
``Calendar``. You must specify the time zone as an explicit and quoted
element of the predefined set :any:`AllTimeZones` (explained below), or
through a reference to an element parameter into that set. If you do not
specify the *Std* and *Dst* indicators, AIMMS will ignore daylight
saving time when generating the time slots, regardless whether daylight
saving time is defined for that time zone. If you do not use the ``%TZ``
specifier to specify a time zone, AIMMS assumes that you intend to use
the local time zone without daylight saving time.

.. rubric:: The set :any:`AllTimeZones`

AIMMS provides you access to all time zones defined by your operating
system through the predefined set :any:`AllTimeZones`. The set
:any:`AllTimeZones` contains

-  the fixed element ``'Local'``, representing the local time zone
   without daylight saving time,

-  the fixed element ``'LocalDST'``, representing the local time zone
   with daylight saving time (if applicable),

-  the fixed element ``'UTC'``, representing the Universal Time
   Coordinate (or Greenwich Mean Time) time zone, and

-  all time zones defined by your operating system.

.. rubric:: Daylight saving time indicators

The remaining components of the ``%TZ`` specifier are two string
indicators *Std* and *Dst*, which are displayed in all generated
``Calendar`` slots or period strings when standard time (i.e. no
daylight saving time) or daylight saving time is active, respectively.
Both indicators must be either quoted strings, or references to scalar
string parameters. In addition, a run time error will occur when both
indicators evaluate to the same string.

.. rubric:: Effect on time slots

When you use the ``%TZ`` specifier, the date and time components of the
generated time slots of a calendar may differ when you specify different
time zones, but do not modify the reference dates specified in the
``BeginDate`` and ``EndDate`` attributes of the calendar. AIMMS always
assumes that reference dates are specified in local time without
daylight saving time (i.e. in the ``'Local'`` time zone). Hence, all
time slots will be shifted by the time differences between the specified
time zone and the ``'Local'`` time zone, plus any additional difference
caused by daylight saving time.

.. rubric:: Examples

Consider the following four ``Calendar`` declarations.

.. code-block:: aimms

	Calendar HourCalendarLocal {
	    Index           :  hl;
	    Unit            :  hour;
	    BeginDate       :  "2001-03-25 00";
	    EndDate         :  "2001-03-25 06";
	    TimeslotFormat  :  "%c%y-%m-%d %H:00";
	}
	Calendar HourCalendarLocalIgnore {
	    Index           :  hi;
	    Unit            :  hour;
	    BeginDate       :  "2001-03-25 00";
	    EndDate         :  "2001-03-25 06";
	    TimeslotFormat  :  "%c%y-%m-%d %H:00%TZ('LocalDST')";
	}
	Calendar HourCalendarLocalDST {
	    Index           :  hd;
	    Unit            :  hour;
	    BeginDate       :  "2001-03-25 00";
	    EndDate         :  "2001-03-25 06";
	    TimeslotFormat  :  "%c%y-%m-%d %H:00%TZ('LocalDST')|\"\"|\" DST\"|";
	}
	Calendar HourCalendarUTC {
	    Index           :  hc;
	    Unit            :  hour;
	    BeginDate       :  "2001-03-25 00";
	    EndDate         :  "2001-03-25 06";
	    TimeslotFormat  :  "%c%y-%m-%d %H:00%TZ('UTC')|\"\"|\" DST\"|";
	}

Assuming that the ``'Local'`` time zone has an offset of :math:`+1`
hours compared to the ``'UTC'`` time zone, this will result in the
generation of the following time slots for each of the calendars

.. code-block:: aimms

	!   HourCalendarLocal    HourCalendarIgnore   HourCalendarLocalDST     HourCalendarUTC
	!   ------------------   ------------------   ----------------------   ------------------
	    '2001-03-25 00:00'   '2001-03-25 00:00'   '2001-03-25 00:00'       '2001-03-24 23:00'
	    '2001-03-25 01:00'   '2001-03-25 01:00'   '2001-03-25 01:00'       '2001-03-25 00:00'
	    '2001-03-25 02:00'   '2001-03-25 02:00'   '2001-03-25 03:00 DST'   '2001-03-25 01:00'
	    '2001-03-25 03:00'   '2001-03-25 03:00'   '2001-03-25 04:00 DST'   '2001-03-25 02:00'
	    '2001-03-25 04:00'   '2001-03-25 04:00'   '2001-03-25 05:00 DST'   '2001-03-25 03:00'
	    '2001-03-25 05:00'   '2001-03-25 05:00'   '2001-03-25 06:00 DST'   '2001-03-25 04:00'
	    '2001-03-25 06:00'   '2001-03-25 06:00'   '2001-03-25 07:00 DST'   '2001-03-25 05:00'

Note that the time slots generated for ``HourCalendarLocal`` and
``HourCalendarIgnore`` are identical (although ``'LocalDST'`` supports
daylight saving time). This is because daylight saving time is ignored
when the ``%TZ`` specifier has no *Std* and *Dst* indicators. The time
slots generated for ``HourCalendarUTC`` do not contain the specified
daylight saving time indicator, because the ``'UTC'`` time zone has no
daylight saving time.