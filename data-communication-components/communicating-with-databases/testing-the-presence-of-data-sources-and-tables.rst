.. _sec:db.avail:

Testing the Presence of Data Sources and Tables
===============================================

.. rubric:: Fail safe access

When you want to run an AIMMS-based application on the computer of an
end-user, you may want to make sure that the data sources and database
tables required to run the application successfully are present, prior
to actually initiating any data transfer. Normally, trying to execute a
``READ`` and ``WRITE`` statements on a nonexisting data source or
database table causes AIMMS to generate run-time errors, which might be
confusing to your end-users. By first verifying the presence of the
required data sources and database tables, you are able to generate
error messages which are more meaningful to your end-users.

.. _testdatasource-LR:

.. _testdatabasetable-LR:

.. rubric:: Syntax

You can test the presence of data sources and database tables on a host
computer through the functions

-  :any:`TestDataSource`\ (*data-source*)

-  :any:`TestDatabaseTable`\ (*data-source*, *table-name*)

Both *data-source* and *table-name* are string arguments.

.. rubric:: The procedure :any:`TestDataSource`

With the procedure :any:`TestDataSource` you can check whether the ODBC
data source named *data-source* is present on the host computer on which
your AIMMS application is being run. The procedure returns 1 if the data
source is present, or 0 otherwise.

.. rubric:: The procedure :any:`TestDatabaseTable`

The function :any:`TestDatabaseTable` lets you check whether a given table
named *table-name* exists in the data source named *data-source*. The
procedure returns 1 if the database table is present in the given data
source, or 0 otherwise. However, the procedure :any:`TestDatabaseTable`
will not let you check whether the table contains the columns which you
expect it to contain. If you try to access columns in the database table
which are not present during either a ``READ`` or ``WRITE`` statement,
AIMMS will still generate a run-time error to this effect.