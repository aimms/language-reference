.. _sec:excel.example:

An Example
==========

.. rubric:: The Excel transport example...

To illustrate the functionality of the Excel add-in, the AIMMS
distribution contains an example, which provides a simple Excel workbook
that illustrates the use of the Excel add-in. In this example workbook,
all the input and output data of a transport model in AIMMS is retained
in the workbook and exchanged with AIMMS using the data exchange
functionality provided by the Excel add-in. You can find the example in
the *Examples* directory of your AIMMS installation.

.. rubric:: ... started from within AIMMS

In this section, you will learn how the same data exchange could be
accomplished from within your model using the spreadsheet function
library of AIMMS. The source code illustrated in this section is
contained in the AIMMS model accompanying the Excel Link example
workbook. Thus, if you run this model in a stand-alone way from within
AIMMS, the Excel Link example also serves as an example of the
spreadsheet function library.

.. rubric:: Retrieving the input data

The input data of the transport model consists of:

-  a set ``Depots`` with index ``d``,

-  a set ``Customers`` with index ``c``,

-  a parameter ``Supply(d)``,

-  a parameter ``Demand(c)``, and

-  a parameter ``UnitTransportCost(d,c)``.

Using the spreadsheet function library, the following function calls
retrieve all input data from the Excel workbook whose name is stored in
the string parameter ``WorkbookName``.

.. code-block:: aimms

	Spreadsheet::SetActiveSheet( WorkbookName, "Transport Model" );
	Spreadsheet::RetrieveSet( WorkbookName, Depots, "DepotsRange" );
	Spreadsheet::RetrieveSet( WorkbookName, Customers, "CustomersRange" );
	Spreadsheet::RetrieveParameter( WorkbookName, Supply, "SupplyRange" );
	Spreadsheet::RetrieveParameter( WorkbookName, Demand, "DemandRange" );
	Spreadsheet::RetrieveTable( WorkbookName, UnitTransportCost,
	                    "UnitTransportRange", "DepotsRange", "CustomersRange" );

This sequence of function calls, with the exception of the first call,
is the direct counterpart of the sequence of actions in the Excel
workbook example used to pass the model data to the AIMMS model.

.. rubric:: Explained

By calling the function :any:`Spreadsheet::SetActiveSheet`, you indicate to
AIMMS that all following calls operate on a single sheet, allowing you
to omit the sheet name as an optional argument in subsequent calls.
Through the functions

-  :any:`Spreadsheet::RetrieveSet`,

-  :any:`Spreadsheet::RetrieveParameter`, and

-  :any:`Spreadsheet::RetrieveTable`,

you indicate to AIMMS that the corresponding set and parameter data must
be obtained from the specified named Excel ranges. The functionality of
these functions is exactly the same as the functionality of the
corresponding actions in the Excel add-in. Note that ranges can also be
described using the standard A1 and R1C1 styles of Excel.

.. rubric:: Writing back the solution

The input data of the transport model consists of:

-  a variable ``Transport(d,c)``, and

-  a variable ``TotalCost`` containing the objective value of the
   optimization model.

These values can be stored in the given workbook using the following
function calls.

.. code-block:: aimms

	Spreadsheet::SetActiveSheet( WorkbookName, "Transport Model" );
	Spreadsheet::AssignParameter( WorkbookName, Transport, "TransportRange", sparse: 1 );
	Spreadsheet::AssignValue( WorkbookName, TotalCost, "TotalCostRange" );

.. rubric:: Explained

Again, these functions provide exactly the same functionality as the
corresponding actions in the Excel add-in, and the sequence of function
calls corresponds in a one-to-one fashion to the sequence of actions in
the Excel workbook example to retrieve the solution back from AIMMS.
Through the optional ``sparse`` argument of
:any:`Spreadsheet::AssignParameter` you can indicate whether zero values
should be passed as 0.0 or as a blank.

.. rubric:: Running a macro

The following function call illustrates how a macro contained in a
workbook can be run from within your AIMMS model.

.. code-block:: aimms

	Spreadsheet::RunMacro( WorkbookName, "AssignRandomTransportCost" );

In the Excel Link example this macro is used to randomize the values of
the range holding the values of ``UnitTransportCost``. After
re-retrieving the input data again and solving the model, this may
result in a different optimal solution to the transport model.