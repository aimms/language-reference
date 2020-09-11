.. _sec:stoch.solve:

Solving Stochastic Models
=========================

.. rubric:: Solving stochastic models

After generating stochastic event data and a scenario tree, you can
generate and solve the stochastic model by using methods from the GMP
library discussed in :ref:`chap:gmp`. AIMMS supports two methods for
solving a stochastic model:

-  by solving its *deterministic equivalent*, or

-  for purely linear mathematical programs only, through the *stochastic
   Benders algorithm*, or

-  using the Benders decomposition algorithm in CPLEX 12.7 or higher.

Both Benders algorithms will decompose the stochastic model into
multiple smaller models, and thus is better suited to solve stochastic
models where the deterministic equivalent, either by the size of the
deterministic model or because of a huge number of scenarios, becomes
too big or time-consuming to solve at once. The Benders decomposition
algorithm in CPLEX can be used to solve stochastic models with integer
variables, as long as all integer variables are assigned to the first
stage. For more information see the CPLEX option ``Benders_strategy``.

Generating and Solving the Deterministic Equivalent
---------------------------------------------------

.. rubric:: Generating a stochastic model

The method for generating a stochastic model for a
``MathematicalProgram`` *MP* is

-  :any:`GMP::Instance::GenerateStochasticProgram`\ ( *MP*,
   *StochasticParameters*, *StochasticVariables*, *Scenarios*,
   *ScenarioProbability*, *ScenarioTreeMap*,
   *DeterministicScenarioName*\ [, *GenerationMode*][, *Name*])

The function returns an element into the set
:any:`AllGeneratedMathematicalPrograms`. This generated math program
instance contains a memory-efficient representation of the technology
matrix of the stochastic model and the stochastic event data, and can be
used to create a deterministic equivalent of the stochastic model, as
well as the submodels necessary for a stochastic Benders approach.

.. rubric:: Specifying stochastic identifiers

Through the arguments *StochasticParameters* and *StochasticVariables*
you indicate to AIMMS which stochastic parameters and variables you want
to take into consideration when generating this stochastic model. These
arguments must be subsets of the predefined sets
:any:`AllStochasticParameters` and :any:`AllStochasticVariables`,
respectively. You may want to use real subsets, for instance, when your
AIMMS project contains multiple stochastic models, each referring only
to a subset of the stochastic parameters and variables.

.. rubric:: Specifying scenarios

Through the *Scenarios*, *ScenarioProbability* and *ScenarioTreeMap*
arguments you specify the set of scenarios, their probabilities and the
mapping defining the scenario tree for which you want to generate the
stochastic model to AIMMS. Through the string argument
*DeterministicScenarioName*, you supply the name of the artificial
element that AIMMS will add to the predefined set
:any:`AllStochasticScenarios` (if not created already), and use to store
the solution of non-stochastic variables in their respective
:ref:`.Stochastic` suffices as explained in :ref:`sec:stoch.stoch`.

.. rubric:: Enforcing non-anticipativity constraints

Using the *GenerationMode* argument you can specify whether you want
AIMMS to explicitly add the non-anticipativity constraints to your
stochastic model, or whether you want non-anticipativity to be enforced
implicitly by substituting the representative scenario for every
non-representative scenario at every stage. *GenerationMode* is an
element parameter into the predefined set
:any:`AllStochasticGenerationModes`, with possible values

-  ``'CreateNonAnticipativityConstraints'``, and

-  ``'SubstituteStochasticVariables'`` (the default value).

.. rubric:: Name argument

With the optional *Name* argument you can explicitly specify a name for
the generated mathematical program. If you do not choose a name, AIMMS
will use the name of the underlying ``MathematicalProgram`` as the name
of the generated mathematical program as well. Please note, that AIMMS
will also use this name as the default name for solving the
deterministic model. Therefore, if you do not want the generated
mathematical program of the deterministic model to be deleted, then you
have to choose a non-default name.

