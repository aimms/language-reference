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

.. rubric:: The Excel Add-In

On the other hand, *from within Excel*, it is possible to exchange data
with an AIMMS model in a variety of list and tabular formats using the
Excel add-in provided with AIMMS. The Excel add-in is described in full
detail in the *Excel Add-In `User's Guide <https://documentation.aimms.com/_downloads/AIMMS_user.pdf>`__*.

.. rubric:: The OpenOffice Calc function library

From AIMMS version 3.12 FR1 on, it is also possible to communicate with
OpenOffice Calc workbooks from within the AIMMS model (there is no
equivalent of the Excel add-in for OpenOffice Calc). The function
library is the same as used for the communication with Excel from within
the AIMMS model. To use the functions with OpenOffice Calc workbooks
instead of Excel workbooks, simply use the extension ``.ods`` in the
``WorkbookName`` argument of the functions.

.. rubric:: This chapter

This chapter provides a brief description of an AIMMS function library
that allows you programmatic access, *from within your model*, to the
extensive data exchange capabilities provided by the Excel add-in.

.. toctree::
   :maxdepth: 1

   an-example
   function-overview