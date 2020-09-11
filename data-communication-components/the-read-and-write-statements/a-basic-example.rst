.. _sec:rw.example:

A Basic Example
===============

.. rubric:: Getting started

The aim of this section is to give you an overview of the ``READ`` and
``WRITE`` statements through a short illustrative example. It shows how
to read data from and write data to text files and database tables. It
is based on the familiar transport problem with the following input
data:

-  the set ``Cities``,

-  the relation ``Routes`` from ``Cities`` to ``Cities``,

-  the parameters ``Supply(i)`` and ``Demand(i)`` for each city ``i``,
   and

-  the parameters ``Distance(i,j)`` and ``TransportCost(i,j)`` for each
   route between two cities ``i`` and ``j``.

For the sake of simplicity, it is assumed that there is only a single
output, the actual ``Transport(i,j)`` along each route.

.. rubric:: Format of input data

The input data can be conveniently given in the form of tables. One for
the identifiers defined over a single city like ``Supply`` and
``Demand``, and the other for the identifiers defined over a tuple of
cities like ``Distance`` and ``TransportCost``. These tables can be
provided in the form of text files as in :ref:`examp:rw.examp-data`
(format explained in :ref:`sec:text.composite`). Alternatively, the data
can be obtained from particular tables in a database. This example
assumes the following database tables exist:

-  ``CityData`` for the one-dimensional parameters, and

-  ``RouteData`` for the two-dimensional parameters.

.. code-block:: aimms
   :caption: Example data set for the transport model
   :name: examp:rw.examp-data

	COMPOSITE TABLE
	    Cities      Supply  Demand
	!   ----------  ------  ------
	    Amsterdam     50
	    Rotterdam    100
	    Antwerp       75      25
	    Berlin               125
	    Paris                 75
	;

.. code-block:: aimms

	COMPOSITE TABLE
	    i          j          Distance  TransportCost
	!   ---------  ---------  --------  -------------
	    Amsterdam  Rotterdam       85        1.00
	    Amsterdam  Antwerp        170        2.50
	    Amsterdam  Berlin         660       10.00
	    Amsterdam  Paris          510        8.25
	    Rotterdam  Antwerp        100        1.20
	    Rotterdam  Berlin         700       10.00
	    Rotterdam  Paris          440        7.50
	    Antwerp    Berlin         725       11.00
	    Antwerp    Paris          340        5.00
	    Berlin     Paris         1050       17.50
	;

.. _sec:rw.example.simple:

Simple Data Transfer
--------------------

.. rubric:: Simple data initialization

The simplest use of the ``READ`` statement is to initialize data from a
fixed name text data file, or a database table. 
To read all the data from each source, the
following groups of statements will suffice

.. code-block:: aimms

	read from file  "transport.inp" ;

	read from table CityData;
	read from table RouteData;

Such statements are typically found in the body of the predefined
procedure ``MainInitialization``.

.. rubric:: Reading identifier selections

When a data source also contains data for identifiers that are of no
interest to your particular application (but may be to others), AIMMS
allows you to restrict the data transfer to a specific selection of
identifiers in that data source. For instance, the following ``READ``
statement will only read the identifiers ``Distance`` and
``TransportCost``, not changing the current contents of the AIMMS
identifiers ``Supply`` and ``Demand``.

.. code-block:: aimms

	read Distance, TransportCost from file "transport.inp" ;

Similar identifier selections are possible when reading from

a database table.

.. rubric:: Writing the solution

After your model has computed the optimal transport, you may want to
write the solution ``Transport(i,j)`` to an text output file for future
reference. You can do this by calling the ``WRITE`` statement, which has
equivalent syntax to the ``READ`` statement. The transfer of
``Transport(i,j)`` to the file ``transport.out`` is accomplished by the
following ``WRITE`` statement.

.. code-block:: aimms

	write Transport to file "transport.out" ;

If you omit an identifier selection, AIMMS will write all model data to
the file. When writing to a database table, AIMMS can of course only
transfer data for those identifiers that are known in the table that you
are writing to.

.. rubric:: File name need not be explicit

File data transfer is not restricted to files with a fixed name. To
choose the name of the data file either during execution or from within
the end-user interface, you have several options:

-  replace the filename string in the ``READ`` and ``WRITE`` statements
   with a string-valued parameter holding the filename, or

-  use a ``File`` identifier (for text files only).

.. _sec:rw.example.domain:

Set Initialization and Domain Checking
--------------------------------------

.. rubric:: Domain restrictions

When you are reading the initial data of the transport model from an
external data source several situations can occur:

-  you just want to initialize the set ``Cities`` from the data source,

-  the set ``Cities`` has already been initialized, and you want to
   retrieve the parametric data for existing cities only, or

-  the set ``Cities`` has already been initialized, but you want to
   extend it on the basis of the data read from the external data
   source.

.. rubric:: The ``READ`` statements

The following statements impose domain restrictions on the ``READ``
statement.

.. code-block:: aimms

	read Cities
	     from file "transport.inp" ;

	read Supply, Demand
	     from file "transport.inp"
	     filtering i ;

	read Supply, Demand
	     from file "transport.inp" ;

.. rubric:: Initializing sets

The first ``READ`` statement is a straightforward initialization of the
set ``Cities``. By default, AIMMS reads in replace mode, which implies
that any previous contents of the set ``Cities`` is overwritten.

.. rubric:: Domain checking

The second ``READ`` statement assumes that the set ``Cities`` has
already been initialized. From all entries of the identifiers ``Supply``
and ``Demand`` it will only read those which correspond to existing
elements in the set ``Cities``, and skip over the data from the
remaining entries.

.. rubric:: Extending domain sets

The third ``READ`` statement differs from the second in that the clause
``FILTERING i`` has been omitted. As a result, AIMMS will not reject
data that does not correspond to an existing label in the set
``Cities``, but will read all available ``Supply`` and ``Demand`` data,
and extend the set ``Cities`` accordingly.