.. rubric:: Solving the deterministic equivalent of a stochastic model

You can solve a stochastic model by using the regular GMP procedure

-  :any:`GMP::Instance::Solve`\ (*gmp*)

By applying this function to a generated mathematical program associated
with a stochastic model, AIMMS will create the deterministic equivalent
and pass it to the appropriate LP/MIP solver. The
:any:`GMP::Instance::Solve` method is discussed in full detail in
:ref:`sec:gmp.instance`.

.. rubric:: Changing the model input

Note that, when you adjust the scenario tree map, the stochastic data,
the scenario probabilities, or the value of the ``Stage`` attribute of
some variables after you generated the stochastic model, you should
regenerate the stochastic model again to reflect these changes.

.. rubric:: Example

Consider the following call to
:any:`GMP::Instance::GenerateStochasticProgram`

.. code-block:: aimms

	GMP::Instance::GenerateStochasticProgram(
	    TransportModel, AllStochasticParameters, AllStochasticVariables,
	    MyScenarios, MyScenarioProbability, MyScenarioTreeMap,
	    "TransportModel", 'SubstituteStochasticVariables', "StochasticTransportModel");

After solving the generated stochastic model, its solution will be
stored as follows, where ``sc`` is an index into ``MyScenarios``

-  the per-scenario solution of a stochastic variable ``Transport(i,j)``
   will be stored in ``Transport.Stochastic(sc,i,j)``,

-  the deterministic solution of a non-stochastic variable
   ``InitialStock(i)`` will be stored in
   ``InitialStock.Stochastic('TransportModel',i)``,

-  the weighted objective value for the objective variable ``TotalCost``
   will be stored in ``TotalObjective.Stochastic('TransportModel')``,
   while the contribution by every scenario is available through
   ``TotalCost.Stochastic(sc)``.

.. _sec:stoch.benders:

Using the Stochastic Benders Algorithm
--------------------------------------

.. rubric:: Using the stochastic Benders algorithm

Instead of solving the deterministic equivalent of a stochastic model,
AIMMS also allows you to solve *linear* stochastic models using a
stochastic Benders algorithm. The stochastic Benders algorithm is based
on a reformulation of the original model as a sequence of models
outlined below. The solution of the original model can be achieved by
solving the sequence of models iteratively until a terminating condition
is reached. A more detailed discussion of the stochastic Benders
algorithm can be found in :cite:`bib:DT98` or :cite:`bib:Al03`.

.. rubric:: Definitions

All nodes in the scenario tree are numbered starting at 1 (the root
node).

.. math::

   \begin{align}
   & \textbf{Indices:} \\
   &&& \text{$i$} & & \text{index for the set of nodes $N$} \\
   &&& \text{$t$} & & \text{index for the set of stages $T$} \\
   & \textbf{Parameters:} \\
   &&& \text{$q_i$} & & \text{probability belonging to node $i$} \\
   &&& \text{$p_i$} & & \text{parent of node $i$} \\
   & \textbf{Sets:} \\
   &&& \text{$I_i$} & & \text{set with children of node $i$} \\
   &&& \text{$N_t$} & & \text{set of nodes belonging to stage $t$} 
   \end{align}

.. rubric:: Convention

In the algorithmic outline below we identify the problem names with
their associated solutions. That is, if a problem is, for instance,
identified as :math:`F_i(x_{p_i})`, we will also use this name to denote
its solution in other sub- problems.

.. rubric:: The original model

The nested Benders algorithm can be used for problems of the form

.. math::

   \begin{align}
   & \text{minimize} & & \sum_{t\in T}\sum_{i\in N_t} q_i c_i^T x_i \\
   & \text{subject to} & & W_1 x_1 = h_1 & & \\
   &&& A_i x_{p_i} + W_i x_i = h_i & & \forall i\in N_t, t\in T\backslash\{1\} \\ 
   &&& x_i \geq 0 & & \forall i\in N_t, t\in T \\ 
   \end{align}

.. rubric:: A reformulation as a sequence of models

