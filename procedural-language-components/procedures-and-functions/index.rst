.. _chap:intern:

Procedures and Functions
========================

.. rubric:: Functions and procedures

Functions and procedures are pieces of execution code dedicated to a
specific task that can be called either from within the graphical
end-user interface or from within the model text. Both functions and
procedures in AIMMS can have arguments. A function returns either a
scalar value or an indexed set of values, and can be used inside
expressions. Procedures are more general than functions in that they can
have both multiple inputs and outputs. A procedure invocation is a
single statement in AIMMS, and can be used to modify the values of
global identifiers.

.. rubric:: Procedures for initiating execution

Any computation that is part of your application must be started from
within a procedure. For simple applications, execution from within the
predefined procedure ``MainExecution`` is usually sufficient to perform
all tasks. However, in more complicated applications there are often
many entry points, and these can best be implemented as separate
procedures.

.. rubric:: This chapter

This chapter describes how to construct and use procedures and functions
in the AIMMS language. Such procedures and functions are called
*internal*. In :ref:`chap:extern` you will find additional material on
how to link *external* functions and procedures written in ``FORTRAN``
and ``C`` to your application.

.. toctree::
   :maxdepth: 1

   internal-procedures
   internal-functions
   calls-to-procedures-and-functions