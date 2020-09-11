.. _sec:time.tz:

Working in Multiple Time Zones
==============================

.. rubric:: Multiple time zones

If your application uses external time-dependent data supplied by users
worldwide, you are faced with the problem of converting all dates and
times to the calendar in which your application is set up to run. The
facilities described in this section help you with that task.

.. rubric:: Obtaining time zone info

With the functions ``TimeZoneOffset``, :any:`DaylightSavingStartDate` and
``DayLightSavingEndDate`` you can obtain various time zone specific
characteristics.

-  ``TimeZoneOffset``\ (*FromTimeZone*, *ToTimeZone*)

-  :any:`DaylightSavingStartDate`\ (*year*, *TimeZone*)

-  :any:`DaylightSavingEndDate`\ (*year*, *TimeZone*)

The function ``TimeZoneOffset`` returns the offset in minutes between
the time zones *FromTimeZone* and *ToTimeZone*. You can use the function
:any:`DaylightSavingStartDate` and :any:`DaylightSavingEndDate` to retrieve
the reference dates, within a particular time zone, corresponding to the
begin and end date of daylight saving time.

.. rubric:: Example

.. code-block:: aimms

	offset    := TimeZoneOffset('UTC', 'Eastern Standard Time');
	             ! result: -300 [min]
	startdate := DaylightSavingStartDate( '2001', 'Eastern Standard Time');
	             ! result: "2001-04-01 02"

.. rubric:: Converting reference dates

With the function :any:`ConvertReferenceDate` you can convert reference
dates to different time zones. Its syntax is:

-  :any:`ConvertReferenceDate`\ (*ReferenceDate*, *FromTimeZone*,
   *ToTimeZone*\ [, *IgnoreDST*])

With the function you can convert a reference date *ReferenceDate*,
within the time zone *FromTimeZone*, to a reference date within the time
zone *ToTimeZone*. If the optional argument *IgnoreDST* is set to 1,
AIMMS will ignore daylight saving time for both input and output
reference dates (see also :ref:`sec:time.format.dst`). By default, AIMMS
will not ignore daylight saving time.

.. rubric:: Example

.. code-block:: aimms

	UTCdate := ConvertReferenceDate("2001-05-01 12", 'Local', 'UTC');
	           ! result: "2001-05-01 11"

.. rubric:: ``Conventions`` and time zones

When your application needs to read data from or write data to a
database or file with dates not specified in local time, some kind of
conversion of all dates appearing in the data source is required during
the data transfer. To support you with such date conversions, AIMMS
allows you to override the default timeslot format of one or more
calendars in your model through a unit ``Convention`` (see also
:ref:`sec:units.convention`).

.. rubric:: The ``TimeslotFormat`` attribute

In the ``TimeslotFormat`` attribute of a ``Convention`` you can specify
the time slot format (see also :ref:`sec:time.format`) to be used for
each ``Calendar`` while communicating with an external source. The
syntax of the ``TimeslotFormat`` attribute is:

.. _timeslot-format-list:

.. rubric:: Syntax

*timeslot-format-list:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 300.48533 67.199997"
	   height="67.199997"
	   width="300.48532"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,186.93333)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,25,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/time-based-modeling/calendars.html#calendar">calendar</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 760.199,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 860.199,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,92.4199,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1060.2,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1160.2,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,121.02,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/time-based-modeling/format-of-time-slots-and-periods.html#timeslot-format">timeslot-format</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2053.64,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,1000 20,50 H 80" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1026.82,1300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,109.082,126)"><tspan
	             id="tspan50"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1226.82,1300 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2153.64,1000 20,50 h -40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2253.64,1000 -50,20 v -40" /><path
	         id="path60"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 100 m 0,0 v 0 h 100 v 100 H 760.188 V 1000 900 H 200 v 100 m 560.199,0 h 100 v 0 c 0,55.23 44.774,100 100,100 v 0 c 55.231,0 100.001,-44.77 100.001,-100 v 0 0 c 0,-55.227 -44.77,-100 -100.001,-100 v 0 c -55.226,0 -100,44.773 -100,100 v 0 m 200.001,0 h 100 v 100 h 893.41 V 1000 900 H 1160.2 v 100 m 893.44,0 h 100 M 100,1000 v 200 c 0,55.23 44.773,100 100,100 h 726.82 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 726.82 c 55.23,0 100,-44.77 100,-100 v -200 h 100" /></g></g></svg></div>

.. rubric:: Use in graphical user interface

When an active ``Convention`` overrides the time slot format for a
particular calendar, all calendar elements will be displayed according
to the time slot format specified in the ``Convention``. The time slot
format specified in the calendar itself is then ignored.

.. rubric:: Reading and writing to file

If you use a ``Convention`` to override the time slot format while
writing data to a data file, report file or listing file, AIMMS will
convert all calendar elements to the format specified in the
``TimeslotFormat`` for that calendar in the ``Convention`` prior to
writing the data. Similarly, when reading data from a data file, AIMMS
will interpret the calendar slots present in the file according to the
specified time slot format, and convert them to the corresponding
calendar elements in the model.

.. rubric:: Database communication...

When communicating calendar data to a database, there is one additional
issue that you have to take into account, namely the data type of the
column in which the calendar data is stored in the database table. If
calendar data is stored in a string column, AIMMS will transfer data
according to the exact date-time format specified in the
``TimeslotFormat`` attribute of the ``Convention``, including any
indicators for specifying the time zone and/or daylight saving time.

.. rubric:: ... for datetime columns

However, if the data type of the column is a special date-time data
type, AIMMS will always communicate calendar slots as reference dates,
which is the standard date-time string representation used by ODBC. In
translating calendar slots to reference dates, AIMMS will adhere to the
format specified in the ``TimeslotFormat`` attribute of either the
``Calendar`` itself, or as overridden in the currently active
``Convention``.

.. rubric:: Generated reference dates

The reference dates are generated according to the time zone specified
in the ``%TZ`` specifier of the currently active ``TIMESLOT SPECIFIER``.
These dates always ignore daylight saving time (i.e. shift back by one
hour if necessary), as daylight saving time cannot be represented in the
fixed reference date format. Specifiers in the ``TIMESLOT FORMAT`` other
than the ``%TZ`` specifier are not used when mapping to date-time values
in a database. If you do not specify a ``%TZ`` specifier in the
``TIMESLOT FORMAT``, AIMMS will assume that all date-time columns in a
database are represented in the ``'Local'`` time zone (the default).

.. rubric:: Example

Consider the calendar ``HourCalendarLocalDST`` defined below.

.. code-block:: aimms

	Calendar HourCalendarLocalDST {
	    Index           :  hd;
	    Unit            :  hour;
	    BeginDate       :  "2001-03-25 00";
	    EndDate         :  "2001-03-25 06";
	    TimeslotFormat  :  "%c%y-%m-%d %H:00%TZ('LocalDST')|\"\"|\" DST\"|";
	}

If you want to transfer data defined over this calendar with a database
table in which all dates are represented in UTC time, you should define
a convention defined as follows.

.. code-block:: aimms

	Convention UTCConvention {
	    TimeslotFormat  : {
	        HourCalendarLocalDST : "%c%y-%m-%d %H:00%TZ('UTC')"
	    }
	}

When this convention is active, AIMMS will represent all calendar slots
of the calendar ``HourCalendarLocalDST`` as reference dates according to
the UTC time zone, by shifting as many hours as dictated by the local
time zone and/or daylight saving time if applicable. Hence, when you use
the convention ``UTCConvention`` during data transfer with the database,
all calendar data slots will be in the expected format.