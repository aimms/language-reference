.. _sec:db.stored-procedures:

Executing Stored Procedures and SQL Queries
===========================================

.. rubric:: Sophisticated control

When transferring data from or to a database table, you may need more
sophisticated control over the data link than offered by the standard
``DatabaseTable`` interface. AIMMS offers you this additional control by
letting you have access to stored procedures as well as letting you
execute SQL statements directly. The following two paragraphs provide
some examples where such control may be useful.

.. rubric:: Useful for data processing

Your application may require its data in a somewhat different form than
is directly available in the database. In this case you may have to
perform some pre-processing of the data in the database. Similarly, you
may want to perform post-processing in the database after writing data
to it. In such circumstances you may call a stored procedure to perform
these tasks for you.

.. rubric:: Useful for dynamic access

In some cases, the required data for your application may need to be the
result of a parameterized query of the database, i.e. a database table
whose contents is dependent on one or more parameters which are only
known during runtime. Such dynamic tables are usually obtained as the
*result set* of a stored procedure or of a parameterized query. In this
case AIMMS will allow you to use a stored procedure call or a
dynamically composed SQL query inside the ``READ`` statement as if it
were a database table. Please note that it's currently not possible to
read a result set from an Oracle stored procedure, since Oracle uses a
non-standard mechanism for that (involving so-called *ref cursors*).

.. _database_procedure:

.. rubric:: The ``DatabaseProcedure`` declaration

Every stored procedure or SQL query that you want to call from within
AIMMS must be declared as a ``DatabaseProcedure`` within your
application. The attributes of a ``DatabaseProcedure`` are listed in
:ref:`this table <table:db.attr-db-procedure>`.

.. _table:db.attr-db-procedure:

.. table:: 

	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| Attribute           | Value type          | See also page                                                                     |
	+=====================+=====================+===================================================================================+
	| ``DataSource``      | *string*            | :ref:`The Datasource attribute <attr:db.data-source>`                             |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``Arguments``       | *argument-list*     | :ref:`sec:intern.ref`                                                             |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``StoredProcedure`` | *string-expression* |                                                                                   |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``SQLQuery``        | *string-expression* |                                                                                   |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``Owner``           | *string-expression* | :ref:`The Owner  attribute <attr:db.owner>`                                       |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``Property``        | ``UseResultSet``    |                                                                                   |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``Mapping``         | *mapping-list*      | :ref:`The Mapping attribute <attr:db.mapping>`                                    |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``Comment``         | *comment string*    | :ref:`The Text and Comment attributes <attr:prelim.comment>`                      |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	| ``Convention``      | *convention*        | :ref:`The Convention attribute <attr:db.convention>`, :ref:`sec:units.convention` |
	+---------------------+---------------------+-----------------------------------------------------------------------------------+
	
.. rubric:: SQL query or stored procedure

A ``DatabaseProcedure`` in AIMMS can represent either a (dynamically
created) SQL query or a call to a stored procedure. AIMMS makes the
distinction on the basis of the ``StoredProcedure`` and ``SQLQuery``
attributes. If the ``StoredProcedure`` attribute is nonempty, AIMMS
assumes that the ``DatabaseProcedure`` represents a stored procedure and
expects the ``SQLQuery`` attribute to be empty, and vice versa.

.. rubric:: The ``StoredProcedure`` attribute
   :name: attr:db.proc.actual-name

.. _database_procedure.stored_procedure:

.. _database_procedure.owner:

With the ``StoredProcedure`` attribute you can specify the name of the
stored procedure within the ODBC data source that you want to be called.
The ``StoredProcedure`` wizard will let you select any stored procedure
name available within the specified ODBC data source. If the stored
procedure that you want to call is not owned by yourself, or if there
are name conflicts, you should specify the owner with the ``Owner``
attribute.

.. _database_procedure.sql_query:

.. rubric:: The ``SQLQuery`` attribute

You can use the ``SQLQuery`` attribute to specify the SQL query that you
want to be executed when the ``DatabaseProcedure`` is called. The value
of this attribute can be any string expression, allowing you to generate
a dynamic SQL query using the arguments of the ``DatabaseProcedure``.

.. rubric:: The ``Arguments`` attribute
   :name: attr:db.proc.arguments

.. _database_procedure.arguments:

With the ``Arguments`` attribute you can indicate the list of *scalar*
arguments of the database procedure. The specified arguments must have a
matching declaration in a declaration section local to the
``DatabaseProcedure``. If the ``DatabaseProcedure`` represents a stored
procedure, the argument list is interpreted as the argument list of the
stored procedure. When you use the ``StoredProcedure`` wizard, AIMMS
will automatically enter the argument list, including their AIMMS
prototype, for you. For a ``DatabaseProcedure`` representing an SQL
query, you can use the arguments in composing the SQL query string.

