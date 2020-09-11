.. _chap:var:

Variable and Constraint Declaration
===================================

.. rubric:: Terminology

The word variable does not have a uniform meaning. In general,
programmers view a variable as a known but varying quantity that
receives its value through direct assignments. *However, in the context
of constraints in AIMMS, the word variable denotes an unknown quantity.*
Constraints can be grouped together to form a system of simultaneous
equations and/or inequalities, which is referred to as a *mathematical
program*. Variables in a mathematical program are assigned values when a
solver (a solution algorithm) finds a solution for the unknowns in the
system.

.. rubric:: Similarity of parameters and variables

When used outside the scope of constraints and the solution of
mathematical programs, variables in AIMMS behave essentially the same as
parameters in AIMMS. Like parameters, variables can be initialized, used
as known quantities in assignment statements, and be referred to as data
from within the graphical user interface.

.. toctree::
   :maxdepth: 1

   variable-declaration-and-attributes
   constraint-declaration-and-attributes