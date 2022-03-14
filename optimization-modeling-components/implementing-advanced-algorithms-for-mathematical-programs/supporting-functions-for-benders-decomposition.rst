.. _sec:gmp.benders:

Supporting Functions for Benders' Decomposition
===============================================

.. rubric:: Supporting functions for Benders' decomposition

The Benders' decomposition algorithm (see :ref:`ch:benders`) is
implemented in AIMMS as a combination of a system module that can be
included into your model, and a number of supporting functions in the
``GMP::Benders`` namespace of the GMP library. The procedures and
functions of the ``GMP::Benders`` namespace are listed in
:ref:`this table <table:gmp.benders>`.

.. _GMP::Benders::UpdateSubProblem-LR:

.. _GMP::Benders::CreateSubProblem-LR:

.. _GMP::Benders::CreateMasterProblem-LR:

.. _GMP::Benders::AddOptimalityCut-LR:

.. _GMP::Benders::AddFeasibilityCut-LR:

.. _table:gmp.benders:

.. table:: : ``GMP::Benders`` functions and procedures

	+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateMasterProblem <GMP::Benders::CreateMasterProblem>`\ (*GMP*, *Variables*, *name*\ [, *feasibilityOnly*][, *addConstraints*])\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms` |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateSubProblem <GMP::Benders::CreateSubProblem>`\ (*GMP1*, *GMP2*, *name*\ [, *useDual*][, *normalizationType*])\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`UpdateSubProblem <GMP::Benders::UpdateSubProblem>`\ (*GMP1*, *GMP2*, *solution*\ [, *round*])                                                                                           |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`AddFeasibilityCut <GMP::Benders::AddFeasibilityCut>`\ (*GMP1*, *GMP2*, *solution*, *cutNo*)                                                                                             |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`AddOptimalityCut <GMP::Benders::AddOptimalityCut>`\ ( *GMP1*, *GMP2*, *solution*, *cutNo*)                                                                                              |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Overview of functionality

For a more detailed overview of the functionality offered by the
functions in the ``GMP::Benders`` namespace, we refer to

-  :ref:`ch:benders` for an outline of the Benders' decomposition
   algorithm,

-  the system module containing the AIMMS implementation of the Benders'
   decomposition algorithm, and

-  the AIMMS `Function Reference <https://documentation.aimms.com/functionreference/>`__ for a detailed explanation of the
   functionality of each function.