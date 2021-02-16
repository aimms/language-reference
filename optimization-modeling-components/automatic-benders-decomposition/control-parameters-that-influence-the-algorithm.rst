.. _sec:benders.control.par:

Control Parameters That Influence the Algorithm
===============================================

.. rubric:: This section

Some of the control parameters of :ref:`this table <table:benders.controlparam>`
can be used to influence the behavior of the Benders' decomposition
algorithm. We discuss these parameters in this section.

.. _sec:benders.primaldual.sub:

Primal Versus Dual Subproblem
-----------------------------

.. rubric:: Parameter ``UseDual``

In the textbook algorithm the dual of the subproblem is used. It is also
possible to use the primal of the subproblem instead. This is controlled
by the parameter ``UseDual``. By default the Benders' decomposition
algorithm uses the primal subproblem.

.. rubric:: Dual solution

If the primal subproblem is solved and it appears to be feasible then
the dual solution is used to construct an optimality cut. By the dual
solution we mean the shadow prices of the constraints and the reduced
costs of the variables in the primal subproblem.

.. rubric:: Feasibility problem

If the primal subproblem is infeasible then another problem is solved to
find a solution of minimum infeasibility (according to some
measurement). The *feasibility problem* of :math:`PS(x^*)` (see
:ref:`sec:benders.textbook.alg`) is denoted by :math:`PFS(x^*)` and
defined by:

.. math::

   \begin{align}
   & \text{minimize} & & z \\
   & \text{subject to} & & Q y - z \leq r - Tx^* & & \\
   &&& y \in \mathbb{R}^m_+ & & \\ 
   &&& z \in \mathbb{R} & & \\ 
   \end{align}

Here :math:`z` is a scalar variable. The dual solution of this
feasibility problem is used to create a feasibility cut which is added
to the master problem.

.. rubric:: Alternative feasibility problem

The feasibility problem above minimizes the maximum infeasibility among
all constraints. It is also possible to minimize the sum of
infeasibilities over all constraints; this is controlled by the
parameter ``UseMinMaxForFeasibilityProblem`` which we discuss in
:ref:`sec:benders.feas.mode`. Also the parameter ``NormalizationType``
influences the formulation of the feasibility problem; see
:ref:`sec:benders.normalization`. Note that the feasibility problem is
always feasible and bounded. Note further that if the optimal objective
value of the feasibility problem is 0 or negative then the corresponding
subproblem is feasible.

.. rubric:: Relationship with parameter ``FeasibilityOnly``

In the next subsection we discuss the parameter ``FeasibilityOnly``.
This parameter has a big influence on how the subproblem is created, for
both the primal and dual subproblem. In some cases the subproblem can
become a pure feasibility problem.

.. _sec:benders.feas.prob:

Subproblem as Pure Feasibility Problem
--------------------------------------

.. rubric:: Until now

By so far we assumed that the Benders' decomposition algorithm first
tries to solve the subproblem to optimality to either conclude that the
combined solution of the master problem and subproblem forms an optimal
solution for the original problem, or to create an optimality cut that
is added to the master problem. If the primal or dual subproblem appears
to be infeasible or unbounded respectively, then a feasibility problem
is solved (if we used the primal subproblem) or an unbounded extreme ray
is calculated (if we used the dual subproblem) to create a feasibility
cut.

.. rubric:: Benders' subproblem always infeasible

For some problems the Benders' subproblem will (almost) always be
infeasible unless an optimal solution of the original problem is found.
For example, assume that the variables that become part of the
subproblem have no objective coefficients. (In the MIP problem of
:ref:`sec:benders.problem.statement` this is equivalent to the vector
:math:`d` being equal to 0.) In that case the Benders' decomposition
algorithm tries to find a solution for the master problem that remains
feasible if we also consider the part of the model that became the
subproblem. The algorithm is finished if such a solution is found. Until
then all subproblems will be infeasible. In that case it is useless to
try to solve the subproblem to optimality (which will always fail) but
instead directly solve a feasibility problem for the subproblem.

.. rubric:: Reformulation

It is possible to let the AIMMS automatically reformulate the original
problem such that the variables that become part of the subproblem have
no longer objective coefficients. (This reformulation exists only
temporary while the function :any:`GMP::Benders::CreateMasterProblem` is
executed; the user will not notice anything inside his project.) For the
MIP problem of :ref:`sec:benders.problem.statement` the reformulated
problem becomes:

.. math::

   \begin{align}
   & \text{minimize} & & c^Tx + \eta \\
   & \text{subject to} & & d^Ty - \eta \leq 0 & & \\
   &&& A x \leq b & & \\ 
   &&& T x + Q y \leq r & & \\ 
   &&& x \in \mathbb{Z}^n_+ & & \\ 
   &&& y \in \mathbb{R}^m_+ & & \\ 
   &&& \eta \in \mathbb{R} & & \\ 
   \end{align}

If we assign the new continuous variable :math:`\eta`, together with the
integer variable :math:`x`, to the master problem then the subproblem
variables no longer have objective coefficients. As a consequence, the
subproblem will always be infeasible (unless an optimal solution is
found).