.. rubric:: Input-output type

For SQL queries all arguments must be ``Input`` arguments, as the query
cannot modify them. For stored procedures, the ``StoredProcedure``
wizard will by default set the input-output type of each argument equal
to its SQL input-output type. However, if you want to discard the result
of any output argument, you can change its type to ``Input``.

.. rubric:: The ``Property`` attribute
   :name: attr:db.proc.property

.. _database_procedure.property:

.. _useresultset:

With the ``Property`` attribute of a ``DatabaseProcedure`` you can
indicate the intended use of the procedure.

-  When you do not specify the property ``UseResultSet``, AIMMS lets you
   call the ``DatabaseProcedure`` as if it were an AIMMS procedure.

-  When you do specify the property ``UseResultSet``, AIMMS lets you use
   the ``DatabaseProcedure`` as a parameterized table in the ``READ``
   statement. In that case, you can also provide a ``Mapping`` attribute
   to specify the mapping from column names in the result set onto the
   corresponding AIMMS identifiers.

.. rubric:: Stored procedure examples

The following declarations will make two stored procedures contained in
the data source ``Topological Data`` available in your AIMMS
application. The local declarations of all arguments are omitted for the
sake of brevity. They are all assumed to be ``Input`` arguments.

.. code-block:: aimms

	DatabaseProcedure StoreSingleTransport {
	    DataSource       : "Topological Data";
	    StoredProcedure  : "SP_STORE_SINGLE_TRANSPORT";
	    Arguments        : (from, to, transport);
	}
	DatabaseProcedure SelectTransportNetwork {
	    DataSource       : "Topological Data";
	    StoredProcedure  : "SP_DISTANCE";
	    Arguments        : MaxDistance;
	    Property         : UseResultSet;
	    Mapping          : {
	        "from"        --> i,
	        "to"          --> j,
	        "dist"        --> Distance(i,j),
	        ("from","to") --> Routes
	    }
	}

The procedure ``StoreSingleTransport`` can be used like any other AIMMS
procedure, as in the following statement.

.. code-block:: aimms

	StoreSingleTransport( 'Amsterdam', 'Rotterdam',
	                      Transport('Amsterdam', 'Rotterdam') );

The second procedure ``SelectTransportNetwork`` can be used in a
``READ`` statement as if it were a database table, as illustrated below.

.. code-block:: aimms

	read from table SelectTransportNetwork( UserSelectedDistance );

.. rubric:: SQL query example

The following example illustrates the declaration of a
``DatabaseProcedure`` representing a direct SQL query. Its aim is to
delete those records in the specified table for which the column
``VersionCol`` equals the specified version. Both arguments must be
declared as local ``Input`` string parameters.

.. code-block:: aimms

	DatabaseProcedure DeleteTableVersion {
	    DataSource  : "Topological Data";
	    Arguments   : (DeleteTable, DeleteVersion);
	    SQLQuery    : {
	        FormatString( "DELETE FROM %s WHERE VersionCol = '%s'",
	                      DeleteTable, DeleteVersion )
	    }
	}

.. rubric:: Executing SQL statements directly

In addition to executing SQL queries through ``DatabaseProcedure``,
AIMMS also allows you to execute SQL statements directly within a data
source. The interface for this mechanism is simple, and forms a
convenient alternative for a ``DatabaseProcedure`` when you want to
execute a single SQL statement only once.

.. _directsql-LR:

.. rubric:: The procedure :any:`DirectSQL`

You can send SQL statements to a data source by calling the procedure
:any:`DirectSQL` with the following prototype:

-  :any:`DirectSQL`\ (*data-source*, *SQL-string*)

Both arguments of the procedure should be string expressions. Note that
in case the SQL statement also produces a result set, then this set is
ignored by AIMMS.

.. rubric:: Example

The following call to :any:`DirectSQL` drops a table called
``"Temporary_Table`` from the data source ``Topological Data"``.

.. code-block:: aimms

	DirectSQL( "Topological Data",
	           "DROP TABLE Temporary_Table" );

.. rubric:: Use :any:`FormatString`

The procedure :any:`DirectSQL` does not offer direct capabilities for
parameterizing the SQL string with AIMMS data. Instead, you can use the
function :any:`FormatString` to construct symbolic SQL statements with
terms based on AIMMS identifiers.