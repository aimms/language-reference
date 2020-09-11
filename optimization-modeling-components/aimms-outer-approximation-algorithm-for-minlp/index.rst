.. _ch:aoa:

AIMMS Outer Approximation Algorithm for MINLP
=============================================

.. _AIMMS_Outer_Approximation:

.. rubric:: Open solver approach

Outer approximation (see :cite:`bib:DG86`) is a basic approach for solving
**M**\ ixed-**I**\ nteger **N**\ on\ **L**\ inear **P**\ rogramming
(MINLP) models. The underlying algorithm is an interplay between two
solvers, one for solving mixed-integer linear models and one for solving
nonlinear models. Even though the standard outer approximation algorithm
is provided with AIMMS, you as an algorithmic developer may want to
customize the individual steps in order to obtain better performance
and/or a better solution for your particular model.

.. rubric:: The AIMMS Outer Approximation algorithm

The outer approximation algorithm in AIMMS is, therefore, provided as a
customizable procedure written in the AIMMS language itself using
functions and procedures provided by the GMP library (a white box
solver), whereas most other outer approximation solvers are provided as
a closed implementation (a black box solver). The outer approximation
algorithm in AIMMS is implemented as a system module with the name
``GMP Outer Approximation``. You can install this module using the
**Install System Module** command in the AIMMS **Settings** menu. In the
remainder of this chapter, we will refer to the outer approximation
algorithm as **A**\ IMMS **O**\ uter **A**\ pproximation (AOA).

.. rubric:: Convex algorithm

Besides the basic algorithm, the AOA module also implements the
Quesada-Grossmann algorithm (see :cite:`bib:QG92`) which is designed to solve
convex MINLP models. The basic algorithm can also be used to solve
convex models but the Quesada-Grossmann algorithm is often more
efficient.

.. rubric:: This chapter

In this chapter you find the description of, and the motivation behind,
the open approach to solving MINLP models based on outer approximation.
We continue with a brief introduction to the problem statement and the
basic algorithm. Next we explain how the AOA algorithm can be setup,
followed by a detailed explanation of the parameters inside the AOA
module that can be used to control the outer approximation algorithm. We
then describe the Quesada-Grossmann algorithm for convex MINLP models.
Next we describe an initial implementation of the basic solution
algorithm using procedures in the AIMMS language is described. These
procedures use functions that are especially designed to support the
open approach. The chapter concludes with suggestions on additional ways
to vary the individual steps of the overall algorithm in order to obtain
customized versions of the outer approximation algorithm.

.. toctree::
   :maxdepth: 1

   problem-statement
   basic-algorithm
   using-the-aoa-algorithm
   control-parameters-that-influence-the-aoa-algorithm
   the-quesada-grossmann-algorithm
   a-first-and-basic-implementation
   alternative-uses-of-the-open-approach