.. _sec:nlp.presolve:

The AIMMS Presolver
===================

.. rubric:: The need for a presolver

Of all nonlinear solvers in AIMMS only a couple use (limited)
preprocessing techniques. Therefore, AIMMS itself has implemented a
presolve algorithm with the goal to reduce the size of the problem and
to tighten the variable bounds, which may help the solver to solve
nonlinear problems faster. Besides the BARON global solver, all
nonlinear solvers in AIMMS are local solvers, i.e. the solution found by
the solver is a local solution and cannot be guaranteed to be a global
solution. The presolve algorithm may help the solver in finding a better
solution. A local solver might sometimes fail to find a solution and
then it is often not clear whether that is caused by the problem being
infeasible or by the solver failing to find a solution for a feasible
problem. The presolve algorithm may reveal inconsistent constraints
and/or variable bounds and hence identify a problem as infeasible.

.. rubric:: Presolve techniques

Consider the following constrained nonlinear optimization problem:

.. math::

   \begin{align}
   & \text{minimize} & & f(x) \\
   & \text{subject to} & & g(x) \leq d & & \\
   &&& Ax \leq b & & \\ 
   &&& l\leq x \leq u & & \\ 
   \end{align}

The objective function :math:`f(x)` can either be linear or nonlinear,
while :math:`g(x)` is a nonlinear function. The AIMMS presolve algorithm
will (amongst others)

-  remove singleton rows by moving the bounds to the variables,

-  reduce variable bounds from linear and nonlinear constraints that
   contain bounded variables,

-  delete fixed variables,

-  remove one variable of a doubleton, and

-  delete redundant constraints.

A detailed description of each of these techniques can be found in
:cite:`bib:FG94`.

.. rubric:: Singleton rows

A singleton row is a linear constraint that contains only one variable.
An equality singleton row fixes the variable to the right-hand-side
value of the row, and unless this value conflicts with the current
bounds of the variable in which case the problem is infeasible, AIMMS
can remove both the row and variable from the problem. An inequality
singleton row introduces a new bound on the variable which can be
redundant, tighter than an existing bound in which case AIMMS will
update the bound, or infeasible. The AIMMS presolve algorithm will
remove all singleton rows.

.. rubric:: Deleting fixed variables

If a variable is fixed then sometimes another row becomes a singleton
row, and if that row is an equality row AIMMS can fix the remaining
variable and remove it from the problem. By repeating this process AIMMS
can solve any triangular system of linear equations that is part of the
problem.

.. rubric:: Bound reductions using linear constraints

The following analysis applies to a linear "less than or equal to"
constraint. A similar analysis applies to other constraint types. Assume
we have a linear constraint :math:`i` that originally has the form

.. math::
   :label: eq:nlp.row

       \sum_j a_{ij}x_j \leq b_i

Assuming that all variables in this constraint have finite bounds, we
can determine the following lower and upper limits on constraint
:math:`i`

.. math::
   :label: eq:nlp.lower

       \underline{b_i} = \sum_{j\in P_i} a_{ij}l_j + \sum_{j\in N_i} a_{ij}u_j

and

.. math::
   :label: eq:nlp.upper

       \overline{b_i} = \sum_{j\in P_i} a_{ij}u_j + \sum_{j\in N_i} a_{ij}l_j

where :math:`P_i = \{j \mid a_{ij} > 0\}` and
:math:`N_i = \{j \mid a_{ij} < 0\}` define the sets of variables with a
positive coefficient and negative coefficient in constraint :math:`i`
respectively.

.. rubric:: Bound analysis

By comparing the lower and upper limits of a constraint with the
right-hand-side value we obtain one of the following situations:

-  :math:`\underline{b_i} > b_i`: constraint :eq:`eq:nlp.row` cannot be
   satisfied and is infeasible.

-  :math:`\underline{b_i} = b_i`: constraint :eq:`eq:nlp.row` can only
   be satisfied if all variables in the constraint are fixed on their
   lower bound if they have a positive coefficient, or fixed on their
   upper bound if they have a negative coefficient. The constraint and
   all its variables can be removed from the problem.

-  :math:`\overline{b_i} \leq b_i`: constraint :eq:`eq:nlp.row` is
   redundant, i.e. will always be satisfied, and can be removed from the
   problem.

-  :math:`\underline{b_i} < b_i < \overline{b_i}`: constraint
   :eq:`eq:nlp.row` cannot be eliminated but can often be used to
   improve the bounds of one or more variables as we will see below.

If :math:`\underline{b_i} < b_i < \overline{b_i}`, then combining
:eq:`eq:nlp.row` with :eq:`eq:nlp.lower` gives the following bounds on a
variable :math:`k` in constraint :math:`i`:

.. math::
   :label: eq:nlp.upper-reduction

       x_k \leq l_k + (b_i - \underline{b_i})/a_{ik}\qquad\mbox{if $a_{ik} > 0$}

and

.. math::
   :label: eq:nlp.lower-reduction

       x_k \geq u_k + (b_i - \underline{b_i})/a_{ik}\qquad\mbox{if $a_{ik} < 0$}

If the upper bound given by :eq:`eq:nlp.upper-reduction` is smaller than
the current lower bound of variable :math:`k` then the problem is
infeasible. If it is smaller then the current upper bound of variable
:math:`k`, AIMMS will update the upper bound for variable :math:`k`.
Something similar holds for the lower bound as given by
:eq:`eq:nlp.lower-reduction`. Note that bounds
:eq:`eq:nlp.upper-reduction` and :eq:`eq:nlp.lower-reduction` can only
be derived if all bounds :math:`l_j` and :math:`u_j` in
:eq:`eq:nlp.lower` are finite. But also if exactly one of the bounds in
:eq:`eq:nlp.lower` is an infinite bound, AIMMS can still find an implied
bound for the corresponding variable.

