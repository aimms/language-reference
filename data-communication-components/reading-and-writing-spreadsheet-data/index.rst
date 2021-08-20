.. _chap:spreadsheet:

Reading and Writing Spreadsheet Data
====================================

.. rubric:: Treating Excel as a database

While it is technically possible to exchange data with Excel through the
``READ`` and ``WRITE`` statements using the ODBC database connectivity
interfaces (see :ref:`chap:db`), the Excel ODBC drivers have many
limitations. Essential internal SQL statements like ``UPDATE`` and
``DELETE`` are not supported by these interfaces, effectively making the
``READ`` statement the only AIMMS statement which might be used in this
setup. For this reason, we strongly recommend you not to use this setup,
but to consider to use the spreadsheet functions, described in this
chapter, instead. Please note that there are no ODBC drivers available
for OpenOffice Calc, so the remarks above apply to the Excel case only.

.. rubric:: The AIMMSXLLibrary

The :doc:`axll:index`
is the preferred way to communicate with excel files from AIMMS applications.
This library can also communicate with Excel files in server environments 
where Excel is not installed. This is particularly useful when one deploys 
applications on :doc:`docs:pro/index` 
which is typically installed on a machine with no Office or Excel instance.

.. rubric:: The Data Exchange library

The :doc:`docs:dataexchange/index` 
allows you to flexibly map any JSON, XML format, 
and CSV or Excel sheet onto appropriate identifiers in your AIMMS model. 