This problem corresponds to the following sequence of problems. For node
:math:`i = 1`, the problem :math:`F_1` is defined as

.. math::

   \begin{align}
   & \text{minimize} & & c_1^Tx_1 + \sum_{j\in I_1} q_i F_j(x_1) \\
   & \text{subject to} & & W_1x_1 = h_1 & & \\
   &&& x_1 \geq 0 & & \\ 
   \end{align}

For all other nodes :math:`i\in N_t` in stage
:math:`t\in T\backslash\{1\}`, the problem :math:`F_i(x_{p_i})` is
defined as follows (note that :math:`\sum_{j\in I_i} q_j = q_i`)

.. math::

   \begin{align}
   & \text{minimize} & & c_i^Tx_i + \sum_{j\in I_i} \frac{q_j}{q_i} F_j(x_i) \\
   & \text{subject to} & & W_ix_i = h_i - A_ix_{p_i} & & \\
   &&& x_i \geq 0 & & \\ 
   \end{align}

For the leaf nodes in the scenario tree, the term
:math:`\sum_{j\in I_i}\frac{q_j}{q_i}F_j(x_i)` is omitted.

.. rubric:: Formulated differently

If we now introduce an upper bound :math:`\theta_i` to replace the term
:math:`\sum_{j\in I_i}\frac{q_j}{q_i}F_j(x_i)`, we can rewrite the
subproblem :math:`F_i(x_{p_i})` as

.. math::

   \begin{align}
   & \text{minimize} & & c_i^Tx_i + \theta_i \\
   & \text{subject to} & & W_ix_i = h_i - A_ix_{p_i} & & \\
   &&& \theta_i \geq \sum_{j\in I_i}\frac{q_j}{q_i}F_j(x_i) & & \\ 
   &&& x_i \geq 0 & & \\ 
   \end{align}

Because of the linear nature of the original problem, the terms
:math:`\sum_{j\in I_i}\frac{q_j}{q_i}F_j(x_i)` are piecewise linear and
convex. Therefore there exists an (a priori unknown) set of equations

.. math:: D^l_i x_i = d^l_i

that describes such a term and for which

.. math:: D^l_i x_i + \theta_i \geq d^l_i.

Moreover, we are only interested in those :math:`x_i` such that
:math:`F_j(x_i)` are feasible for all :math:`j\in I_i`. This requirement
can be enforced by an (a priori unknown) set of constraints

.. math:: E^l_i x_i  \geq e^l_i.

By substituting these constraints we obtain the following reformulation
of problem :math:`F_i(x_{p_i})`

.. math::

   \begin{align}
   & \text{minimize} & & c_i^Tx_i + \theta_i \\
   & \text{subject to} & & W_ix_i = h_i - A_ix_{p_i} & & \\
   &&& D^l_i x_i + \theta_i \geq  d^l_i & & \forall l\in 1,\dots,R_i \\ 
   &&& E^l_i x_i \geq e^l_i & & \forall l\in 1,\dots,S_i \\ 
   &&& x_i \geq 0 & & \\ 
   \end{align}

.. rubric:: The relaxed master problem

The actual problem that is solved at node :math:`i` is the following
relaxed master problem :math:`\tilde{N}_i(x_{p_i})` defined as follows:

.. math::

   \begin{align}
   & \text{minimize} & & c_i^Tx_i + \theta_i \\
   & \text{subject to} & & W_ix_i = h_i - A_ix_{p_i} & & \\
   &&& D^l_i x_i + \theta_i \geq  d^l_i & & \forall l\in 1,\dots,r_i \\ 
   &&& E^l_i x_i \geq e^l_i & & \forall l\in 1,\dots,s_i \\ 
   &&& x_i \geq 0 & & \\ 
   \end{align}

