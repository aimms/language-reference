.. _sec:gmp.stochastic:

Supporting Functions for Stochastic Programs
============================================

.. rubric:: Supporting functions for stochastic models

The stochastic Benders algorithm (see :ref:`sec:stoch.benders`) is
implemented in AIMMS as a combination of a system module that can be
included into your model, and a number of supporting functions in the
``GMP::Stochastic`` namespace of the GMP library. The procedures and
functions of the ``GMP::Stochastic`` namespace are listed in
:numref:`table:gmp.stochastic`.

.. _GMP::Stochastic::UpdateBendersSubproblem-LR:

.. _GMP::Stochastic::MergeSolution-LR:

.. _GMP::Stochastic::GetRepresentativeScenario-LR:

.. _GMP::Stochastic::GetRelativeWeight-LR:

.. _GMP::Stochastic::GetObjectiveBound-LR:

.. _GMP::Stochastic::CreateBendersRootproblem-LR:

.. _GMP::Stochastic::BendersFindReference-LR:

.. _GMP::Stochastic::BendersFindFeasibilityReference-LR:

.. _GMP::Stochastic::AddBendersOptimalityCut-LR:

.. _GMP::Stochastic::AddBendersFeasibilityCut-LR:

.. _table:gmp.stochastic:

.. table:: 

	+---------------------------------------------------------------------------------------------------------------------+
	| ``BendersFindFeasibilityReference``\ (*GMP*, *stage*, *scenario*):math:`\to`:any:`AllGeneratedMathematicalPrograms` |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``BendersFindReference``\ (*GMP*, *stage*, *scenario*):math:`\to`:any:`AllGeneratedMathematicalPrograms`            |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``CreateBendersRootproblem``\ (*GMP*\ [, *name*]):math:`\to`:any:`AllGeneratedMathematicalPrograms`                 |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``UpdateBendersSubproblem``\ (*GMP*, *solution*)                                                                    |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``AddBendersFeasibilityCut``\ (*GMP*, *solution*, *cutNo*)                                                          |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``AddBendersOptimalityCut``\ ( *GMP*, *solution*, *cutNo*)                                                          |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``MergeSolution``\ (*GMP*, *solution1*, *solution2*\ [, *updObj*])                                                  |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``GetRepresentativeScenario``\ (*GMP*, *stage*, *scenario*):math:`\to`:any:`AllStochasticScenarios`                 |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``GetObjectiveBound``\ (*GMP*, *solution*)                                                                          |
	+---------------------------------------------------------------------------------------------------------------------+
	| ``GetRelativeWeight``\ (*GMP*, *stage*, *scenario*)                                                                 |
	+---------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Overview of functionality

For a more detailed overview of the functionality offered by the
functions in the ``GMP::Stochastic`` namespace, we refer to

-  :ref:`sec:stoch.benders` for an outline of the stochastic Benders
   algorithm,

-  the system module containing the AIMMS implementation of the
   stochastic Benders algorithm, and

-  the AIMMS `Function Reference <https://documentation.aimms.com/functionreference/>`__ for a detailed explanation of the
   functionality of each function.