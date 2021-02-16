.. _sec:db.database-table:

The ``DatabaseTable`` Declaration
=================================

.. rubric:: Database tables
   :name: database-table

You can make a database table known to AIMMS by means of a
``DatabaseTable`` declaration in your application. Inside this
declaration you can specify the ODBC data source name of the database
and the name of the database table from which you want to read, or to
which you want to write. The list of attributes of a ``DatabaseTable``
is given in :ref:`this table <table:db.attr-db-table>`.

.. _table:db.attr-db-table:

.. table:: 

	=============== =================== ==============================================================
	Attribute       Value-type          See also page
	=============== =================== ==============================================================
	``IndexDomain`` *index-domain*      :ref:`The IndexDomain attribute <attr:par.index-domain>`
	``DataSource``  *string-expression*    
	``TableName``   *string-expression*    
	``Owner``       *string-expression*    
	``Property``    ``ReadOnly``           
	``Mapping``     *mapping-list*         
	``Text``        *string*            :ref:`The Text and Comment attributes <attr:prelim.comment>`
	``Comment``     *comment string*    :ref:`The Text and Comment attributes <attr:prelim.comment>`
	``Convention``  *convention*        :ref:`sec:units.convention`
	=============== =================== ==============================================================
	
.. rubric:: The ``DataSource`` attribute
   :name: attr:db.data-source

.. _database_table.data_source:

The mandatory ``DataSource`` attribute specifies the ODBC data source
name of the database you want to link with. Its value must be a string
or a string parameter. If you are unsure about the data source name by
which a particular database is known, AIMMS will help you. While
completing the declaration form of a database table, AIMMS will
automatically let you choose from the available data sources on your
system using the ``DataSource`` wizard. AIMMS supports the following
data source types:

-  ODBC file data sources (``.dsn`` extension, only available on
   Windows), and

-  ODBC user and system data sources (no extension), and

-  ODBC connection string.

In addition, you can specify the name of an AIMMS string parameter,
holding the name of any of the above data source types. If the data
source you are looking for is not available in this list, you can set up
a link to that database from within the wizard.

.. rubric:: The ``TableName`` attribute
   :name: attr:db.table-name

.. _database_table.table_name:

With the ``TableName`` attribute you must specify the name of the table
or view within the data source to which the ``DatabaseTable`` is mapped.
Once you have provided the ``DataSource`` attribute, the ``TableName``
wizard will let you select any table or view available in the specified
data source.

.. rubric:: Example

The following declaration illustrates the simplest possible
``DatabaseTable`` declaration.

.. code-block:: aimms

	DatabaseTable RouteData {
	    DataSource  :  "Topological Data";
	    TableName   :  "Route Definition";
	}

It will connect to an ODBC user or system data source called
``Topological Data``, and in that data source search for a table named
``Route Definition``.

.. rubric:: The ``Owner`` attribute
   :name: attr:db.owner

.. _database_table.owner:

The ``Owner`` attribute is for advanced use only. By default, when
connecting to a database server, you will have access to all tables and
stored procedures which are visible to you. In case a table name appears
more than once, but is owned by different users, by default a connection
is made to the table instance owned by yourself. By specifying the
``Owner`` attribute you can gain access to the table instance owned by
the indicated user.

.. rubric:: The ``Property`` attribute
   :name: attr:db.property

.. _database_table.property:

With the ``Property`` attribute of a ``DatabaseTable`` you can specify
whether the declared table is ``ReadOnly``. Specifying a database table
as ``ReadOnly`` will prevent you from inadvertently modifying its
content. If you do not provide this property, the database table will
default to read-write permissions unless the server does not allow write
access.

.. rubric:: The ``Mapping`` attribute
   :name: attr:db.mapping

.. _database_table.mapping:

.. _column-name:

By default, AIMMS tries to map the column names used in a database table
onto the AIMMS identifiers of the same name. Such an implicit mapping
is, of course, not always possible. When you link to an existing
database that was not specifically designed for your AIMMS application,
it is very likely that the column names do not correspond to the names
of your AIMMS identifiers. Therefore, the ``Mapping`` attribute lets you
override this default. The database columns explicitly mapped through
the ``Mapping`` attribute are added to the set of implicit mappings
constructed by AIMMS. The column names from the database table used in a
mapping list must be quoted. If the implicit mapping is not desirable
you can provide the property ``No Implicit Mapping``.

.. rubric:: Example

The following declarations demonstrate the use of mappings in a
``DatabaseTable`` declaration. This example assumes the set and
parameter declarations of :ref:`sec:rw.example` plus the existence of
the relation ``Routes`` given by

.. code-block:: aimms

	Set Routes {
	    SubsetOf     : (Cities, Cities);
	}

The following mapped database declaration will take care of the
necessary column to identifier mapping.

