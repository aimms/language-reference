.. _sec:db.restrictions:

Database Table Restrictions
===========================

.. rubric:: Data transfer to single tables

The AIMMS ``READ`` and ``WRITE`` statements are intended to directly
transfer data to and from a *single* text or case file, or a *single*
table in a database. This is the simplest form of communication with a
database. If you need more advanced control over the connection with a
particular database, you can access stored procedures within the
database using AIMMS. Such procedures can be implemented by the database
designer to accomplish advanced tasks that go beyond the ordinary. The
use of stored procedures is discussed in
:ref:`sec:db.stored-procedures`.

.. rubric:: Automatic connection

When you are connecting to a table in a database through a ``READ`` or
``WRITE`` statement, you do not have to make a connection to the server
explicitly. The database table declaration and the ODBC configuration
files on your system provide sufficient information to allow AIMMS to
make the connection automatically whenever needed. If you need to log on
to the database, you will be prompted with a log on screen. On some
systems it is possible to store log on information in the ODBC data
source file.

.. rubric:: Different data representation

There is a fundamental difference in the storage of data in AIMMS and
the storage of data in a database table. Whereas AIMMS stores its data
separately per identifier, a database table stores the data of several
indexed identifiers in records all indexed by the same single index
tuple. This difference implies that AIMMS has to impose some additional
restrictions on data transfer with database tables that are not needed
when reading from or writing to either AIMMS case files or text files.

.. rubric:: Assumptions about database tables

In order to be able to define the semantics of the ``READ`` and
``WRITE`` statements to database tables in an unambiguous way, AIMMS
makes a number of (reasonable) assumptions about the database tables in
an external database. It is, however, not always possible for AIMMS to
verify these assumptions, and unexpected effects may occur when they do
not hold. The following assumptions about database tables are made.

-  Every database table is in second normal form, i.e. every non-primary
   column in the table is functionally dependent on the primary key.

-  Every primary column in a database table is mapped onto an index in
   an AIMMS domain set.

-  Every non-primary column in a database table is mapped onto a (slice
   of an) AIMMS identifier, such that the specific index domain of this
   identifier precisely matches the primary key of the database table
   according to the existing index mapping.

.. rubric:: Assumptions about identifier selections

AIMMS will not allow all identifier selections to be read from or
written to database tables. An identifier selection is allowed when the
following conditions hold for its components.

-  All parameter and variable references must have the same domain after
   slicing. The resulting domain must correspond to the primary key of
   the database table.

-  During a ``WRITE`` statement in ``REPLACE`` mode you can only write a
   simple set or relation mapped onto the primary key of a database
   table as long as there are no non-primary columns, or when the
   selection comprises all the columns of the table.

-  AIMMS allows each domain set associated with a primary column in a
   table of any dimension to be read from that table.

.. rubric:: Simply stated

The above rules can be summarized by stating that the database table can
be transformed into an AIMMS composite table for the indexed identifiers
in it.

.. rubric:: Selections are sparse

Identifier selections in ``READ`` and ``WRITE`` statements form a
one-to-one correspondence with a sparse set of records in the database
table. During a ``READ`` statement the sparsity pattern is determined by
all the records in the database table. During a ``WRITE`` statement the
sparsity pattern is determined by all indexed identifiers in the
selection. Records will be written for only those tuples for which at
least one of the indexed identifiers or tuple references has a
nondefault value. Thus, the transferred data resulting from a ``WRITE``
statement is equivalent to the single composite table in AIMMS for all
indexed identifiers in the selection.

.. rubric:: Creation of records

Writing data to a database in either merge or replace mode may lead to
the creation of new records in a database table. New records will be
created when AIMMS writes a tuple for a key for which no record is
available. If the table has non-primary attributes for which no data is
written, AIMMS will leave these attributes empty when it creates new
rows.

.. rubric:: Removal of records: ``REPLACE COLUMNS/ROWS`` mode

AIMMS supports two replace modes for writing: ``REPLACE COLUMNS`` mode
(default) and ``REPLACE ROWS`` mode.

-  In ``REPLACE`` or ``REPLACE COLUMNS`` mode, AIMMS will only remove
   data from columns mapped onto identifiers in your model. Rows will
   only be removed from the database table if *all* columns in the table
   are mapped onto identifiers in your model.

-  In ``REPLACE ROWS`` mode, AIMMS will remove all rows whose primary
   key does not correspond to an index tuple being written during the
   ``WRITE`` statement. Columns that are not mapped onto identifiers in
   your model, either are assigned their default value specified in the
   database, or a ``NULL`` value otherwise. As a consequence, you should
   make sure that all non-nullable columns in the table are mapped onto
   identifiers in your model (or have a default value in the database)
   during ``REPLACE ROWS`` mode.

AIMMS will only remove records if the selection you are writing
comprises all the columns in the database table, including the set
mapped onto the primary key. In this way, AIMMS ensures that no data is
lost in the table inadvertently.

.. rubric:: Filtering on records

Using the ``DatabaseTable`` interface it is only possible to filter
records using simple domain conditions formulated in a ``FILTERING``
clause. For huge database tables it may be desirable to use more
advanced filtering techniques designed to restrict the number of records
to be transferred. This can be done inside the database application
itself in the following two ways.

-  Create a *view* in the database that does the filtering for you, and
   then use the standard ``READ`` statement. This is the most
   straightforward approach, and is sufficient if the filter does not
   depend on AIMMS data.

-  Create a *stored procedure* in the database that can be activated
   through a ``DatabaseProcedure`` in AIMMS. This allows you to filter
   records dependent on the value of some AIMMS identifiers that are
   used as arguments of the stored procedure (see
   :ref:`sec:db.stored-procedures`).