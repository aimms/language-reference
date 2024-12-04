.. _chap:nlp:

Advanced Methods for Nonlinear Programs
=======================================

.. rubric:: Problems of nonlinear programs

For non-convex nonlinear mathematical programs (NLPs), nonlinear solvers
have no guarantee of returning the global optimum. Due to the local
search algorithms employed by nonlinear solvers, their solution process
depends on the starting point provided by the user. Nonlinear solvers
can, therefore, easily end up in, non-unique, local optima, or, even
worse, may not even find a feasible solution for a given starting point.

.. rubric:: How to counteract?

To counteract these facts, a number of possible actions can be taken.

-  Use a global solver, such as BARON or Gurobi, to solve the NLP. Global solvers,
   however, usually only work well on relatively small NLP problems.

-  Use a multistart algorithm to solve the NLP problem for multiple
   starting points in order to have a better chance to find the global
   optimum.

-  Use the AIMMS Presolver to reduce the problem size and tighten the
   bounds of the remaining variables and constraints of the NLP. This
   will reduce the space which the nonlinear solver needs to search in
   order to find an optimal solution.

.. rubric:: This chapter

This chapter discusses the presolve techniques for nonlinear programs
available in AIMMS. The chapter also discusses the multistart algorithm
built into AIMMS. Using the multistart algorithm will increase the total
solution time, but, in general, will also improve the solution found by
nonlinear solvers.

.. toctree::
   :maxdepth: 1

   the-aimms-presolver
   the-aimms-multistart-algorithm
   control-parameters-that-influence-the-multistart-algorithm