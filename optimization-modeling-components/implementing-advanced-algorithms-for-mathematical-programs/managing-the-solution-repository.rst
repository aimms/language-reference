.. _sec:gmp.solution:

Managing the Solution Repository
================================

.. rubric:: The solution repository

The GMP library maintains a solution repository for every generated
mathematical program instance. You can use this repository, for
instance, to store

-  a number of starting solutions for a NLP problem to be solved
   successively,

-  a number of incumbent solutions as reported by a MIP solver, or

-  let a solver store multiple solutions.

If you are using solver sessions to initiate a solver, you must
explicitly transfer the initial, intermediate or final solutions between
the model, the solution repository and the solver session. As discussed
in :ref:`sec:gmp.instance`, the function :any:`GMP::Instance::Solve`
performs these necessary solution transfer steps for you, and uses the
fixed solution number 1 for all of its communication.

Some solvers are capable of finding multiple solutions instead of at
most one. Examples of such solvers are BARON, CPLEX and Gurobi. When
such a solver finds multiple solutions, these solutions are stored in
the solution repository from number 1 on upwards. The control mechanism
to let solvers find multiple solutions is solver specific:

-  ``BARON 21``: For more information see the **Help** file for option
   ``Number of best solutions`` in option category ``Specific solvers``
   - ``BARON 21`` - ``General``.

-  ``CPLEX 20.1``: For more information see the **Help** file for option
   ``Do populate`` in option category ``Specific solvers`` -
   ``CPLEX 20.1`` - ``MIP solution pool``.

-  ``Gurobi 9.1``: For more information see the **Help** file for option
   ``Pool search mode`` in option category ``Specific solvers`` -
   ``Gurobi 9.1`` - ``Solution pool``.

.. rubric:: Solution repository functions

The procedures and functions of the ``GMP::Solution`` namespace are
listed in :ref:`this table <table:gmp.solution>`. Through these functions you can

-  transfer a solution between the solution repository on the one side
   and the symbolic model or the solver on the other side,

-  obtain and set solution properties of a solution in the repository,
   or

-  perform a feasibility check on a solution in the repository.

.. _GMP::Solution::ConstraintListing-LR:

.. _GMP::Solution::SetRowValue-LR:

.. _GMP::Solution::GetRowValue-LR:

.. _GMP::Solution::SetColumnValue-LR:

.. _GMP::Solution::GetColumnValue-LR:

.. _GMP::Solution::GetFirstOrderDerivative-LR:

.. _GMP::Solution::SendToModelSelection-LR:

.. _GMP::Solution::GetTimeUsed-LR:

.. _GMP::Solution::GetMemoryUsed-LR:

.. _GMP::Solution::GetIterationsUsed-LR:

.. _GMP::Solution::GetBestBound-LR:

.. _GMP::Solution::Count-LR:

.. _GMP::Solution::IsPrimalDegenerated-LR:

.. _GMP::Solution::IsDualDegenerated-LR:

.. _GMP::Solution::IsInteger-LR:

.. _GMP::Solution::SetIterationCount-LR:

.. _GMP::Solution::Check-LR:

.. _GMP::Solution::GetSolverStatus-LR:

.. _GMP::Solution::SetSolverStatus-LR:

.. _GMP::Solution::SetProgramStatus-LR:

.. _GMP::Solution::GetProgramStatus-LR:

.. _GMP::Solution::SetObjective-LR:

.. _GMP::Solution::GetObjective-LR:

.. _GMP::Solution::SendToSolverSession-LR:

.. _GMP::Solution::RetrieveFromSolverSession-LR:

.. _GMP::Solution::SendToModel-LR:

.. _GMP::Solution::RetrieveFromModel-LR:

.. _GMP::Solution::SolutionCount:

.. _GMP::Solution::GetSolutionsSet-LR:

.. _GMP::Solution::DeleteAll-LR:

.. _GMP::Solution::Delete-LR:

.. _GMP::Solution::Move-LR:

.. _GMP::Solution::Copy-LR:

.. _table:gmp.solution:

