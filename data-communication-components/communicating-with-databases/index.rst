.. _chap:db:

Communicating With Databases
============================

.. rubric:: Communicating with databases

One of the most important capabilities of the ``READ`` and ``WRITE``
statements in AIMMS is its ability to transfer data with ODBC-compliant
databases. Although there are similarities between the basic concepts of
data storage in databases and those in AIMMS, they are sufficiently
different to justify a separate chapter in this manual.

.. rubric:: This chapter

This chapter deals with the intricacies of data transfer from and to
databases. It first discusses the link between data in AIMMS and a table
in a database. Then it explains the database-specific requirements
regarding the ``READ`` and ``WRITE`` statements. Next comes a discussion
on how to access stored procedures, followed by a description how to
send SQL statements directly to a particular data source.

.. toctree::
   :maxdepth: 1

   the-databasetable-declaration
   indexed-database-tables
   database-table-restrictions
   data-removal
   executing-stored-procedures-and-sql-queries
   database-transactions
   testing-the-presence-of-data-sources-and-tables
   dealing-with-date-time-values