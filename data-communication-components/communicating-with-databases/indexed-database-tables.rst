.. _sec:db.indexed-table:

Indexed Database Tables
=======================

.. rubric:: Exogenous columns in primary key

While the ``Mapping`` attribute allows you to map data columns in a
database table onto a slice of a higher-dimensional AIMMS identifier, a
different type of slicing is required when the primary key of a database
table contains *exogenous* columns that are of no interest to your
application. Consider, for instance, the following situations.

-  You are linking to a database table that contains data for a huge set
   of cities, but your model only deals with a single city that is not
   explicitly part of the model formulation. For your application the
   city column is exogenous.

-  A table in a database contains several versions of a particular data
   set, where the version number is represented by an additional version
   column in the table. For your application the version column is
   exogenous.

.. _database_table.index_domain:

.. rubric:: Indexed DatabaseTables

In your AIMMS application you can deal with these situations by
partitioning a single table inside the database into a set of *virtual*
lesser-dimensional tables indexed by the exogenous column(s). You can do
this by declaring the database table to have an ``IndexDomain``
corresponding to the sets that map onto the exogenous columns. In
subsequent ``READ`` and ``WRITE`` statements you can then refer to a
particular instance of a virtual table through a reference to the
database table with an explicit set element or an element parameter.

.. rubric:: Example

The following example assumes that the table ``"Route Definition"``
contains several versions of the data, each identified by the value of
an additional column ``version``. In the AIMMS model, this column is
associated with a set ``TableVersions`` given by the following
declaration.

.. code-block:: aimms

	Set TableVersions {
	    Index      : v;
	    Parameter  : LatestVersion;
	}

The following declaration will provide a number of virtual tables
indexed by ``v``.

.. code-block:: aimms

	DatabaseTable RouteData {
	    IndexDomain  :  v;
	    DataSource   :  "Topological Data";
	    TableName    :  "Route Definition";
	    Mapping      : {
	        "version"   --> v,
	        "from"      --> i,
	        "to"        --> j,
	        "dist"      --> Distance(i,j),
	        "cost"      --> TransportCost(i,j)
	    }
	}

Note that the index ``v`` in the index domain is mapped onto the column
``version`` in the table.

.. rubric:: Data transfer with indexed tables

In order to obtain the set of ``TableVersions`` you can follow one of
two strategies:

-  you can obtain the set of the available versions from the table
   ``"Route Definition"`` itself by declaring another ``DatabaseTable``
   in AIMMS

   .. code-block:: aimms
   
   	DatabaseTable VersionTable {
   	    DataSource   :  "Topological Data";
   	    TableName    :  "Route Definition";
   	    Mapping      : {
   	        "version"   --> TableVersions
   	    }
   	}

-  or, you can obtain the versions from a separate table in a relational
   database declared similarly as above.

A typical sequence of actions for data transfer with indexed tables
could then be the following.

-  Read the set of all possible versions from ``VersionTable``:

   .. code-block:: aimms
   
   	read TableVersions from table VersionTable ;

-  Obtain the value of ``LatestVersion`` from within the language or the
   graphical user interface.

-  Read the data accordingly:

   .. code-block:: aimms
   
   	read Distance, TransportCost from RouteData(LatestVersion) ;