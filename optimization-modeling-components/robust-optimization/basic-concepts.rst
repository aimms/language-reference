.. _sec:robust.concepts:

Basic Concepts
==============

.. rubric:: Basic concepts

In this section you will find a number of basic concepts that are
commonly used in robust optimization. They will help you to
unambiguously understand the robust optimization facilities in AIMMS.

.. rubric:: Robust counterpart

In robust optimization the model with uncertain data is translated into
the so-called *robust counterpart*. Consider the following linear
programming problem:

.. math::
   :label: eq:robust.P

   \begin{align}
   \max \{c^{T}x: A^{T}x\leq b\} \tag{P}
   \end{align}

in which :math:`c\in \mathbb{R}^m`, :math:`b\in \mathbb{R}^n` and
:math:`A\in \mathbb{R}^{m\times n}`. Suppose that the actual technology
matrix :math:`A` is in fact uncertain and it is only known to belong to
a bounded uncertainty set :math:`U_A\subset\mathbb{R}^{m\times n}`.
Similarly assume that right hand side :math:`b` belongs to an
uncertainty set :math:`U_b\subset\mathbb{R}^n`, and the objective
coefficients :math:`c` to an uncertainty set
:math:`U_c\subset\mathbb{R}^m`. The robust counterpart
:eq:`eq:robust.RC` for the nominal problem :eq:`eq:robust.P` is then
defined as follows:

.. math::
   :label: eq:robust.RC

   \begin{align}
   \max \{c^{T}x:A^{T}x\leq b,\,\forall A\in U_A, c\in U_c, b\in U_b\}. \tag{RC}
   \end{align}

.. rubric:: Uncertainty set

The sets :math:`U_A`, :math:`U_c` and :math:`U_b` specify all possible
realizations of the uncertain data and are collectively called the
*uncertainty set*. The main questions associated with the uncertainty
set are:

-  When and how can the robust counterpart of an uncertain problem be
   reformulated as a computationally tractable optimization problem?

-  How to specify a reasonable uncertainty set, i.e., meaningful for a
   particular application and yielding a tractable robust counterpart?

It can be shown that when the uncertainty set is a multi-dimensional
interval or described by linear constraints, then the robust counterpart
can be reformulated as a linear problem. Furthermore, when the
uncertainty set is an ellipsoid, then the robust counterpart is still
tractable, i.e., it can be reformulated as a second-order cone program
(SOCP), for which efficient (polynomial time) solution methods exist.
The reformulation of the robust counterpart is an automated process
performed by AIMMS during the generation of your mathematical program.

.. rubric:: Integer programming

If the uncertainty set is a multi-dimensional interval or described by
linear constraints, then the robust counterpart of a mixed-integer
robust optimization problem can also be reformulated as a mixed-integer
optimization problem. If the uncertainty set is described by ellipsoidal
constraints then the robust counterpart becomes a mixed-integer
second-order cone program. This class of problems is more difficult to
solve than mixed-integer optimization problems.

.. rubric:: Scenarios

A special situation to consider is when the uncertainty set consists of
a finite number of points representing a collection of scenarios. This
discrete case resembles the situation in multi-stage stochastic
programming with discrete data realizations. More precisely, in this
case hard constraints are imposed for every scenario :math:`s`, while
the objective is to optimize a worst-case performance measure with
respect to the set of scenarios. This performance measure can be, for
example, the objective value of the original (deterministic) model
associated with an uncertain scenario. Another possibility is to define
this performance measure as a deviation of the objective for a decision
with respect to the absolutely optimal objective for each scenario. In
the latter case, the optimal robust solution will be the one with the
minimum maximum deviation across scenarios.

.. rubric:: Chance constraints

Another manner to account for uncertainty into your model is by
specifying so-called *chance constraints*. In order to introduce chance
constraints, you have to declare some of the parameters in your model to
take random values from a distribution with given characteristics.
Subsequently, you can specify that some of the constraints in your model
be satisfied with a given probability with respect to the specified data
distributions. For example, if a chance constraint has a probability of
95%, this means that the constraint should be satisified for (at least)
95% of the realizations drawn from specified distributions of the random
parameters contained in it. Compared to using uncertain parameters,
specifying random parameters with the same range and formulating the
existing constraints as chance constraints may lead to solutions that
put less emphasis on worst-case scenarios that only occur occasionally.

.. rubric:: Multistage optimization

All decision variables in problem :eq:`eq:robust.P` represent "here and
now" decisions; they get specific numerical values as a result of
solving the problem before the actual data "reveals itself" and as such
are independent of the actual values of the data. There are situations
where this is too restrictive, since "in reality" some of the decision
variables can adjust themselves, to some extent, to the true values of
the uncertain data.

.. rubric:: Adjustable variables

For that reason, it is possible to specify both *non-adjustable* and
*adjustable* variables in AIMMS, similar to first-stage and second-stage
(or multi-stage) decisions in stochastic programming, where the solution
of a variable in stage :math:`n` depends on the specific solution of
variables in stage :math:`n-1` in a scenario-dependent manner. Please
note that, while non-adjustable variables can be integer, adjustable
variables *must* be continuous.

.. rubric:: Basic procedure for solving robust optimization models

The implementation of robust optimization in AIMMS closely follows the
concepts described in this section. The basic procedure to create and
solve a robust optimization model in AIMMS is as follows:

-  indicate in your model which parameters are to become uncertain or
   random,

-  for every constraint in your model that you want to become a chance
   constraint, specify the probability with which it must hold,

-  for every adjustable variable in your model specify on which
   uncertain parameters it depends, and

-  specify possible realizations of the uncertain parameters in terms of
   predefined regions or using specialized uncertainty constraints.

Each of these steps is explained in more detail in the sections to
follow. Note that changing parameters, variables and constraints in your
model into uncertain or random parameters, adjustable variables and
chance constraints does in no way influence the possibility to solve the
underlying deterministic model in its original form. Thus, the robust
optimization facilities in AIMMS always form a true extension of the
functionality of the existing AIMMS application. It is even possible to
extend an existing deterministic model to both a stochastic model and a
robust optimization model, all of which can be solved independently.