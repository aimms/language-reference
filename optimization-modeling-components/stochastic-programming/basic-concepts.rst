.. _sec:stoch.concepts:

Basic Concepts
==============

.. rubric:: Basic concepts
   :name: sec:stochastic.basicconcepts

In this section you will find a number of basic concepts that are
commonly used in stochastic programming. They will help you to
unambiguously understand the stochastic programming facilities in AIMMS.

.. rubric:: Stages

In stochastic programming *stages* define a collection of consecutive
periods of time. Stages are usually identified through positive integers
:math:`1,2,\dots`, and are characterized as follows:

-  during each stage one or more stochastic (i.e. uncertain) events take
   place, and

-  at the end of a stage decisions are taken, taking into account the
   specific outcomes of the stochastic events of this and previous
   stages.

Stochastic events may be such quantities as the demand realized during a
period. They are usually represented as input data used in the
deterministic model. Any variables in the deterministic model that are
modeled conceptually to take their value *at the beginning* of a period
(for instance, the stock at the beginning of a period), should be
considered as decisions taken at the end of the previous period/stage
within the stage concept.

.. rubric:: Stages versus model periods

If the deterministic model already contains a ``Horizon`` (see
:ref:`sec:time.horizon`) or any other set of time periods, the stages of
the stochastic model may naturally coincide with the time periods from
the deterministic model, but this certainly needs not be the case. A
single period model, possibly even without an explicit period set, but
with variables representing decisions taken at the beginning *and* at
the end of the period, may still constitute a two-stage stochastic
model. For a multi-period model, a single stage in the stochastic model
may consist of multiple time periods from the deterministic model, and
hence one can always construct a mapping from the deterministic period
set to stages in the stochastic model.

.. rubric:: Variables and stages

Every individual stochastic variable in a stochastic model should be
uniquely associated with a single stage. This stage represents the
period at the end of which the variable conceptually takes it value

-  taking into consideration the *specific* outcomes of stochastic
   events taking place during the stage at hand and during prior stages,

-  but only taking into account the *distribution* of possible outcomes
   of the stochastic events taking place in any further stage.

Even if model periods of the deterministic model and the stages of the
stochastic model coincide, variables with an index into the period set
do not have to be associated with the stage corresponding to the value
of that index. As discussed above, variables that conceptually take
their value at the beginning of a period, provide a first example of
this behavior as they must be associated with the stage corresponding to
the previous period within the stochastic model.

.. rubric:: Examples

Other examples may arise, for instance, when the monthly productions of
January, February and March should be decided upon prior to the
beginning of January, regardless of the specific outcomes for the
demands during these months. Conversely, if market research has
delivered good estimates for the demand in January, February and March,
the decisions for the production in these months should take into
consideration the demand estimates of all three months. Hence the
production variables for January, February and March should be part of
the stage associated with March.

.. rubric:: Scenarios

A *scenario* for a stochastic model is a collection of outcomes for all
the stochastic events taking place in the model, along with the
associated probability of the scenario to occur. For the event values
associated with each scenario, one could solve a deterministic model,
which would yield the optimal decisions for that particular scenario.
For different scenarios, however, the decisions resulting from solving
such deterministic models individually are, in general, completely
unrelated, even if the event outcomes of the scenarios are exactly the
same up to a certain stage. To address this problem, the scenarios of a
stochastic model must be organized into a scenario tree.

.. rubric:: Scenario trees

A single scenario can be graphically represented as a simple tree
illustrated in :numref:`fig:stoch.single-scen`.

.. figure:: basic-concepts-pspic1.svg
   :name: fig:stoch.single-scen

   A tree representing a single scenario *sc\ :math:`_1`*

For multiple scenarios, the specific outcomes of the stochastic events
up to a certain stage usually coincide for a subset of the scenarios.
This gives rise to a scenario tree as illustrated in
:numref:`fig:stoch.tree`.

.. figure:: basic-concepts-pspic2.svg
   :name: fig:stoch.tree

   A scenario tree with 8 scenarios

In such a scenario tree, the path from the root node of the tree to each
of its leaf nodes corresponds to a single scenario, and the event
outcomes for scenarios that pass through the same intermediate node are
identical for all stages up to that node. If a stage consists of
multiple time periods in the deterministic model, this means that the
stochastic events taking place during *all* periods associated with the
stage should coincide. The solution process of a stochastic model will
make sure that the decisions that are to be taken at the end of these
stages are identical for all the scenarios passing through the node, as
one would intuitively expect.

.. rubric:: Scenario generation

The scenarios and the scenario tree used in a stochastic model are
usually generated by using one of the following two techniques

-  generate scenarios by incrementally creating a scenario tree
   according to a given distribution for each stochastic event, or

-  given an externally created set of scenarios, create a scenario tree
   by grouping identical or similar scenarios at every level of the
   tree.

.. rubric:: Distribution-based scenario generation

Given a leaf node in an intermediate scenario tree, for every stochastic
event that occurs during the stage directly following that node, a fixed
number of values is computed according to a given distribution (each
with its own relative probability of taking place). For each of these
values a new branch is added to the node. The process starts by adding
branches to the root node of the tree and ends when a tree is generated
for all stages. The total number of scenarios generated by the process
is the final number of leaf nodes generated. The probability of a
scenario is the multiplication of the relative probabilities associated
with each branch along the path from root to leaf node. The scenario
tree in :numref:`fig:stoch.tree` could be generated in this way, for
example, by choosing, at every intermediate node, a *high* or a *low*
level for the demand during the stage following that particular node.

.. rubric:: Scenario-based tree generation

Another approach is to start from a given collection of scenarios with
probabilities adding up to 1. Such a collection of scenarios can either
be randomly generated or be the result of some external process. As a
tree, they can be represented as a trivial scenario tree, as illustrated
in :numref:`fig:stoch.scengen`.

.. figure:: basic-concepts-pspic3.svg
   :name: fig:stoch.scengen

   An initial disconnected scenario tree

This tree can be transformed into a scenario tree by bundling together
identical or similar scenarios into a fixed or dynamic number of
branches. The group of scenarios passing through a particular
intermediate node in the scenario tree is analyzed and grouped into
subgroups of scenarios with similar or identical outcomes of the
stochastic events during the stage following that node. For every
subgroup, the existing branches are bundled into a single branch, and
the stochastic event outcomes are made identical for all scenarios in
the subgroup. The process starts by analyzing all scenarios at the root
node of the tree, and ends when every scenario is associated with a
single leaf node.

.. rubric:: Basic procedure for solving stochastic models

The implementation of stochastic programming in AIMMS closely follows
the concepts described in this section. The basic procedure to create
and solve a stochastic model in AIMMS is as follows:

-  indicate in your model which parameters and variables are to become
   stochastic,

-  for every stochastic variable in your model specify during which
   stage of the stochastic model the decision is to be taken,

-  generate scenarios, their stochastic data, and a scenario tree, using
   one of the techniques described above, and

-  generate and solve the stochastic model using the special methods
   available for this purpose in AIMMS.

Each of these steps is explained in more detail in the sections to
follow. Note that changing parameters and variables in your model into
stochastic parameters and variables, does in no way influence the
possibility to solve the underlying deterministic model in its original
form. Thus, the stochastic programming facilities in AIMMS always form a
true extension of the functionality of the existing AIMMS application.