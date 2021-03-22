.. _sec:data.init:

Model Initialization and Termination
====================================

.. rubric:: Separation of model and data

In general, it is a good strategy to separate the initialization of data
from the specification of your model structure. This is particularly
true for large models. The separation improves the clarity of the model
text, but more importantly, it allows you to use the same model
structure with various data sets.

.. rubric:: Supplying initial data

There are several methods to input the initial data of the identifiers
in your model. AIMMS allows you:

-  to supply initial data for a particular identifier as part of its
   declaration,

-  to read in data from various external data sources, such as text data
   files, AIMMS cases and databases, and

-  to initialize data by means of algebraic statements.

.. rubric:: Interactive initialization

In an interactive application the end-user often has to enter additional
data or modify existing data before the core of the model can be
executed. Thus, proper data initialization in most cases consists of
more steps than just reading data from external sources. It is the
responsibility of the modeler to make sure that an end-user is guided
through all necessary initialization steps and that the sequence is
completed before the model is executed.

.. _initial_data:

.. _attr:par.initialdata:

.. rubric:: The attribute ``InitialData``

Both sets and parameters can have an ``InitialData`` attribute. You can
use it to supply the initial data of a set or parameter, but only when
the set or parameter does not have a definition as well. In general, the
``InitialData`` attribute is not recommended when different data sets
are used. However, it can be useful for initializing those identifiers
in your model that are likely to remain constant for all data sets. The
contents of the ``InitialData`` attribute must be a *constant
expression* (i.e. a constant, a constant enumerated set or a constant
list expression) or a ``DataTable``. The table format is explained in
:ref:`sec:text.table`.

.. rubric:: The ``MainInitialization`` and ``PostMainInitialization`` procedures

AIMMS will add the procedures ``MainInitialization`` and
``PostMainInitialization`` to a new project automatically. Initially
these are empty, leaving the (optional) specification of their bodies to
you. You can use these procedures to read in data from external sources
and to specify AIMMS statements to compute your model's initial data in
terms of other data. The latter step may even include solving a
mathematical program. Both the ``MainInitialization`` and
``PostMainInitialization`` procedure are aimed at initializing your
model. The distinction between the two becomes apparent in the presence
of libraries in your model (cf. :ref:`sec:module.library`).

.. rubric:: Library initialization

Each library can provide ``LibraryInitialization`` and
``PostLibraryInitialization`` procedures. The ``LibraryInitialization``
procedure is aimed at initializing the state of each library,
*regardless of the state of other libraries*, such as sets and
parameters that represent the internal state of the library, or, when
the library uses an external DLL, initializing such a DLL. The
``PostLibraryInitialization`` procedures are executed after all
``LibraryInitialization`` procedures have been executed, and thus, can
rely on the internal state of all other libraries already being
initialized to perform tasks on its behalf.

.. rubric:: Model initialization sequence

To initialize the data in your model, AIMMS performs the following
actions directly after compiling the model:

-  AIMMS fills the contents of any global set or parameter with the
   contents of its ``InitialData`` attribute,

-  AIMMS executes the predefined procedures ``MainInitialization``,

-  AIMMS executes the predefined procedure ``LibraryInitialization`` for
   each library,

-  AIMMS executes the predefined procedure ``PostMainInitialization``,
   and

-  finally AIMMS executes the predefined procedure
   ``PostLibraryInitialization`` for each library.

Thus, as a guideline, any model initialization that depends on (other)
libraries should go into a ``PostLibraryInitialization`` or the
``PostMainInitialization`` procedure, to make sure that it can be
executed successfully.

.. rubric:: Library termination

Similarly to the situation of library initialization, each library can
provide ``PreLibraryTermination`` and ``LibraryTermination`` procedures.
The ``PreLibraryInitialization`` procedures are executed before all
``LibraryTermination`` procedures have been executed, and are aimed at
at library termination steps that may still need other libraries to be
functioning. The ``LibraryTermination`` procedures are aimed at
terminating the state of each library individually, for instance, to
deinitialize any external DLLs the library may depend upon.

.. rubric:: Model termination sequence

To terminate your model, AIMMS performs the following actions directly
prior to closing the project:

-  AIMMS executes the predefined procedure ``PreMainTermination``,

-  AIMMS executes the predefined procedure ``PreLibraryTermination`` for
   each library,

-  AIMMS executes the predefined procedures ``MainTermination``, and

-  finally AIMMS executes the predefined procedure
   ``LibraryTermination`` for each library.

.. _sec:data.init.external:

Reading Data from External Sources
----------------------------------

.. rubric:: The ``READ`` statement

You can use the ``READ`` statement to initialize data from the following
external data sources:

-  user-supplied text files containing constant lists and tables,

-  AIMMS-generated binary case files, and

-  external ODBC-compliant databases.

.. rubric:: Reading from text data files

With the ``READ`` statement you can initialize selected model input data
from text files containing explicit data assignments. Only
``DataTables`` and constant expressions (i.e. a constant, a constant
enumerated set or a constant list expression) are allowed. Since the
format of these AIMMS data assignments is simple, the corresponding
files are easily generated by external programs or by using the AIMMS
``DISPLAY`` statement.

.. rubric:: When useful

Reading from text files is especially useful when

-  the data must come directly from your end-users, but is not contained
   in a formal database,

-  the data is produced by external programs that are not linked or
   cannot be linked directly to AIMMS

.. rubric:: Reading from binary case files

The ``READ`` statement can also initialize data from an AIMMS case file.
You can instruct AIMMS to read either selected identifiers or all
identifiers. The case file data is already in an appropriate format, and
therefore provides a fast medium for data storage and retrieval inside
your application.

.. rubric:: When useful

Reading from case files is especially useful when

-  you want to start up your AIMMS application in the same state as you
   left it when you last used it,

-  you want to read from different data sources captured inside
   different cases making up your own internal database.

.. rubric:: Reading from databases

A third (and powerful) application of the ``READ`` statement is the
retrieval of data from any ODBC-compliant database. This form of data
initialization gives you direct access to up-to-date corporate
databases.

.. rubric:: When useful

Reading from databases is especially useful when

-  data is shared by several users or applications inside an
   organization,

-  data integrity over time in a database plays a crucial role during
   the lifetime of your application.

.. rubric:: Computing initial data

After reading initial data from internal and external sources, AIMMS
allows you to compute other identifiers not yet initialized. This
feature is very useful when the external data sources of your model
supply only partial initial data. For instance, after reading in event
data which represent tank actions (when and at what rate do charges and
discharges take place), all stock levels at distinct model time
instances can be computed.