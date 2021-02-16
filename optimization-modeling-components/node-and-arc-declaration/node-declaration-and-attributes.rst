.. _sec:net.node:

``Node`` Declaration and Attributes
===================================

.. _node:

.. rubric:: Node attributes

Each node in a network has a number of associated incoming and outgoing
flows. Unless stated otherwise, these flows should be in balance. Based
on the flows specified in the model, AIMMS will automatically generate a
balancing constraint for every node. The possible attributes of a
``Node`` declaration are given in :ref:`this table <table:net.attr-node>`.

.. _table:net.attr-node:

.. table:: 

	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| Attribute       | Value-type                                   | See also page                                                                                                                                                                                                      |
	+=================+==============================================+====================================================================================================================================================================================================================+
	| ``IndexDomain`` | *index-domain*                               | :ref:`The Parameter IndexDomain attribute <attr:par.index-domain>`, :ref:`The Variable IndexDomain attribute <attr:var.index-domain>`, :ref:`The Constraint IndexDomain attribute <attr:var.constr.index-domain>`  |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Unit``        | *unit-valued expression*                     | :ref:`The Parameter Unit attribute <attr:par.unit>`, :ref:`The Variable Unit attribute <attr:var.unit>`                                                                                                            |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Text``        | *string*                                     | :ref:`The Text attribute <attr:prelim.text>`, :ref:`The Parameter Text attribute <attr:par.text>`                                                                                                                  |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Comment``     | *comment string*                             | :ref:`here <attr:prelim.comment>`                                                                                                                                                                                  |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Definition``  | *expression*                                 | :ref:`here <attr:var.constr.definition>`                                                                                                                                                                           |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Property``    | ``NoSave``, ``Sos1``, ``Sos2``,              | :ref:`The Parameter Property attribute <attr:par.property>`, :ref:`The Variable Property attribute <attr:var.property>`, :ref:`The Constraint Property attribute <attr:var.constr.property>`                       |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	|                 | ``Level``, ``Bound``, ``ShadowPrice``,       |                                                                                                                                                                                                                    |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	|                 | ``RightHandSideRange``, ``ShadowPriceRange`` |                                                                                                                                                                                                                    |
	+-----------------+----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	
.. _node.index_domain:

.. _node.unit:

.. _node.definition:

.. _node.property:

.. rubric:: Nodes are like constraints

Nodes are a special kind of constraint. Therefore, the remarks in
:ref:`sec:var.constr` that apply to the attributes of constraints are
also valid for nodes. The only difference between constraints and nodes
is that in the definition attribute of a node you can use one of the
keywords ``NetInflow`` and ``NetOutflow``.

.. _netinflow:

.. _netoutflow:

.. rubric:: ``NetInflow`` and ``NetOutflow``

The keywords ``NetInflow`` and ``NetOutflow`` denote the net input or
net output flow for the node. The expressions represented by
``NetInflow`` and ``NetOutflow`` are computed by AIMMS on the basis of
all arcs that depart from and arrive at the declared node. Since these
keywords are opposites, you should choose the keyword that makes most
sense for a particular node.

.. rubric:: Example

The following two ``Node`` declarations show natural applications of the
keywords ``NetInflow`` and ``NetOutflow``.

.. code-block:: aimms

	Node CustomerDemandNode {
	    IndexDomain  : (j in Customers, p in Products);
	    Definition   : {
	        NetInflow >= ProductDemanded(j,p)
	    }
	}

.. code-block:: aimms

	Node DepotStockSupplyNode {
	    IndexDomain  : (i in Depots, p in Products);
	    Definition   : {
	        NetOutflow <= StockAvailable(i,p) + ProductImport(i,p)
	    }
	}

The declaration of ``CustomerDemandNode(c,p)`` only involves network
flows, while the flow balance of ``DepotStockSupplyNode(d,p)`` also uses
a variable ``ProductImport(d,p)``.