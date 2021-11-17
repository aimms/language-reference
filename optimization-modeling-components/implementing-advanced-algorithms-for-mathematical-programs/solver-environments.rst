.. _sec:gmp.environments:

Solver Environment Procedures
=============================

.. rubric:: Solver environments

The procedures and functions in the ``GMP::Solver`` namespace deal with solver environments and
are listed in :ref:`this table <table:gmp.environments>`.
Normally AIMMS initializes one solver environment for each active solver at startup and frees it
when AIMMS is closed. In some cases it is more practical to initialize a solver environment just
before solving a mathematical program and free it afterwards, and possibly repeat this process
if multiple mathematical programs have to be solved.

.. _GMP::Solver::FreeEnvironment-LR:

.. _GMP::Solver::GetAsynchronousSessionsLimit-LR:

.. _GMP::Solver::InitializeEnvironment-LR:

.. _GMP::Solver::SetEnvironmentDoubleParameter-LR:

.. _GMP::Solver::SetEnvironmentIntegerParameter-LR:

.. _GMP::Solver::SetEnvironmentStringParameter-LR:

.. _table:gmp.environments:

.. table:: : ``GMP::Solver`` functions and procedures

	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`InitializeEnvironment <GMP::Solver::InitializeEnvironment>`\ (*solver*\ [, *computeserver*][, *password*][, *priority]*][, *timeout*][, *logfile*]) |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`FreeEnvironment <GMP::Solver::FreeEnvironment>`\ (*solver*)                                                                                         |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetEnvironmentDoubleParameter <GMP::Solver::SetEnvironmentDoubleParameter>`\ (*solver*, *parameter*, *value*)                                       |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetEnvironmentIntegerParameter <GMP::Solver::SetEnvironmentIntegerParameter>`\ (*solver*, *parameter*, *value*)                                     |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetEnvironmentStringParameter <GMP::Solver::SetEnvironmentStringParameter>`\ (*solver*, *parameter*, *value*)                                       |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetAsynchronousSessionsLimit <GMP::Solver::GetAsynchronousSessionsLimit>`\ (*solver*\ [, *cores*][, *GMP*])                                         |
	+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