At the start of the Benders algorithm :math:`r_i` and :math:`s_i` will
be 0 for all :math:`i\in N`. The constraints
:math:`D^l_i x_i + \theta_i\geq  d^l_i` are optimality cuts obtained
from the children. That is, if :math:`\tilde{N}_j(x_i)` is feasible for
all :math:`j\in I_i` (but not optimal) then an optimality cut is added
to :math:`\tilde{N}_i(x_{p_i})`. The optimality cut is constructed by
using a combination of the dual solutions of :math:`\tilde{N}_j(x_i)`
for all :math:`j\in I_i`. Adding an optimality cut does not make a
feasible relaxed master problem infeasible. The Benders algorithm fails
if one of the subproblems is unbounded. This can be avoided by giving
all variables, except the objective variable, finite bounds.

.. rubric:: Adding feasibility cuts

The constraints :math:`E^l_i x_i\geq e^l_i` are feasibility cuts
obtained from a child. If some child problem :math:`\tilde{N}_j(x_i)` is
not feasible then the following problem :math:`\tilde{E}_j(x_i)` is
solved

.. math::

   \begin{align}
   & \text{minimize} & & w_j = e^T u^+_j + e^T u^-_j \\
   & \text{subject to} & & W_jx_j + I u^+_j - I u^-_j  = h_j - A_jx_i & & \\
   &&& E^l_j x_j \geq e^l_j & & \forall l\in 1,\dots,s_j \\ 
   &&& x_j \geq 0 & & \\ 
   &&& u^+_j \geq 0 & & \\ 
   &&& u^-_j \geq 0 & & \\ 
   \end{align}

This feasibility problem can only be formulated for linear problems, is
always feasible, and bounded from below by 0. Its dual solution is used
to construct a new feasibility constraint for
:math:`\tilde{N}_i(x_{p_i})`. Note that node :math:`j` in its turn
obtains optimality and/or feasibility cuts from its children for
:math:`\tilde{N}_j(x_i)` and :math:`\tilde{E}_j(x_i)`, unless :math:`j`
refers to a leaf node.

.. rubric:: Terminating condition

If :math:`(x_i, \theta_i)` is an optimal solution of
:math:`\tilde{N}_i(x_{p_i})` and

.. math:: \theta_i  \geq  \tilde{N}_i(x_{p_i})

then :math:`(x_i, \theta_i)` is an optimal solution of
:math:`F_i(x_{p_i})`. If this holds for all non-leaf nodes then we have
found an optimal solution of our original problem. For the leaf nodes,
:math:`x_i` only needs to be an optimal solution of
:math:`\tilde{N}_i(x_{p_i})`.

.. rubric:: Implementation in AIMMS

The stochastic Benders algorithm outlined above is implemented in AIMMS
as a system module that you can include into your model, together with a
number of supporting functions in the GMP library to perform a number of
algorithmic steps that cannot be performed in the AIMMS language itself,
for instance, to actually generate the stochastic sub-problems, and to
generate feasibility and optimality cuts.

.. rubric:: Adding the module

You can add the system module implementing the stochastic Benders
algorithm to your model through the **Settings-Install System Module...**
menu. By selecting the **Stochastic Decomposition Module** in the
**Install System Module** dialog box, AIMMS will add this system module
to your model.

.. rubric:: Using the stochastic Benders module

The main procedure for using the stochastic Benders algorithm is
``DoStochasticDecomposition``. Its inputs are:

-  a stochastic GMP,

-  the set of stages to consider, and

-  the set of scenarios to consider.

The procedure implements the algorithm outlined above. The supporting
GMP functions for the stochastic Benders algorithm are described in
:ref:`sec:gmp.stochastic`.

.. rubric:: Modifying the algorithm

Because the stochastic Benders algorithm is written in the AIMMS
language, you have complete freedom to modify the algorithm in order to
tune it for your stochastic programs. Also, the basic algorithm solves
all sub-problems sequentially. If your AIMMS license permits parallel
solver sessions, you can also speed up the algorithm by solving multiple
sub-problems in parallel using the GMP function
:any:`GMP::SolverSession::AsynchronousExecute`.