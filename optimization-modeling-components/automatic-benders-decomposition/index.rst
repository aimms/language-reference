.. _ch:benders:

Automatic Benders' Decomposition
================================

.. _Automatic_Benders:

.. rubric:: Important note

The solver CPLEX has its own implementation of the Benders'
decomposition algorithm. An important difference is that the algorithm
in CPLEX supports multiple subproblems. CPLEX allows you to specify the
decomposition by assigning the variables to the master problem or a
subproblem by using the procedure :any:`GMP::Column::SetDecomposition`. For
more information see the CPLEX option ``Benders_strategy``.

.. rubric:: Introduction

Benders' decomposition, introduced by Jacques F. Benders in 1962
(:cite:`bib:Be62`), is an algorithm that decomposes a problem into two simpler
parts. The first part is called the master problem and solves a relaxed
version of the problem to obtain values for a subset of the variables.
The second part is often called the subproblem (or slave problem or
auxiliary problem) and finds values for the remaining variables fixing
the variables of the master problem. If the problem contains integer
variables then typically they become part of the master problem while
the continuous variables become part of the subproblem.

.. rubric:: Cuts

The solution of the subproblem is used to cut off the solution of the
master problem by adding one or more constraints ("cuts") to the master
problem. This process of iteratively solving master problems and
subproblems is repeated until no more cuts can be generated. The
combination of the variables found in the last master problem and
subproblem iteration forms the solution to the original problem.

.. rubric:: Reduced solution times possible

For particular optimization problems, Benders' decomposition may lead to
a good, or even the optimal, solution in relatively few iterations. In
such cases, employing Benders' decomposition results in drastically
reduced solution times compared to solving the original problem. For
other problems, however, the progress per iteration is so small that
there is no positive, or even an adversary, effect by applying Benders'
decomposition. Upfront, it is hard predict whether or not there will be
positive effects for your particular model.

.. rubric:: Hard to implement manually

Implementing Benders' decomposition from scratch for a particular
problem is a non-trivial and error-prone task. Because duality theory
plays an important role, the process often involves explicitly working
out the dual formulation of the subproblem-and keeping it up-to-date
when you make changes to the original problem. Given the uncertainty
whether Benders' decomposition will lead to an improvement in solution
times at all, a manual implementation may not be a prospect to look
forward to.

.. rubric:: Automatic Benders' decomposition in AIMMS

For AIMMS, on the other hand, generating the master and slave problems
in an automated fashion is a fairly straightforward task, given a
generated mathematical program and the collection of variables that
should go into the master problem. With such an automated scheme,
verifying whether your particular model will benefit from Benders'
decomposition becomes completely trivial. With just a few lines of code,
and simply re-solving your model you will get immediate insight into the
benefits of Benders' decomposition for your model.

.. rubric:: Classical versus modern

The Benders' decomposition module in AIMMS implements both the classical
Benders' decomposition algorithm and a modern version. By the classical
approach we mean the algorithm described above that solves an
alternating sequence of master problems and subproblems, and that, in
principle, will work for any problem type. The modern approach will only
work for problems containing integer variables. In the modern approach,
the algorithm will solve only a *single* master MIP problem, where
subproblems are solved whenever the MIP solver finds a solution for the
master problem, using callbacks provided by modern MIP solvers.

.. rubric:: Several algorithms

Besides the classical and the modern algorithm, the Benders'
decomposition module in AIMMS also implements a two phase algorithm that
solves a relaxed problem in the first phase and the original problem in
the second phase. In addition, the module offers you the flexibility to
solve the subproblem as a primal or dual problem, to normalize the
subproblem to get better feasibility cuts, and so on.

.. rubric:: Limitations of current implementation

Benders' decomposition in AIMMS can be used for solving Mixed-Integer
Programming (MIP) problems and Linear Programming (LP) problems.
Currently it cannot be used to solve nonlinear problems. Also, the
current implementation does not support multiple subproblems which could
be efficient in case the subproblem has a block diagonal structure. This
implies that the current implementation cannot be used to solve (two
stage) stochastic programming problems with a subproblem for each
scenario.

.. rubric:: Open algorithm

Benders' decomposition in AIMMS is implemented as a system module with
the name ``GMP Benders Decomposition``. You can install this module
using the **Install System Module** command in the AIMMS **Settings**
menu. The Benders' decomposition algorithms are implemented in the AIMMS
language. Some supporting functions that are computationally difficult,
or hard to express in the AIMMS language, have been added to the GMP
library in support of the Benders' decomposition algorithm. Besides this
small number of fixed subtasks, the implementation is an open algorithm;
you as an algorithmic developer may want to customize the individual
steps in order to obtain better performance and/or a better solution for
your particular problem.

.. rubric:: This chapter

This chapter starts with a quick start for using Benders' decomposition
in AIMMS for those already familiar with Benders' decomposition.
Following a brief introduction to the problem statement, we discuss the
Benders' decomposition algorithm as it can be found in several
textbooks. Next we describe the implementation of the classic Benders'
decomposition algorithm using procedures in the AIMMS language that are
especially designed to support the open approach. This section is
important for users that want to modify the algorithm. Next, we discuss
in detail the parameters inside the Benders' module that can be used to
control the Benders' decomposition algorithm. We continue by describing
the implementation of a modern Benders' decomposition algorithm. The
chapter ends by introducing a two phase algorithm that solves a problem
by using information gathered while solving a relaxed version of the
problem, and we also describe its implementation.

.. toctree::
   :maxdepth: 1

   quick-start-to-using-benders-decomposition
   problem-statement
   benders-decomposition-textbook-algorithm
   implementation-of-the-classic-algorithm
   control-parameters-that-influence-the-algorithm
   implementation-of-the-modern-algorithm
   implementation-of-the-two-phase-algorithm