.. rubric:: Parameter ``FeasibilityOnly``

The parameter ``FeasibilityOnly`` can be used to control whether AIMMS
should reformulate the original problem as explained above. AIMMS will
do so if the value of this parameter equals 1, which is the default
value. Also, if parameter ``FeasibilityOnly`` equals 1 then the Benders'
decomposition algorithm will no longer solve the primal subproblem
before solving the feasibility problem. Instead it will directly solve
the feasibility problem.

.. rubric:: Primal subproblem

After reformulating the original problem, the primal of the subproblem
will be different from :math:`PS(x^*)` of
:ref:`sec:benders.textbook.alg`, namely:

.. math::

   \begin{align}
   & \text{minimize} & & 0 \\
   & \text{subject to} & & d^Ty \leq \eta^* & & \\
   &&& Q y \leq r - Tx^* & & \\ 
   &&& y \in \mathbb{R}^m_+ & & \\ 
   \end{align}

We denote this primal subproblem by :math:`PS'(x^*,\eta^*)`. The
feasibility problem will also become slightly different, as compared to
:math:`PFS(x^*)` of :ref:`sec:benders.primaldual.sub`, namely:

.. math::

   \begin{align}
   & \text{minimize} & & z \\
   & \text{subject to} & & d^Ty - z \leq \eta^* & & \\
   &&& Q y - z \leq r - Tx^* & & \\ 
   &&& y \in \mathbb{R}^m_+ & & \\ 
   &&& z \in \mathbb{R} & & \\ 
   \end{align}

We denote this feasibility problem by :math:`PFS'(x^*,\eta^*)`. If the
optimal objective value of this feasibility problem is 0 or negative
then we have found an optimal solution for the original problem, and the
Benders' decomposition algorithm terminates. Otherwise the dual solution
of the feasibility problem is used to add a feasibility cut to the
master problem, and the algorithm continues by solving the master
problem.

.. rubric:: Dual subproblem

We have seen before that if we use the dual of the subproblem and
parameter ``FeasibilityOnly`` equals 0 then the Benders' decomposition
algorithm will first solve the dual subproblem and, if that subproblem
is infeasible, use an unbounded extreme ray to create a feasibility cut.
If parameter ``FeasibilityOnly`` equals 1 then the algorithm follows a
different route. Consider the dual formulation of the above problem, the
feasibility problem for :math:`PS'(x^*,\eta^*)`:

.. math::

   \begin{align}
   & \text{maximize} & & \pi^T(r - Tx^*) + \pi_0 \eta^* \\
   & \text{subject to} & & \pi^TQ + \pi_0 d^T \geq 0 & & \\
   &&& 1^T \pi + \pi_0 = 1 & & \\ 
   &&& \pi, \pi_0 \geq 0 & & \\ 
   \end{align}

Here :math:`1^T` denotes a vector of all 1's. We denote this problem by
:math:`DS'(x^*,\eta^*)`. This problem is always feasible and bounded.
The Benders' decomposition algorithm uses this problem as the (dual)
subproblem if the parameters ``FeasibilityOnly`` and ``UseDual`` equal
1. If the optimal objective value of this problem is 0 or negative then
we have found an optimal solution for the original problem, and the
Benders' decomposition algorithm terminates. Otherwise the solution of
this problem is used to add a feasibility cut to the master problem, and
the algorithm continues by solving the master problem.

.. rubric:: Disadvantage

A serious disadvantage of reformulating the problem, as done in this
section, is that a first feasible solution (which will be optimal) for
the original problem will be found just before the Benders'
decomposition algorithm terminates. This means that the "gap" between
the lower and upper bound on the objective value is meaningless, and
therefore this measurement of progress toward finding and proving
optimality by the algorithm is not available. However, this disadvantage
only occurs when using the classic Benders' decomposition algorithm. For
the modern approach in which only a single MIP problem is solved, see
:ref:`sec:benders.modern.impl`, the algorithm finds feasible solutions
for the original problem during the solution process and therefore the
"gap" exists.

.. _sec:benders.normalization:

Normalization of Feasibility Problem
------------------------------------

.. rubric:: Normalization

In the previous subsection we introduced the dual subproblem
:math:`DS'(x^*,\eta^*)` which contains the normalization condition

.. math::
   :label: eq:benders.norm.cond1

   \begin{align}
   1^T \pi + \pi_0 = 1. \tag{NC1}
   \end{align}

In order to obtain better feasibility cuts, Fischetti et al. (in
:cite:`bib:FSZ10`) proposed another normalization condition. The matrix
:math:`T` often contains null constraints which correspond to
constraints that do not depend on :math:`x`. These are "static"
conditions in the subproblem that are always active. According to
Fischetti et al. there is no reason to penalize the corresponding dual
multiplier :math:`\pi_i`. The new normalization condition then becomes

.. math::
   :label: eq:benders.norm.cond2

   \begin{align}
   \sum_{i\in I(T)} \pi_i + \pi_0 = 1 \tag{NC2}
   \end{align}

