.. _sec:intro.expressions:

Data Initialization
===================

.. rubric:: Separation of model and data

In the previous section the entire depot location model was specified
without any reference

-  to specific elements in the sets ``Depots`` and ``Customers``, or

-  to specific values of parameters defined over such elements.

As a result of this clear separation of model and data values, the model
can easily be run for different data sets.

.. rubric:: Data sources

A data set can come from various sources. In AIMMS there are six sources
you might consider for your application. They are:

-  commercial databases,

-  text data files,

-  AIMMS case files,

-  internal procedures,

-  external procedures, or

-  the AIMMS graphical user interface (GUI).

These data sources are self-explanatory with perhaps the AIMMS case
files as an exception. AIMMS case files are obtained by using the case
management facilities of AIMMS to store data values from previous runs
of your model.

.. rubric:: A simple data set in text format

The following fictitious data set is provided in the form of an text
data file. It illustrates the basic constructs available for providing
data in text format. In this file, assignments are made using the
'\ ``:=``\ ' operator and the keywords of ``DATA TABLE`` and
``COMPOSITE TABLE`` announce the table format. The exclamation mark
denotes a comment line.

.. code-block:: aimms

	  Depots    := DATA { Amsterdam, Rotterdam };
	  Customers := DATA { Shell, Philips, Heineken, Unilever };

	  COMPOSITE TABLE
	      d        DepotRentalCost    DepotCapacity
	! ---------    ---------------    -------------
	  Amsterdam        25550              12500
	  Rotterdam        31200              14000
	;

	  COMPOSITE TABLE
	      c        CustomerDemand
	! ---------    --------------
	  Shell            10000
	  Philips           5000
	  Heineken          3000
	  Unilever          5000
	;

	  Distance(d,c) := DATA TABLE
	                Shell   Philips   Heineken   Unilever
	  !             -----   -------   --------   --------
	  Amsterdam      100      200        50         150
	  Rotterdam       75      100        50          75
	  ;

	  UnitTransportRate   := 1.25 ;
	  MaxDeliveryDistance := 125  ;

.. rubric:: Reading in the data

Assuming that the text data file specified above was named
``"initial.dat"``, then its data can easily be read using the following
``READ`` statement.

.. code-block:: aimms

	read from file "initial.dat" ;

Such ``READ`` statements are typically placed in the predefined
procedure ``MainInitialization``. This procedure is automatically
executed at the beginning of every session immediately following the
compilation of your model source.

.. rubric:: Automatic initialization

When AIMMS encounters any reference to a set or parameter with its own
definition inside a procedure, AIMMS will automatically compute its
value on the basis of its definition. When used inside the procedure
``MainInitialization``, this form of data initialization can be viewed
as yet another data source in addition to the six data sources mentioned
at the beginning of this section.