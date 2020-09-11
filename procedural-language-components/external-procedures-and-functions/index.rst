.. _chap:extern:

External Procedures and Functions
=================================

.. rubric:: Why call external procedures
   :name: external

Even though AIMMS offers easy-to-use multidimensional data structures
combined with a powerful programming language, there are often good
reasons to relay parts of the execution of your model to external
procedures and functions written in e.g. ``C``/``C++`` or ``FORTRAN``.
The capability to call external procedures and functions in your AIMMS
application allows you

-  to re-use existing software (e.g. a library of financial functions,
   or a collection of accurate, nonlinear process models),

-  to speed up selected computations by making use of dedicated data
   structures which are difficult to implement in AIMMS itself, and

-  to provide links to external data sources (e.g. on-line data feeds or
   proprietary databases).

.. rubric:: This chapter

This chapter describes the steps you have to follow for linking
libraries of external procedures and functions to AIMMS. Such procedures
and functions can be used to manipulate AIMMS data during the execution
of a model. In addition, external libraries may contain functions that
can be used inside the constraints of a nonlinear mathematical program.

.. toctree::
   :maxdepth: 1

   introduction
   declaration-of-external-procedures-and-functions
   win32-calling-conventions
   external-functions-in-constraints
   c-versus-fortran-conventions