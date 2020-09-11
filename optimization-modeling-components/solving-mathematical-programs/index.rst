.. _chap:mp:

Solving Mathematical Programs
=============================

.. rubric:: Mathematical program components

A *mathematical program* consists of

-  a set of unknowns to be determined,

-  a collection of constraints that has to be satisfied, and

-  an (optional) objective function to be optimized.

The aim of a mathematical program is to find a solution with the aid of
a solver such that the objective function assumes an optimal
(i.e. minimal or maximal) value.

.. rubric:: Different types

Depending on the characteristics of the variables and constraints, a
mathematical program in AIMMS can be classified as one of the following.

-  If the objective function and all constraints contain only linear
   expressions (in terms of the variables), and all variables can assume
   continuous values within their ranges, then the program is a *linear*
   program.

-  If some of the variables in a linear program can assume only integer
   values, then the program is a *linear mixed integer* program.

-  If the objective is a quadratic function in terms of the variables
   while the constraints are linear, then the program is a *quadratic*
   program.

-  If the objective is neither linear nor quadratic, or some of the
   constraints contain nonlinear expressions, the program is a
   *nonlinear* program.

AIMMS will automatically call the appropriate solver to find an
(optimal) solution.

.. rubric:: This chapter

This chapter first discusses the declaration of a mathematical program,
together with auxiliary functions that you can use to specify its set of
variables and constraints. The ``SOLVE`` execution statement needed to
solve any type of mathematical program is presented, and, finally,
AIMMS' capabilities to help resolve infeasibilities in your model are
discussed.

.. toctree::
   :maxdepth: 1

   mathematicalprogram-declaration-and-attributes
   suffices-and-callbacks
   the-solve-statement
   infeasibility-analysis