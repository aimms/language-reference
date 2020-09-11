What is in the Language Reference
=================================

.. rubric:: Preliminaries

Part I of the Language Reference introduces and illustrates the basic
concepts of the AIMMS language.

-  :ref:`chap:intro` provides you
   with a quick overview of AIMMS' modeling capabilities through a
   simple, and completely worked out example model.

-  :ref:`chap:prelim` globally describes the
   basic structure of an AIMMS model, the available data types and
   execution statements.

.. rubric:: Nonprocedural language components

Part II introduces the fundamental concepts of sets and multidimensional
parameters, and discusses the expressions and evaluation mechanisms
available for these data types.

-  :ref:`chap:set` discusses the declaration and
   attributes of index sets.

-  :ref:`chap:par` describes the declaration and
   available attributes of scalar and multidimensional parameters which
   can be used to store and manipulate data.

-  :ref:`chap:set-expr` provides a complete overview of all expressions which
   evaluate to either a set, a set element or a string.

-  :ref:`chap:expr` describes all
   expressions which evaluate to a numerical or logical value, and also
   explains the concept of macro expansion in AIMMS.

-  :ref:`chap:nonproc` describes
   the dependency and automatic execution structure of the system of
   functional relationships formed by all defined sets and parameters.

.. rubric:: Procedural language components

Part III focuses on the procedural aspects of the AIMMS language which
allow you to implement you own algorithms, seamlessly making use of the
advanced built-in functionality already provided by AIMMS.

-  :ref:`chap:exec` provides a complete overview
   of all assignment and flow control statements in AIMMS.

-  :ref:`chap:bind` specifies the precise rules for the
   fundamental concept of index binding underlying AIMMS execution
   engine.

-  :ref:`chap:intern` explains how
   to declare and call internal AIMMS procedures and functions.

-  :ref:`chap:extern` explains how
   functions and procedures in an external DLL can be linked to and
   called from within an existing AIMMS application.

.. rubric:: Sparse execution

Part IV of the reference guide tries to make you aware of the
differences between a dense versus a sparse execution engine (as used by
AIMMS). It provides valuable insight into the inner workings of AIMMS
and may help to implement large-scale modeling applications in a correct
and efficient manner.

-  :ref:`chap:sparse` provides you
   with a basic insight into the inner workings AIMMS sparse execution
   engine, and provides a number of convenience operators to modify the
   semantics of some operators.

-  :ref:`chap:eff` discusses various
   techniques that you may apply to find and address performance issues
   in your AIMMS models.

.. rubric:: Optimization modeling components

Part V of the reference guide discusses all concepts offered by
AIMMS for specifying and solving optimization models.

-  :ref:`chap:var` discusses the
   declaration and attributes of variables and constraints.

-  :ref:`chap:mp` describes the steps
   necessary for specifying and solving an optimization program in
   AIMMS.

-  :ref:`chap:net` discusses the declaration
   and attributes of node and arc types available in AIMMS to specify
   single commodity network flow models.

-  :ref:`chap:nlp` discusses
   the multistart algorithm and nonlinear presolver available in AIMMS
   for nonlinear models.

-  :ref:`chap:compl` describes the
   declaration and attributes of complementarity variables, which can be
   used to specify mixed complementarity and MPCC models in AIMMS.

-  :ref:`chap:stoch` discusses the facilities
   in AIMMS to generate stochastic models and associated scenario trees
   for existing deterministic model formulations.

-  :ref:`chap:robust` introduces the facilities in
   AIMMS to generate and solve robust optimization models for existing
   deterministic model formulations.

-  :ref:`chap:gmp` describes a library of procedures which allow you to
   implement advanced algorithms for solving linear and mixed-integer
   linear programming models.

-  :ref:`ch:aoa` introduces an open approach to solving MINLP models using the
   well-known outer approximation algorithm.

.. rubric:: Data communication components

Part VI introduces the mechanisms provided by AIMMS to import data from
files and databases, as well as its capabilities to export data and
produce standardized or customized text reports.

-  :ref:`chap:data` describes your options to initialize the identifiers
   associated with an AIMMS model. It also introduces the concept of
   assertions which can be used to verify the consistency of data, as
   well as a number of data control statements which can help you to
   keep the data in a consistent state.

-  :ref:`chap:rw` describes the
   basic mechanism offered by AIMMS for data transfer with various data
   sources.

-  :ref:`chap:db` discusses the specific
   aspects of setting up a link between AIMMS and a database.

-  :ref:`chap:text.data.file` presents the
   various data formats offered by AIMMS for initializing a model
   through a number of text data files.

-  :ref:`chap:spreadsheet` provides you with an overview of AIMMS' capabilities to
   exchange data with Excel or with OpenOffice Calc workbooks.

-  :ref:`chap:xml` discusses AIMMS'
   facilities to read and write XML data from within AIMMS.

-  :ref:`chap:report` describes the
   statements and formatting options available for producing
   standardized and customized text reports.

.. rubric:: Advanced language components

Part VII of the reference guide introduces a number of advanced features
available in AIMMS both in the area of modeling and communication with
external applications.

-  :ref:`chap:units` discusses the declaration
   and use of units and unit conventions in an AIMMS model both for
   checking the consistency of a model formulation, scaling of
   mathematical programs and display of data in the interface and
   reports.

-  :ref:`chap:time` describes the advanced
   concepts in AIMMS to deal with time-dependent data and models in a
   flexible and easy manner.

-  :ref:`chap:api` offers a complete
   description of the application programming interface (API) which can
   be used to access AIMMS data structures and call AIMMS procedures
   from within an external DLL or application.

-  :ref:`chap:module` discusses the
   organizational data structures such as the main model, model sections
   and modules, which can be used to supply the model with a logical
   structure, as well as library modules, which facilitate model
   development by multiple developers.