.. table:: : ``GMP::Solution`` functions and procedures

	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Copy <GMP::Solution::Copy>`\ (*GMP*, *fromSol*, *toSol*)                                                                                |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Move <GMP::Solution::Move>`\ (*GMP*, *fromSol*, *toSol*)                                                                                |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Delete <GMP::Solution::Delete>`\ (*GMP*, *solNo*)                                                                                       |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`DeleteAll <GMP::Solution::DeleteAll>`\ (*GMP*)                                                                                          |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetSolutionsSet <GMP::Solution::GetSolutionsSet>`\ (*GMP*)\ :math:`\to`\ :any:`Integers`                                                |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Count <GMP::Solution::Count>`\ (*GMP*)                                                                                                  |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`RetrieveFromModel <GMP::Solution::RetrieveFromModel>`\ (*GMP*, *SolNr*)                                                                 |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SendToModel <GMP::Solution::SendToModel>`\ (*GMP*, *SolNr*\ [, *merge*]\ [, *evalInline*])                                              |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SendToModelSelection <GMP::Solution::SendToModelSelection>`\ (*GMP*, *SolNr*, *Identifiers*, *Suffices*\ [, *merge*]\ [, *evalInline*]) |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`RetrieveFromSolverSession <GMP::Solution::RetrieveFromSolverSession>`\ (*solverSession*, *SolNr*)                                       |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SendToSolverSession <GMP::Solution::SendToSolverSession>`\ (*solverSession*, *SolNr*)                                                   |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetObjective <GMP::Solution::GetObjective>`\ (*GMP*, *SolNr*)                                                                           |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetBestBound <GMP::Solution::GetBestBound>`\ (*GMP*, *SolNr*)                                                                           |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetProgramStatus <GMP::Solution::GetProgramStatus>`\ (*GMP*, *SolNr*)\ :math:`\to`\ :any:`AllSolutionStatus`                            |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetSolverStatus <GMP::Solution::GetSolverStatus>`\ (*GMP*, *SolNr*)\ :math:`\to`\ :any:`AllSolutionStatus`                              |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetIterationsUsed <GMP::Solution::GetIterationsUsed>`\ (*GMP*, *SolNr*)                                                                 |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetMemoryUsed <GMP::Solution::GetMemoryUsed>`\ (*GMP*, *SolNr*)                                                                         |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetTimeUsed <GMP::Solution::GetTimeUsed>`\ (*GMP*, *SolNr*)                                                                             |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetObjective <GMP::Solution::SetObjective>`\ (*GMP*, *SolNr*, *value*)                                                                  |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetProgramStatus <GMP::Solution::SetProgramStatus>`\ (*GMP*, *SolNr*, *PrStatus*)                                                       |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetSolverStatus <GMP::Solution::SetSolverStatus>`\ (*GMP*, *SolNr*, *PrStatus*)                                                         |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetIterationCount <GMP::Solution::SetIterationCount>`\ (*GMP*, *SolNr*, *IterCnt*)                                                      |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetColumnValue <GMP::Solution::GetColumnValue>`\ (*GMP*, *SolNr*, *column*\ [, *valueType*])                                            |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetColumnValue <GMP::Solution::SetColumnValue>`\ (*GMP*, *SolNr*, *column*, *value*\ [, *valueType*])                                   |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetRowValue <GMP::Solution::GetRowValue>`\ (*GMP*, *SolNr*, *row*\ [, *valueType*])                                                     |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetRowValue <GMP::Solution::SetRowValue>`\ (*GMP*, *SolNr*, *row*, *value*\ [, *valueType*])                                            |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Check <GMP::Solution::Check>`\ (*GMP*, *SolNr*, *NumInf*, *SumInf*, *MaxInf*\ [, *skipObj*]\ [, *feasTol*])                             |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`IsInteger <GMP::Solution::IsInteger>`\ (*GMP*, *SolNr*)                                                                                 |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`IsPrimalDegenerated <GMP::Solution::IsPrimalDegenerated>`\ (*GMP*, *SolNr*)                                                             |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`IsDualDegenerated <GMP::Solution::IsDualDegenerated>`\ (*GMP*, *SolNr*)                                                                 |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetFirstOrderDerivative <GMP::Solution::GetFirstOrderDerivative>`\ (*GMP*, *SolNr*, *row*, *column*)                                    |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`ConstraintListing <GMP::Solution::ConstraintListing>`\ (*GMP*, *SolNr*, *name*)                                                         |
	+-----------------------------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Solution contents

Each solution in the repository is represented by a solution vector
containing all relevant solution data, such as

-  solution status,

-  level values,

-  basis information,

-  marginals, and

-  other relevant requested sensitivity information.

.. rubric:: Solution numbering

Each generated mathematical program instance has its own associated
solution repository. Each solution in the repository is represented by
an integer solution number. Through the function
:any:`GMP::Solution::GetSolutionsSet` you can retrieve a subset of the
predefined set :any:`Integers` containing the set of all solution numbers
that are currently in use for the given mathematical program instance.

.. rubric:: Solution transfer to the model

Through the functions

-  :any:`GMP::Solution::RetrieveFromModel`,

-  :any:`GMP::Solution::SendToModel`, and

-  :any:`GMP::Solution::SendToModelSelection`

you can (re-)initialize a solution with the values currently contained
in the symbolic model, and vice versa. The function
``SendToModelSelection`` allows you to only initialize a part of the
model identifiers and suffices with a solution of from the solution
repository.

.. rubric:: Solution transfer to a solver session

Through the functions

-  :any:`GMP::Solution::RetrieveFromSolverSession`, and

-  :any:`GMP::Solution::SendToSolverSession`

you can set a solution in the repository equal to a solution reported by
a given solver session, or initialize the (initial) solution of a solver
session with a solution stored in the repository. Notice that these
functions do not have a *GMP* argument. Because each solver session is
uniquely associated with a single mathematical program instance, AIMMS
is able to determine the correct solution repository.

.. rubric:: Computing first order derivatives

Using the function :any:`GMP::Solution::GetFirstOrderDerivative`, you can
compute, for the given solution, first order derivative of a particular
row in a mathematical program with respect to a given variable. You can
use such a function, for instance, to implement a sequential linear
programming approach for nonlinear programs, as outlined in
:ref:`sec:matrix.examples.slp`.