where :math:`I(T)` indexes the nonzero constraints of matrix :math:`T`.

.. rubric:: Parameter ``NormalizationType``

The parameter ``NormalizationType`` controls which normalization
condition is used. If it equals 0 then normalization condition
:eq:`eq:benders.norm.cond1` is used, else :eq:`eq:benders.norm.cond2`.
The Benders' decomposition algorithm uses :eq:`eq:benders.norm.cond2` by
default because various computational experiments showed a better
performance with this normalization condition.

.. rubric:: Translation to primal subproblem

We can apply the normalization rule of Fischetti et al. also if we use
the primal subproblem. In the corresponding feasibility problem, we then
only add variable :math:`z` for the nonzero rows of :math:`T`. The
relevant constraints in :math:`PFS'(x^*,\eta^*)` then become:

.. math::

   \begin{align}
   (Q y)_i - z_i & \leq r_i - (Tx^*)_i & & i \in    I(T) \\
   (Q y)_i & \leq r_i & & i \notin I(T) \\
   \end{align}

The feasibility problem can be normalized in this way regardless of the
setting of parameter ``FeasibilityOnly``.

.. rubric:: Exception

In case the parameter ``UseDual`` equals 1 and the parameter
``FeasibilityOnly`` equals 0 then no feasibility problem is solved to
derive a feasibility cut. Instead an unbounded extreme ray for the
unbounded dual subproblem is used. Therefore, in that case the parameter
``NormalizationType`` is ignored.

.. _sec:benders.feas.mode:

Feasibility Problem Mode
------------------------

.. rubric:: Parameter ``UseMinMaxForFeasibilityProblem``

The parameter ``UseMinMaxForFeasibilityProblem`` determines what kind of
infeasibility is minimized: the maximum infeasibility among all
constraints (value 1, the default) or the sum of infeasibilities over
all constraints (value 0). If the sum of the infeasibilities over all
constraints is used then also the normalization rule of Fischetti et al.
can be used, as controlled by the parameter ``NormalizationType``. This
parameter is ignored if the parameter ``UseDual`` equals 1.

.. _sec:benders.tight.cons:

Tightening Constraints
----------------------

.. rubric:: Illustrative example

If the Benders' master problem is created, using the function
:any:`GMP::Benders::CreateMasterProblem`, then AIMMS can try to
automatically add valid constraints to the master problem that will cut
off some infeasible solutions. This is best illustrated by the following
MIP example.

.. math::

   \begin{align}
   & \text{minimize} & & \sum_i x_i \\
   & \text{subject to} & & y_i \leq u_i x_i & & \forall i \\
   &&& \sum_i y_i \geq b & & \\ 
   &&& x \in \{0,1\} & & \\ 
   &&& y \geq 0 & & \\ 
   \end{align}

We assume that :math:`u` and :math:`b` are strictly positive parameters.
The binary variable :math:`x` is assigned to the master problem and the
continuous variable :math:`y` to the subproblem. For this example, the
initial master problem has no constraints (besides the integrality
restriction on :math:`x`) and therefore :math:`x=0` is the optimal
solution of the initial master problem. Clearly, for :math:`x=0` our MIP
example has no solution. Adding the constraint

.. math::

   \begin{align}
   \sum_i u_i x_i & \geq b & &  \\
   \end{align}

to the master problem cuts off the :math:`x=0` solution. Note that this
constraint is redundant in the original MIP example. By adding these
kind of master-problem-tightening constraints we hope that the Benders'
decomposition algorithm requires less iterations to find an optimal
solution.

.. rubric:: Parameter ``AddTighteningConstraints``

Adding tightening constraints to the master problem is controlled by the
parameter ``AddTighteningConstraints``. If this parameter equals 1, its
default, then AIMMS will try to find and add tightening constraints.
Computational experiments indicate that in general the Benders'
decomposition algorithm benefits from adding these tightening
constraints.

.. _sec:benders.start.point:

Using a Starting Point
----------------------

.. rubric:: Parameter ``UseStartingPointForMaster``

The parameter ``UseStartingPointForMaster`` can be used to let the
classic Benders' decomposition algorithm start from a "good" solution.
This solution can be obtained from a heuristic and must be a feasible
solution for the master problem. The solution should be copied into the
level suffix of the problem variables before the Benders' decomposition
algorithm is called. If this parameter is set to 1 then the algorithm
will skip the solve of the first master problem. Instead, the master
problem variable :math:`x^*` will be fixed in the subproblem
:math:`PS(x^*)` according to the starting point, and the algorithm will
continue by solving the subproblem.

.. _sec:benders.aimms.presolver:

Using the AIMMS Presolver
-------------------------

.. rubric:: Parameter ``UsePresolver``

The Benders' decomposition algorithm can use the AIMMS Presolver at the
start. In that case the algorithm will use the preprocessed model
instead of the original model. By preprocessing the model it might
become smaller and easier to solve. The parameter ``UsePresolver`` can
be used to switch on the preprocessing step.