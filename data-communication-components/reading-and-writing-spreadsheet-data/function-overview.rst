.. _sec:excel.overview:

Function Overview
=================

.. rubric:: Function overview

In this section you will find an overview of all the functions provided
by the spreadsheet function library. The function library contains both

-  control functions, and

-  data exchange functions.

All functions are described in full detail in the `Function Reference <https://documentation.aimms.com/functionreference/>`__.

.. rubric:: Function naming

From AIMMS 3.12 Feature Release 1 on, the first part of the function
names has changed from ``Excel...`` to the more general
``Spreadsheet::...``, to reflect the fact that the functions are not
exclusively used to communicate with Excel anymore. When you want to
work with an OpenOffice Calc workbook, the ``WorkbookName`` argument of
the functions should end in ``.ods`` (which is the extension of Calc
workbooks). Any other ending of this argument will result in AIMMS
operating on an Excel workbook.

.. rubric:: Control functions

The control functions listed in :ref:`this table <table:spreadsheet.control>`
allow you to perform actions such as opening and closing workbooks and
worksheets, copying and printing ranges, and running macros contained in
the workbook.

.. rubric:: Not in Excel add-in

The control functions listed in :ref:`this table <table:spreadsheet.control>` do
not have a direct counterpart in the AIMMS Excel add-in. They represent
a subset of common spreadsheet commands, which may be convenient when
reading and writing data to an Excel or OpenOffice Calc workbook.

.. _table:spreadsheet.control:

.. table:: Spreadsheet control functions

   +--------------------------------------------+-------------------------------------------+
   | Procedure                                  | Description                               |
   +============================================+===========================================+
   | :any:`Spreadsheet::CreateWorkbook`         | Creates a workbook                        |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::SaveWorkbook`           | Saves an opened workbook                  |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::CloseWorkbook`          | Closes an opened workbook                 |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::AddNewSheet`            | Adds a new sheet to a workbook            |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::DeleteSheet`            | Delete a sheet from a workbook            |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::SetActiveSheet`         | Sets the currently active sheet           |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::Print`                  | Prints a range from a workbook            |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::ClearRange`             | Clears the specified range                |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::CopyRange`              | Copies a source into a destination range  |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::SetVisibility`          | Changes the visibility of a workbook      |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::SetUpdateLinksBehavior` | Sets the behavior w.r.t. linked workbooks |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::ColumnName`             | Returns the name of a numbered column     |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::ColumnNumber`           | Returns the number of a named column      |
   +--------------------------------------------+-------------------------------------------+
   | :any:`Spreadsheet::RunMacro`               | Runs the specified macro                  |
   +--------------------------------------------+-------------------------------------------+

.. rubric:: Data exchange functions

The functions listed in :ref:`this table <table:spreadsheet.exchange>` can be used
to exchange set data, scalar values, one- and two-dimensional
identifiers, and general multi-dimensional identifiers with tabular
ranges in an Excel or Calc sheet. Each of these functions corresponds to
an associated action in the Excel add-in.

.. _table:spreadsheet.exchange:

.. table:: Spreadsheet data exchange functions

   +---------------------------------------+------------------------------------------------+
   | Function                              | Description                                    |
   +=======================================+================================================+
   | :any:`Spreadsheet::AssignSet`         | Assigns set elements to specified range        |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::RetrieveSet`       | Fills set with elements from specified range   |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::AssignValue`       | Assigns scalar value to specified range        |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::RetrieveValue`     | Fills scalar parameter from specified range    |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::AssignParameter`   | Assigns 1- or 2-dimensional parameter to range |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::RetrieveParameter` | Fills 1- or 2-dimensional parameter from range |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::AssignTable`       | Assigns multi-dimensional parameter to range   |
   +---------------------------------------+------------------------------------------------+
   | :any:`Spreadsheet::RetrieveTable`     | Fills multi-dimensional parameter from range   |
   +---------------------------------------+------------------------------------------------+