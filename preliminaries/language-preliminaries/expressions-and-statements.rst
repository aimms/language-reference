.. _sec:prelim.expr:

Expressions and Statements
==========================

.. rubric:: Model execution

The creation of an AIMMS model is implemented using two separate but
interacting mechanisms. They are:

-  automatic updating of the functional relationships specified through
   expressions in the ``Definition`` attributes of sets and parameters
   in your model, and

-  manual execution of the statements that constitute the ``Body``
   attribute of the procedures and functions defined in your
   application.

The precise manner in which these components are executed, and the way
they interact, is discussed in detail in :ref:`chap:nonproc` and
:ref:`chap:exec`. This section discusses the general structure of an
AIMMS model as well as the requirements for the ``Definition`` and
``Body`` attributes.

.. rubric:: Line length and empty lines

The length of any particular line in the ``Definition`` attribute of an
identifier or the ``Body`` attribute of a procedure or function is
limited to 255 characters. Although this full line length may be
convenient for data instantiation in the form of large tables, it is
recommended that you do not exceed a line length of 80 characters in
these attributes in order to preserve maximum readability. Empty lines
can be inserted anywhere for easier reading.

.. rubric:: Commenting

Expressions and statements in the ``Body`` attribute of a procedure or
function can be interspersed with comments that are ignored during
compilation. AIMMS supports two kinds of comments:

-  the tokens ``/*`` and ``*/`` for a block comment, and

-  the exclamation mark ``!`` for a one line comment.

Each block comment starts with a ``/*`` token, and runs up to the
matching ``*/`` token, and cannot be nested. It is a useful method for
entering pieces of explanatory text, as well as for temporarily
commenting out one or more execution statements. A one-line comment
starts anywhere on a line with an exclamation mark ``!``, and runs up
to the end of that line.

.. rubric:: Expressions

The value of a ``Definition`` attribute must be a valid expression of
the appropriate type. An expression in AIMMS can result in either

-  a set,

-  a set element,

-  a string,

-  a numerical value,

-  a logical value, or

-  a unit expression.

Set, element and string expressions are discussed in full detail in
:ref:`chap:set-expr`, numerical and logical expressions in
:ref:`chap:expr`, while unit expressions are discussed in
:ref:`chap:units`.

.. rubric:: Statements

AIMMS statements in the body of procedures and functions constitute the
algorithmic part of a modeling application. All statements are
terminated by a semicolon. You may enter multiple statements on a single
line, or a single statement over several lines.

.. rubric:: Execution statements

To specify the algorithmic part of your modeling application, the
following statements can be used:

-  assignments-to compute a new value for a data item,

-  the ``SOLVE`` statement-to solve a mathematical program for the
   values of its variables,

-  flow control statements like ``IF-THEN-ELSE``, ``FOR``, ``WHILE``,
   ``REPEAT``, ``SWITCH``, and ``HALT``-to manage the flow of execution,

-  the ``OPTION`` and ``Property`` statements-to set identifier
   properties and options dealing with execution, output, progress, and
   solvers,

-  the data control statements ``EMPTY``, ``CLEANUP``, ``READ``,
   ``WRITE``, ``DISPLAY``, and ``PUT``-to manage the contents of
   internal and external data.

-  procedure calls-to execute the statements contained in a procedure.

The precise syntax of these execution statements is discussed in
:ref:`chap:exec` and further.