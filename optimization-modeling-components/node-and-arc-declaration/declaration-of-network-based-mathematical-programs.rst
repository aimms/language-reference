.. _sec:net.mp:

Declaration of Network-Based Mathematical Programs
==================================================

.. _flowcost:

.. rubric:: The ``FlowCost`` variable

If your model contains arcs and nodes, the special variable ``FlowCost``
can be used in the definition of the objective of your mathematical
program. During the model generation phase, AIMMS will generate an
expression for this variable based on the associated unit cost for each
of the arcs in your mathematical program.

.. rubric:: Pure network models

AIMMS will mark your mathematical program as a pure network, if the
following conditions are met:

-  your mathematical program consists of arcs and nodes only,

-  all arcs are continuous and do not have one of the ``SOS`` or the
   ``SemiContinuous`` properties,

-  the value of the ``Objective`` attribute equals the variable
   ``FlowCost``, and

-  all ``Multiplier`` attributes assume the default value of one,

For pure network models you can specify ``network`` as its ``Type``.

.. rubric:: Network versus LP solver

If your mathematical program is a pure network model, AIMMS will pass
the model to a special network solver. If your mathematical program is a
generalized network or a mixed network-LP problem, AIMMS will generate
the constraints associated with the nodes in your network as linear
constraints and use an LP solver to solve the problem. AIMMS will also
use an LP solver if you have specified its type to be ``lp``. You may
assert that your mathematical program is a pure network model by
specifying ``network`` as its type.

.. rubric:: Example

A pure network model containing the arc and node declarations of the
previous sections, but without the additional term
``ProductImport(d,p)`` in the node ``DepotStockSupplyNode(d,p)``, is
defined by the following declaration.

.. code-block:: aimms

	MathematicalProgram ProductFlowDecisionModel {
	    Objective   : FlowCost;
	    Direction   : minimize;
	    Constraints : AllConstraints;
	    Variables   : AllVariables;
	    Type        : network;
	}

If the arc ``Transport(i,j)`` declared in the previous section is the
only arc, then the variable ``FlowCost`` can be represented by the
expression

.. code-block:: aimms

	sum [(i,j,p), UnitTransportCost(i,j) * Transport(i,j,p)]

Note that the addition of the term ``ProductImport(i,p)`` in
``DepotStockSupplyNode(i,p)`` would result in a mixed network/linear
program formulation, which requires an LP solver.