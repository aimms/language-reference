.. _sec:net.intro:

Networks
========

.. rubric:: Networks

There are several model-based applications which contain networks and
flows. Typical examples are applications for the distribution of
electricity, water, materials, etc. AIMMS offers two special constructs,
``Arcs`` and ``Nodes``, to formulate flows and flow balances as an
alternative to the usual algebraic constructs. Specialized algorithms
exist for pure network problems.

.. rubric:: Mixed formulations

It is possible to intermingle network constructs with ordinary variables
and constraints. As a result, the choice between ``Arcs`` and
``Variables`` on the one hand, and ``Nodes`` and ``Constraints`` on the
other, becomes a matter of convenience. For instance, in the formulation
of a flow balance at a node in the network you can refer to flows along
arcs as well as to variables that represent import from outside the
network. Similarly, you can formulate an ordinary capacity constraint
involving both network flows and ordinary variables.

.. rubric:: Flow keywords

It is assumed here that you know the basics of network flow
formulations. Following are three flow-related keywords which can be
used to specify a network flow model:

-  ``NetInflow``-the total flow into a node minus the total flow out of
   that node,

-  ``NetOutflow``-the total flow out of a node minus the total flow into
   that node, and

-  ``FlowCost``-the cost function representing the total flow cost built
   up from individual cost components specified for each arc.

The first two are always used in the context of a node declaration,
while the third may be used for the network model declaration.