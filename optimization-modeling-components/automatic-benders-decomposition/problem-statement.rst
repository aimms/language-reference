.. _sec:benders.problem.statement:

Problem Statement
=================

.. rubric:: MIP

We consider the following generic mixed-integer programming model to
explain Benders' Decomposition. (The notation used is similar to
:cite:`bib:FSZ10`.)

.. math::

   \begin{align}
   & \text{minimize} & & c^Tx + d^Ty \\
   & \text{subject to} & & A x \leq b & & \\
   &&& T x + Q y \leq r & & \\ 
   &&& x \in \mathbb{Z}^n_+ & & \\ 
   &&& y \in \mathbb{R}^m_+ & & \\ 
   \end{align}

The variable :math:`x` is integer and the variable :math:`y` is
continuous. The matrix :math:`T` may contain empty constraints but we
assume that the matrix :math:`Q` does not contain any empty constraint.
So, the model can have constraints that only contain continuous
variables.

.. rubric:: Limitation

Benders' Decomposition cannot be used if the model contains only integer
variables. If the number of continuous variable is small compared to the
number of integer variables then Benders' Decomposition will very likely
be inefficient.