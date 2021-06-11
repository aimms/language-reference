.. _sec:time.calendar:

Calendars
=========

.. _calendar:

.. rubric:: Calendars

A *calendar* is defined as a set of consecutive *time slots* of unit
length covering the complete time frame from the calendar's begin date
to its end date. You can use a calendar to index data defined in terms
of calendar time.

.. rubric:: Calendar attributes

Calendars have several associated attributes, which are listed in
:ref:`this table <table:time.attr-calendar>`. Some of these attributes are
inherited from sets, while others are new and specific to calendars. The
new ones are discussed in this section.

.. _table:time.attr-calendar:

.. table:: Calendar attributes

   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | Attribute          | Value-type        | See also page                                                | Mandatory |
   +====================+===================+==============================================================+===========+
   | ``BeginDate``      | *string*          |                                                              | yes       |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``EndDate``        | *string*          |                                                              | yes       |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``Unit``           | *unit*            |                                                              | yes       |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``TimeslotFormat`` | *string*          |                                                              | yes       |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``Index``          | *identifier-list* | :ref:`The Index attribute <attr:set.index>`                  | yes       |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``Parameter``      | *identifier-list* | :ref:`The Parameter attribute <attr:set.parameter>`          |           |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``Text``           | *string*          | :ref:`The Text and Comment attributes <attr:prelim.text>`    |           |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+
   | ``Comment``        | *comment string*  | :ref:`The Text and Comment attributes <attr:prelim.comment>` |           |
   +--------------------+-------------------+--------------------------------------------------------------+-----------+

.. _calendar.unit:

.. rubric:: Unit

The ``Unit`` attribute defines the length of a single time slot in the
calendar. It must be specified as one of the following time units or an
integer multiple thereof:

-  ``century``,

-  ``year``,

-  ``month``,

-  ``day``,

-  ``hour``,

-  ``minute``,

-  ``second``, and

-  ``tick`` (i.e. ``sec``/100).

Thus, ``15*min`` and ``3*month`` are valid time units, but the
equivalent ``0.25*hour`` and ``0.25*year`` are not. Besides a constant
integer number it is also allowed to use an AIMMS parameter to specify
the length of the time slots in the calendar
(e.g. ``NumberOfMinutesPerTimeslot*min``).

.. rubric:: Not predefined

Although you can only use the fixed unit names listed above to specify
the ``Unit`` attribute of a calendar, AIMMS does not have a predefined
``Quantity`` for time (see also :ref:`chap:units`). This means that the
units of time you want to use in your model, do not have to coincide
with the time units required in the calendar declaration. Therefore,
prior to specifying the ``Unit`` attribute of a calendar, you must first
specify a quantity defining both your own time units and the conversion
factors to the time units required by AIMMS. In the **Model Explorer**,
AIMMS will automatically offer to add the relevant time ``Quantity`` to
your model when the calendar unit does not yet exist in the model tree.

.. _calendar.begin_date:

.. _calendar.end_date:

.. rubric:: BeginDate and EndDate

The mandatory ``BeginDate`` and ``EndDate`` attributes of a calendar
specify its range. AIMMS will generate all time slots of the specified
length, whose *begin time* lies between the specified ``BeginDate`` and
``EndDate``. As a consequence, the *end time* of the last time slot may
be after the specified ``EndDate``. An example of this behavior occurs,
for instance, when the requested length of all time slots is 3 days and
the ``EndDate`` does not lie on a 3-day boundary from the ``BeginDate``.
Any period references that start outside this range will be ignored by
the system. This makes it easy to select all relevant time-dependent
data from a database.

.. _calendar.reference_date_format:

.. rubric:: Reference date format

Any set element describing either the ``BeginDate`` or the ``EndDate``
must be given in the following fixed *reference date* format which
contains the specific year, month, etc. up to and including the
appropriate reference to the time unit associated with the calendar.

   ``YYYY-MM-DD hh:mm:ss``

All entries must be numbers *with leading zeros present*. The hours are
expressed using the 24-hour clock. You do not need to specify all
entries. Only those fields that refer to time units that are longer or
equal to the predefined AIMMS time unit in your calendar are required.
All time/date fields beyond the requested granularity are ignored. For
instance, a calendar expressed in hours may have a ``BeginDate`` such as

-  ``1996-01-20 09:00:00``, or

-  ``1996-01-20 09:00``, or

-  ``1996-01-20 09``,

which all refer to exactly the same time, 9:00 AM on January 20\ *th*,
1996.

.. rubric:: Time zone and DST offsets

AIMMS always assumes that reference dates are specified according to UTC. However, for calendars
with granularity ``day`` AIMMS will ignore any timezone and daylight
saving time offsets, and just take the day as specified. In the example
above, a daily calendar with the above ``BeginDate`` will always start
with period ``1996-01-20``, while an hourly calendar may start with a
period ``1996-01-19 23:00`` if the difference between UTC and the time zone specification in the timeslot format is 10
hours.

.. _calendar.timeslot_format:

.. rubric:: Format of time-related attributes

Set elements and string-valued parameters capturing time-related
information must deal with a variety of formatting possibilities in
order to meet end-user requirements around the globe (there are no true
international standards for formatting time slots and time periods). The
flexible construction of dates and date formats using the
``TimeslotFormat`` is presented in :ref:`sec:time.format`.

.. rubric:: Example

The following example is a declaration of a daily calendar and a monthly
calendar

.. code-block:: aimms

	Calendar DailyCalendar {
	    Index            : d;
	    Parameter        : CurrentDay;
	    Text             : A work-week calendar for production planning;
	    BeginDate        : "1996-01-01";
	    EndDate          : "1997-06-30";
	    Unit             : day;
	    TimeslotFormat   : {
	        "%d/%m/%y"      ! format explained later
	    }
	}
	Calendar MonthlyCalendar {
	    Index            : m;
	    BeginDate        : CalendarBeginMonth;
	    EndDate          : CalendarEndMonth;
	    Unit             : month;
	    TimeslotDormat   : {
	        "%m/%y"         ! format explained later
	    }
	}

.. rubric:: Varying number of time slots

The calendar ``DailyCalendar`` thus declared will be a set containing
the elements ``'01/01/96'``,...,\ ``'06/30/97'`` for every day in the
period from January 1, 1996 through June 30, 1997. When the
``BeginDate`` and ``EndDate`` attributes are specified as string
parameters containing the respective begin and end dates (as in
``MonthlyCalendar``), the number of generated time slots can be changed
dynamically. In order to generate zero time slots, leave one of these
string parameters empty.

.. rubric:: Time zones and daylight saving time

By default, AIMMS assumes that a calendar uses the local time zone
without daylight saving time, in accordance with the specification of
the ``BeginDate`` and ``EndDate`` attributes. However, if this is not
the case, you can modify the ``TimeslotFormat`` attribute in such a
manner, that AIMMS

-  will take daylight saving time into account during the construction
   of the calendar slots, or,

-  will generate the calendar slots according to a specified time zone.

In both cases, AIMMS still requires that the ``BeginDate`` and
``EndDate`` attributes be specified as reference dates in the local time
zone without daylight saving time, as already indicated. Support for
time zones and daylight saving time is explained in full detail in
:ref:`sec:time.format.dst`.