.. code-block:: aimms

	DatabaseTable RouteData {
	    DataSource   :  "Topological Data";
	    TableName    :  "Route Definition";
	    Mapping      : {
	        "from"        --> i,                              ! name substitution
	        "to"          --> j,
	        "dist"        --> Distance(i,j),

	        "fcost"       --> TransportCost(i,j,'fixed'),     ! slicing
	        "vcost"       --> TransportCost(i,j,'variable'),

	        ("from","to") --> Routes                          ! mapping to relation
	    }
	}

.. rubric:: Name substitution

The first three lines of the ``Mapping`` attribute provide a simple name
translation from a column in the database table to an AIMMS identifier.
You can only use this type of mapping if the structural form of the
database table (i.e. the primary key) coincides with the domain of the
AIMMS identifier.

.. rubric:: Mapping columns to slices

If the number of attributes in the primary key of a database table is
lower than the dimension of the intended AIMMS identifier, you can also
map a column name to a *slice* of an AIMMS identifier of the proper
dimension, as shown in the ``fcost`` and ``vcost`` mapping. You can do
this by replacing one or more of the indices in the identifier's index
space with a reference to a fixed element.

.. rubric:: Mapping primary key to relation

As shown in the last line of the ``Mapping`` attribute, you can let the
complete primary key in a database table correspond with a simple set,
or with a relation (see :ref:`sec:set.relation`) in AIMMS. This
correspondence is specified by mapping the tuple of primary attributes
of the table onto the AIMMS set itself, or onto an index into this set.
The primary attributes in the tuple are mapped in a one-to-one fashion
onto the indices in the relation.

.. rubric:: Syntax

The syntax of the ``Mapping`` attribute is given by the following
diagram.

.. _mapping-list:

*mapping-list:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 473.29735 147.19999"
	   height="147.2"
	   width="473.29733"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,720.26665)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,5000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 400,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,46.4,436)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 600,4400 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 800,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,85,436)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/communicating-with-databases/the-databasetable-declaration.html#column-name">column-name</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1626.84,4400 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 700,4400 20,50 h -40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1113.42,4700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,117.742,466)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1313.42,4700 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1726.84,4400 20,50 h -40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1826.84,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g52"><text
	           id="text56"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,189.084,436)"><tspan
	             id="tspan54"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2026.84,4400 50,-20 v 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2226.84,5000 -20,-50 h 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 800.004,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,85,496)"><tspan
	             id="tspan66"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/communicating-with-databases/the-databasetable-declaration.html#column-name">column-name</a></tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1626.84,5000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2326.84,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g74"><text
	           id="text78"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,237.684,496)"><tspan
	             id="tspan76"
	             y="0"
	             x="0">--&gt;</tspan></text>
	</g><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2642.84,5000 50,-20 v 40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2742.84,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,279.284,496)"><tspan
	             id="tspan86"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#reference">reference</a></tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3349.72,5000 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,5000 20,50 H 80" /><path
	         id="path94"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1674.86,5300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g96"><text
	           id="text100"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,173.886,526)"><tspan
	             id="tspan98"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1874.86,5300 50,-20 v 40" /><path
	         id="path104"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3449.73,5000 20,50 h -40" /><path
	         id="path106"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3549.73,5000 -50,20 v -40" /><path
	         id="path108"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5000 h 100 m 0,0 v 0 h 100 m 0,0 v -500 c 0,-55.23 44.773,-100 100,-100 v 0 h 100 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 100 m 0,0 v 0 h 100 v 100 h 826.82 V 4400 4300 H 800 v 100 m 826.84,0 h 100 M 700,4400 v 200 c 0,55.23 44.773,100 100,100 h 213.42 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 100 213.42 c 55.23,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 100 v 0 c 55.23,0 100,44.77 100,100 v 500 M 200,5000 h 100 400 100 v 100 h 826.82 V 5000 4900 H 800 v 100 m 826.84,0 h 100 500 100 v 0 c 0,55.23 44.78,100 100,100 h 116 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -116 c -55.22,0 -100,44.77 -100,100 v 0 m 316,0 h 100 v 100 h 606.87 v -100 -100 h -606.87 v 100 m 606.88,0 h 100 M 100,5000 v 200 c 0,55.23 44.773,100 100,100 h 1374.86 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 100 1374.87 c 55.22,0 100,-44.77 100,-100 v -200 h 100" /></g></g></svg></div>

.. rubric:: The ``Convention`` attribute
   :name: attr:db.convention

With the ``Convention`` attribute you can indicate to AIMMS that the
external data is stored with the units provided in the specified
convention. If the unit specified in the convention differs from the
unit that AIMMS uses to store its data internally, the data is scaled at
the time of transfer. For the declaration of ``Conventions`` you are
referred to :ref:`sec:units.convention`.

.. rubric:: Date conversions

In addition, you can use ``Conventions`` to convert calendar data from
the calendar slot format used within your model to the format expected
by the database and vice versa. The use of ``Conventions`` for this
purpose is discussed in full detail in :ref:`sec:time.tz`. For
non-calendar related date-time values you can use the predefined
identifier ``OBDCDateTimeFormat`` to accomplish this (see
:ref:`sec:db.date-time`).