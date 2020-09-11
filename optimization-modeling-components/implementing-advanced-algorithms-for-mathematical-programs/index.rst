.. _chap:matrix:

.. _chap:gmp:

Implementing Advanced Algorithms for Mathematical Programs
==========================================================

.. rubric:: Control over the solution process

The ``SOLVE`` statement discussed in :ref:`sec:mp.solve` offers a
convenient way to execute all necessary steps to generate and solve a
single instance of a mathematical program in one simple statement. For
most applications, this level of control over the individual steps
required to execute the generation and solution process is sufficient.
However, for advanced applications, you may need a finer-grained level
of control, e.g. to

-  work with multiple, differing, instances of a single symbolic
   mathematical program,

-  manipulate the individual rows and columns and the coefficient matrix
   of a mathematical program instance, for example to efficiently
   implement a column generation scheme,

-  work with a repository of solutions associated with a mathematical
   program instance, for instance as a means to store multiple starting
   solutions or, within a solver callback, to setup and update a
   collection of incumbents of a mixed integer model, or

-  start multiple solver sessions for a mathematical program instance,
   either locally or remotely.

.. rubric:: This chapter

This chapter describes a library of procedures that offers you
fine-grained control over the generation, manipulation and solution of a
mathematical program instance, and allows you to manage a collection of
solutions and solver sessions associated with such mathematical program
instances. As you will see later on, the ``SOLVE`` statement can be
completely expressed in terms of the procedures in this library.

.. toctree::
   :maxdepth: 1

   introduction-to-the-gmp-library
   managing-generated-mathematical-program-instances
   matrix-manipulation-procedures
   managing-the-solution-repository
   using-solver-sessions
   synchronization-events
   multi-objective-optimization
   supporting-functions-for-stochastic-programs
   supporting-functions-for-robust-optimization-models
   supporting-functions-for-benders-decomposition
   creating-and-managing-linearizations
   customizing-the-progress-window
   examples-of-use