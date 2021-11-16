.. _sec:gmp.lin:

Creating and Managing Linearizations
====================================

.. rubric:: MINLP problems and linearizations

When solving a mixed integer nonlinear (MINLP) problem using an outer
approximation approach (see also :ref:`ch:aoa` for a more detailed
description), an associated master MIP problem is created and extended
with linearizations of the nonlinear constraints of the original problem
with respect to successive solutions of the underlying NLP sub-problem.
Using the procedures in the ``GMP::Linearization`` namespace, AIMMS
allows you to add linearizations of nonlinear constraints to a
particular math program instance. Together with the
:any:`GMP::Instance::CreateMasterMIP` procedure to create the initial
master MIP problem, these procedures form the heart of the
implementation of the outer approximation algorithm in AIMMS, as
discussed in :ref:`sec:aoa.impl`.

.. rubric:: Managing linearizations

The procedures and functions of the ``GMP::Linearization`` namespace are
listed in :ref:`this table <table:gmp.linearization>`.

.. _GMP::Linearization::SetType-LR:

.. _GMP::Linearization::SetDeviationBound-LR:

.. _GMP::Linearization::SetWeight-LR:

.. _GMP::Linearization::RemoveDeviation-LR:

.. _GMP::Linearization::GetType-LR:

.. _GMP::Linearization::GetLagrangeMultiplier-LR:

.. _GMP::Linearization::GetDeviationBound-LR:

.. _GMP::Linearization::GetWeight-LR:

.. _GMP::Linearization::GetDeviation-LR:

.. _GMP::Linearization::AddSingle-LR:

.. _GMP::Linearization::Delete-LR:

.. _GMP::Linearization::Add-LR:

.. _table:gmp.linearization:

.. table:: 

	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Add <GMP::Linearization::Add>`\ (*GMP1*, *GMP2*, *solNr*, *conSet*, *devPermitted*, *penalty*, *linNr*\ [, *jacTol*])          |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`AddSingle <GMP::Linearization::AddSingle>`\ (*GMP1*, *GMP2*, *solNr*, *row*, *devPermitted*, *penalty*, *linNr*\ [, *jacTol*]) |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Delete <GMP::Linearization::Delete>`\ (*GMP*, *linNr*)                                                                         |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`RemoveDeviation <GMP::Linearization::RemoveDeviation>`\ (*GMP*, *row*, *linNr*)                                                |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetDeviation <GMP::Linearization::GetDeviation>`\ (*GMP*, *row*, *linNr*)                                                      |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetDeviationBound <GMP::Linearization::GetDeviationBound>`\ (*GMP*, *row*, *linNr*)                                            |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetWeight <GMP::Linearization::GetWeight>`\ (*GMP*, *row*, *linNr*)                                                            |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetLagrangeMultiplier <GMP::Linearization::GetLagrangeMultiplier>`\ (*GMP*, *row*, *linNr*)                                    |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetType <GMP::Linearization::GetType>`\ (*GMP*, *row*, *linNr*)\ :math:`\to`\ :any:`AllRowTypes`                               |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetDeviationBound <GMP::Linearization::SetDeviationBound>`\ (*GMP*, *row*, *linNr*, *value*)                                   |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetWeight <GMP::Linearization::SetWeight>`\ (*GMP*, *row*, *linNr*, *value*)                                                   |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetType <GMP::Linearization::SetType>`\ (*GMP*, *row*, *linNr*, *rowType*)                                                     |
	+--------------------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Creating and deleting linearizations

Through the procedures

-  :any:`GMP::Linearization::Add`,

-  :any:`GMP::Linearization::AddSingle`,

-  :any:`GMP::Linearization::Delete`, and

-  :any:`GMP::Linearization::RemoveDeviation`

you can instruct AIMMS to add and delete one or more rows and columns to
a given math program instance, representing the linearizations of
(nonlinear) constraints of another math program instance at a particular
solution point.

.. rubric:: Modifying linearizations

You can modify the rows and columns generated by these procedures using
the matrix manipulation routines discussed in :ref:`sec:gmp.matrix`. The
rows and columns generated by AIMMS cannot be associated directly with
constraints and variables in your model, but must be addressed using the
:ref:`.ExtendedConstraint` and :ref:`.ExtendedVariable` suffices.
:ref:`sec:matrix.extended` discusses the precise suffices generated by
AIMMS when using the functions :any:`GMP::Linearization::Add` and
:any:`GMP::Linearization::AddSingle`.

.. rubric:: Remaining functions

Through the remaining functions in the ``GMP::Linearization`` namespace
you can

-  get and set information about the devation variables added to the
   linearized constraints, and their penalties added to the objective,
   and

-  get and set the row types of the generated constraints.

Note the you must use the appropriate :ref:`.ExtendedConstraint` suffix to
refer to the particular linearization constraint when using these
functions.