Problem Statement
=================

.. rubric:: MINLP

The mixed-integer nonlinear programming models to be solved can be
expressed as follows.

**Minimize:**

.. math:: f(x,y)

**Subject to:**

.. math::

   \begin{aligned}
   h(x,y)     & =    & 0 \\
   g(x,y)     & \leq & 0 \\
   C y + D x  & \leq & d \\
   x \in {\cal X} & = & \{ x \in \mathbb{R}^n | x^L \leq x \leq x^U \} \\
   y \in {\cal Y} & = & \mathbb{Z}^m\end{aligned}

.. rubric:: Usual assumption

The usual assumption is that the nonlinear subproblem (i.e. the model in
which all integer variables are fixed) is convex. This assumption is to
guarantee that each locally optimal solution of the nonlinear subproblem
is also a globally optimal solution. In practice this assumption does
not always hold, but the algorithm can still be applied. Convergence to
a global optimum of the MINLP using the outer approximation algorithm is
then no longer guaranteed.