.. _sec:gmp.progress:

Customizing the Progress Window
===============================

.. rubric:: Customizing the progress window

When you are using the GMP library to implement a customized algorithm
for a particular problem or problem class, you can use the procedures in
the ``GMP::ProgressWindow`` namespace to customize the contents of the
AIMMS Progress Window. This allows you to provide customized feedback to
the end-user regarding the progress of the overall solution algorithm,
or to provide simultaneous progress information about multiple solver
session executing in parallel.

.. rubric:: Customizing progress

The procedures and functions of the ``GMP::ProgressWindow`` namespace
are listed in :numref:`table:gmp.progress`. They allow you to modify
every aspect of the solver part of the AIMMS progress window.

.. _GMP::ProgressWindow::UnfreezeLine-LR:

.. _GMP::ProgressWindow::Transfer-LR:

.. _GMP::ProgressWindow::FreezeLine-LR:

.. _GMP::ProgressWindow::DeleteCategory-LR:

.. _GMP::ProgressWindow::DisplaySolverStatus-LR:

.. _GMP::ProgressWindow::DisplayProgramStatus-LR:

.. _GMP::ProgressWindow::DisplayLine-LR:

.. _GMP::ProgressWindow::DisplaySolver-LR:

.. _table:gmp.progress:

.. table:: 

	+------------------------------------------------------------------+
	| ``DisplaySolver``\ (*name*\ [, *Category*])                      |
	+------------------------------------------------------------------+
	| ``DisplayLine``\ (*lineNr*, *title*, *value*\ [, *Category*])    |
	+------------------------------------------------------------------+
	| ``DisplayProgramStatus``\ (*status*\ [, *Category*][, *lineNo*]) |
	+------------------------------------------------------------------+
	| ``DisplaySolverStatus``\ (*status*\ [, *Category*][, *lineNo*])  |
	+------------------------------------------------------------------+
	| ``FreezeLine``\ (*lineNo*, *totalFreeze*\ [, *Category*])        |
	+------------------------------------------------------------------+
	| ``UnfreezeLine``\ (*lineNo*\ [, *Category*])                     |
	+------------------------------------------------------------------+
	| ``DeleteCategory``\ (*Category*)                                 |
	+------------------------------------------------------------------+
	| ``Transfer``\ (*Category*, *solverSession*)                      |
	+------------------------------------------------------------------+
	
.. rubric:: Creating a new progress category

When your model executes multiple solver sessions in parallel, you can
request AIMMS to create a new progress *category* to display separate
solver progress for each solver session in a separate area of the
progress window. Using the function
:any:`GMP::Instance::CreateProgressCategory`, you can create a new progress
category for a specific mathematical program instance that will
subsequently be used to display solver progress for *all* solver
sessions associated with that mathematical program instance.
Alternatively, you can create a per-session category to display separate
solver progress for every single solver session using the function
:any:`GMP::SolverSession::CreateProgressCategory`. The procedure
:any:`GMP::ProgressWindow::Transfer` allows you to share a progress
category among several solver sessions. Through the function
:any:`GMP::ProgressWindow::DeleteCategory` you can delete progress
categories created by either function.

.. rubric:: Freezing category content

Through the functions :any:`GMP::ProgressWindow::FreezeLine` and
:any:`GMP::ProgressWindow::UnfreezeLine` you can instruct AIMMS to stop and
start updating particular areas of the solver progress area associated
with the progress category.

.. rubric:: Displaying custom content

When you are writing a custom algorithm you can use the progress window
to display custom progress information supplied by you using the
functions

-  :any:`GMP::ProgressWindow::DisplaySolver`,

-  :any:`GMP::ProgressWindow::DisplayLine`,

-  :any:`GMP::ProgressWindow::DisplayProgramStatus`, and

-  :any:`GMP::ProgressWindow::DisplaySolverStatus`.

When your custom algorithm consists of a sequence of solves, you can use
these functions, for instance, to display custom progress information
for the overall algorithm, possibly in combination with regular progress
for the underlying solves in a separate category.

.. rubric:: Example of use

An example of the usage of the ``GMP::ProgressWindow`` can be found in
the AIMMS module containing the GMP Outer Approximation algorithm
discussed in :ref:`sec:aoa.impl`. In this module, the contents of the
AIMMS progress window is adapted for the AIMMS Outer Approximation
solver.