.. rubric:: Bound reductions using nonlinear constraints

We can rewrite a nonlinear constraint :math:`g_i(x)\leq d_i` as

.. math::
   :label: eq:nlp.nonlin

       \sum_j a_{ij}x_i + h_i(y) \leq d_i

separating the linear variables :math:`x` in this constraint from the
nonlinear variables :math:`y`. As before, we can find lower and upper
limits on the linear part of the constraint, and again we denote them by
:math:`\underline{b_i}` and :math:`\overline{b_i}` respectively. For
this constraint we can derive the following upper bound on the nonlinear
term in :eq:`eq:nlp.nonlin`:

.. math::
   :label: eq:nlp.nonlin-reduced

       h_i(y) \leq d_i - \underline{b_i}

Note that if there are no linear terms in constraint :eq:`eq:nlp.nonlin`
then :math:`\underline{b_i} = 0`.

.. rubric:: Nonlinear analysis using expression trees

Nonlinear expressions in AIMMS are stored in an expression tree. By
going through the expression tree from the top node to the leafs we can
sometimes derive bounds on some of the variables in the expression. For
example, assume we have the constraint

.. math:: \sqrt{\ln x} \leq  2

with :math:`x` unbounded. It follows that the :math:`\ln x`
sub-expression should be in the range :math:`[0,4]` since
:math:`\sqrt{y}` is not defined for :math:`y<0`, which in turn implies
that :math:`x` should be in the range :math:`(1,e^4]`.

.. rubric:: Types of nonlinear analysis

AIMMS can analyze nonlinear expressions for various types of reductions,
and uses various types of techniques, such as:

-  operator domain analysis: reduce bounds on operator arguments by the
   implicit domains of operators such as :math:`\sqrt{x}` or
   :math:`\ln x`,

-  operator range analysis: compute the bounds of a nonlinear expression
   on the basis of known bounds on the argument(s) and use those bounds
   for further reductions, and

-  for invertible functions, compute bounds on operator arguments on the
   basis of bounds on a known operator range.

.. rubric:: Supported operators

The presolve algorithm can handle nonlinear expressions build up by the
operators listed in :ref:`this table <table:nlp.opr-presolve>`. If a nonlinear
constraint contains an operator that is not in this table then it will
be ignored by the presolve algorithm.

.. _table:nlp.opr-presolve:

.. table:: Operators used by the presolve algorithm

	+---------------------------------------------------------------------------------------------------------+
	| Operators                                                                                               |
	+=========================================================================================================+
	| :math:`\log_{10} x`, :math:`\ln x`, :math:`\exp x`, :math:`e^x`                                         |
	+---------------------------------------------------------------------------------------------------------+
	| :math:`x^a`, :math:`a^x` (:math:`a \neq 0`), :math:`x^y`                                                |
	+---------------------------------------------------------------------------------------------------------+
	| :math:`\sin x`, :math:`\cos x`, :math:`\tan x`, :math:`\arcsin x`, :math:`\arccos x`, :math:`\arctan x` |
	+---------------------------------------------------------------------------------------------------------+
	| :math:`x+y`, :math:`x-y`, :math:`x \cdot y`, :math:`x/y`                                                |
	+---------------------------------------------------------------------------------------------------------+

.. rubric:: Doubletons

If a problem contains a constraint of the form :math:`x = ay`,
:math:`a \neq 0`, then the variables :math:`x` and :math:`y` define a
doubleton. If the presolve algorithm detects a doubleton then it will
replace the variable :math:`x` by the term :math:`ay` in every
constraint in which :math:`x` appears, and remove the variable :math:`x`
from the problem. For some problems good initial values are given to the
variables. In case the initial value given to :math:`x` does not match
the initial value of :math:`y` according to the relationship
:math:`x = a   y`, it is unclear which initial value we should assign to
:math:`y`. Preliminary test results showed that in such a case it is
better not to remove the doubleton, and pass both variables to the
solver with their own initial value. This has become the default
behavior of our presolve algorithm regarding doubletons.

.. rubric:: The presolve algorithm

The AIMMS Presolver iteratively applies all reduction techniques
discussed above until no further reductions are available anymore, or an
iteration limit has been reached. Various options are available in the
**Solvers general - AIMMS presolver** section of the option tree to
steer the presolve algorithm. For instance a user can choose to only use
linear constraints for reducing bounds, or to not remove doubletons.

.. rubric:: Mixed integer programming problems

If the optimization problem contains binary variables then the AIMMS
Presolver can apply probing which is a technique that looks at the
logical implications of fixing a binary variable to 0 or 1. Probing can
be used to reduce more variables bounds, reformulate constraints or
improve coefficients. In some cases quadratic constraints containing
binary variables can be reformulated as linear constraints. Coefficient
improvement is a process of improving the coefficients of the binary
variables such that the relaxation becomes more tight. A detailed
description of probing and coefficient improvement can be found in
:cite:`bib:Sa94`.

.. rubric:: Successes may vary

The benefits of using the AIMMS Presolver may vary from model to model.
The solution of presolved NLPs may become better or worse compared to
the original NLP. Presolving may change infeasible NLPs to feasible
problems for a given starting point, or vice versa. Also, presolving may
make the model more degenerate and harder to solve. Finaly, for
eliminated constraints and variables dual information is lost, and AIMMS
makes no effort yet to recover the lost dual information, as this may be
very hard in the presence of nonlinear reductions.