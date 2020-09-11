.. _chap:rw:

The ``READ`` and ``WRITE`` Statements
=====================================

.. rubric:: Dynamic data transfer

In order to help you separate the model description and its input and
output data, AIMMS offers the ``READ`` and ``WRITE`` statements for
dynamic data transfer between your modeling application and external
data sources such as

-  *text data files*, and

-  *database tables* in external ODBC-compliant databases.

.. rubric:: This chapter

This chapter first introduces the ``READ`` and ``WRITE`` statements in
the form of an extended example. Subsequently, their semantics are
presented in full detail including issues such as filtering, domain
checking, and slicing.

.. toctree::
   :maxdepth: 1

   a-basic-example
   syntax-of-the-read-and-write-statements