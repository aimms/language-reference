.. _sec:prelim.init:

Data Initialization
===================

.. rubric:: Initialization syntax

The initialization of sets, parameters, and variables in an AIMMS
application can be done in several ways:

-  through the :ref:`InitialData attribute <attr:par.initialdata>` of sets, and parameters,

-  by reading in data from a *text file* in AIMMS data format,

-  by reading in data from a previous AIMMS session stored in a binary
   *case file*,

-  by reading in the data from an external *ODBC-compliant database*, or

-  by initializing an identifier through algebraic assignment
   statements.

.. rubric:: Order of initialization

When starting up your AIMMS application, AIMMS will initialize your
model identifiers in the following order.

-  Following compilation each identifier is initialized with the
   contents of its ``InitialData`` attribute.

-  Subsequently, AIMMS will execute the predefined procedure
   ``MainInitialization``. You can use it to specify ``READ`` statements
   to read in data from text files, case files or databases. In
   addition, it can contain any other algebraic statement necessary to
   initialize one or more identifiers in your model. Of course, you can
   also leave this procedure empty if you so desire.

The full details of model initialization are discussed in
:ref:`chap:data`.

.. rubric:: Entering the ``InitialData`` attribute

The ``InitialData`` attribute of an identifier can contain any
*constant* set-valued, set element-valued, string-valued, or numerical
expression. In order to construct such expressions (consisting of mostly
tables and lists), AIMMS offers so-called *data pages* which can be
created on demand. These pages help you enter the data in a convenient
and graphical manner.
