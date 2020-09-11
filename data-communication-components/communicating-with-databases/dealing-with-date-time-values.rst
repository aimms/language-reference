.. _sec:db.date-time:

Dealing with Date-Time Values
=============================

.. rubric:: Mapping date-time values

Special care is required when you want to read data from or write data
to a database which represents a date, a time, or a time stamp in the
database table. The ODBC technology uses a fixed string format for each
of these data types. Most likely, this format will not coincide with the
format that you use to store dates and times in your modeling
application.

.. rubric:: Mapped onto calendars

When a column in a database table containing date-time values maps onto
a ``Calendar`` in your AIMMS model, AIMMS will automatically convert the
date-time values to the associated time slot format of the calendar, and
store the corresponding values for the appropriate time slots.

.. rubric:: Time zone translation

By default, AIMMS assumes that the date-time values mapped onto a
particular ``CALENDAR`` are stored in the database according to the same
time zone (ignoring daylight saving time) as specified in the
``TimeslotFormat`` attribute of that calendar (see also
:ref:`sec:time.format.dst`). In the absence of such a time zone
specification, AIMMS will assume the local time zone (without daylight
saving time). You can override the time zone through the
``TimeslotFormat`` attribute of a ``Convention``. The use of
``Conventions`` with respect to ``Calendar`` is discussed in full detail
in :ref:`sec:time.tz`.

.. rubric:: The :any:`ODBCDateTimeFormat` parameter

If a date-time column in a database table does not map onto a
``Calendar`` in your model, you can still convert the ODBC date-time
format into the date- or time representation of your preference, using
the predefined string parameter :any:`ODBCDateTimeFormat` defined over the
set of :any:`AllIdentifiers`. With it, you can specify, on a per identifier
basis, the particular format that AIMMS should use to store dates and/or
times using the formats discussed in :ref:`sec:time.format`. AIMMS will
never perform a time zone conversion for non-calendar data, and will
ignore :any:`ODBCDateTimeFormat` when it contains a date-time format
specification for a ``CALENDAR``.

.. rubric:: Unmapped columns

If you do not specify a date-time format for a particular identifier,
and the column does not map onto a ``Calendar``, AIMMS will assume the
fixed ODBC format. These formats are:

-  *YYYY-MM-DD hh:mm:ss.tttttt* for date-time columns,

-  *YYYY-MM-DD* for date columns, and

-  *hh:mm:ss* for time columns.

When you are unsure about the specific type of a date/time/date-time
column in the database table during a ``WRITE`` action, you can always
store the AIMMS data in date-time format, as AIMMS can convert these to
both the date and time format. During a ``READ`` action, AIMMS will
always translate into the type for the column type.

.. rubric:: Example

A stock ordering model contains the following identifiers:

-  the set ``Products`` with index ``p``, containing all products kept
   in stock,

-  an ordinary set ``OrderDates`` with index ``d``, containing all
   ordering dates, and

-  a string parameter ``ArrivalTime(p,d)`` containing the arrival time
   of the goods in the warehouse.

The order dates should be of the format '\ ``140319``\ ', whilst the
arrival times should be formatted as '\ ``12:30 PM``\ ' or
'\ ``9:01 AM``\ '. Using the time specifiers of :ref:`sec:time.format`,
you can accomplish this through the following assignments to the
predefined parameter :any:`ODBCDateTimeFormat`:

.. code-block:: aimms

	ODBCDateTimeFormat( 'OrderDates' )  := "%y%m%d";
	ODBCDateTimeFormat( 'ArrivalTime' ) := "%h:%M %p";