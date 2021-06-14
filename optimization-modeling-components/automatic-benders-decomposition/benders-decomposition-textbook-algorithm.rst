.. _sec:benders.textbook.alg:

Benders' Decomposition - Textbook Algorithm
===========================================

.. rubric:: Master problem

The basic Benders' decomposition algorithm as explained in several
textbooks (e.g., :cite:`bib:NW88`, :cite:`bib:Ma99`) works as follows. After
introducing an artificial variable :math:`\eta = d^Ty`, the master
problem relaxation becomes:

.. math::

   \begin{align}
   & \text{minimize} & & c^Tx + \eta \\
   & \text{subject to} & & A x \leq b & & \\
   &&& \eta \geq \overline{\eta} & & \\ 
   &&& x \in \mathbb{Z}^n_+ & & \\ 
   \end{align}

Here :math:`\overline{\eta}` is a lower bound on the variable
:math:`\eta` that AIMMS will automatically derive. For example, if the
vector :math:`d` is nonnegative then we know that 0 is a lower bound on
:math:`d^Ty` since we assumed that the variable :math:`y` is
nonnegative, and therefore we can take :math:`\overline{\eta} = 0`. We
assume that the master problem is bounded.

.. rubric:: Subproblem

After solving the master problem we obtain an optimal solution, denoted
by :math:`(x^*,\eta^*)` with :math:`x^*` integer. This solution is fixed
in the subproblem which we denote by :math:`PS(x^*)`:

.. math::

   \begin{align}
   & \text{minimize} & & d^Ty \\
   & \text{subject to} & & Q y \leq r - Tx^* & & \\
   &&& y \in \mathbb{R}^m_+ & & \\ 
   \end{align}

Note that this subproblem is a linear programming problem in which the
continuous variable :math:`y` is the only variable.

.. rubric:: Dual subproblem

Textbooks that explain Benders' decomposition often use the dual of this
subproblem because duality theory plays an important role, and the
Benders' optimality and feasibility cuts can be expressed using the
variables of the dual problem. The dual of the subproblem
:math:`PS(x^*)` is given by:

.. math::

   \begin{align}
   & \text{maximize} & & r - \pi^T(Tx^*) \\
   & \text{subject to} & & \pi^TQ \geq d^T & & \\
   &&& \pi \geq 0 & & \\ 
   \end{align}

We denote this problem by :math:`DS(x^*)`.

.. rubric:: Optimality cut

If this subproblem is feasible, let :math:`z^*` denote the optimal
objective value and :math:`\overline{\pi}` an optimal solution of
:math:`DS(x^*)`. If :math:`z^* \leq \eta^*` then the current solution
:math:`(x^*,\eta^*)` is a feasible and optimal solution of our original
problem, and the Benders' decomposition algorithm only needs to solve
:math:`PS(x^*)` to obtain optimal values for variable :math:`y`. If
:math:`z^* > \eta^*` then the Benders' optimality cut
:math:`\eta \geq \overline{\pi}^T (r - Tx)` is added to the master
problem and the algorithm continues by solving the master problem again.

.. rubric:: Feasibility cut

If the dual subproblem is unbounded, implying that the primal subproblem
is infeasible, then an unbounded extreme ray :math:`\overline{\pi}` is
selected and the Benders' feasibility cut
:math:`\overline{\pi}^T (r - Tx) \leq 0` is added to the master problem.
Modern solvers like CPLEX and Gurobi can provide an unbounded extreme
ray in case a LP problem is unbounded. After adding the feasibility cut
the Benders' decomposition algorithm continues by solving the master
problem.