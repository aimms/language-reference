.. _sec:gmp.solver:

Using Solver Sessions
=====================

.. rubric:: Using solver sessions

The procedures and functions of the ``GMP::SolverSession`` namespace are
listed in :ref:`this table <table:gmp.solver>`. Solver sessions are created
implicitly by AIMMS or explicitly by calling the procedure
:any:`GMP::Instance::CreateSolverSession`.

.. _GMP::SolverSession::Transfer-LR:

.. _GMP::SolverSession::WaitForSingleCompletion-LR:

.. _GMP::SolverSession::WaitForCompletion-LR:

.. _GMP::SolverSession::SetOptionValue-LR:

.. _GMP::SolverSession::Interrupt-LR:

.. _GMP::SolverSession::GetSolver-LR:

.. _GMP::SolverSession::GetOptionValue-LR:

.. _GMP::SolverSession::ExecutionStatus-LR:

.. _GMP::SolverSession::CreateProgressCategory-LR:

.. _GMP::SolverSession::GenerateCut-LR:

.. _GMP::SolverSession::GetSolverStatus-LR:

.. _GMP::SolverSession::GetProgramStatus-LR:

.. _GMP::SolverSession::GetNumberOfBranchNodes-LR:

.. _GMP::SolverSession::GetNodesUsed-LR:

.. _GMP::SolverSession::GetNodesLeft-LR:

.. _GMP::SolverSession::GetNodeObjective-LR:

.. _GMP::SolverSession::GetNodeNumber-LR:

.. _GMP::SolverSession::GetObjective-LR:

.. _GMP::SolverSession::GetBestBound-LR:

.. _GMP::SolverSession::GetTimeUsed-LR:

.. _GMP::SolverSession::GetMemoryUsed-LR:

.. _GMP::SolverSession::GetIterationsUsed-LR:

.. _GMP::SolverSession::GetCandidateObjective-LR:

.. _GMP::SolverSession::GetCallbackInterruptStatus-LR:

.. _GMP::SolverSession::GetAttributeValue-LR:

.. _GMP::SolverSession::GetInstance-LR:

.. _GMP::SolverSession::GetIIS-LR:

.. _GMP::SolverSession::RejectIncumbent-LR:

.. _GMP::SolverSession::AsynchronousExecute-LR:

.. _GMP::SolverSession::Execute-LR:

.. _GMP::SolverSession::Delete-LR:

.. _table:gmp.solver:

.. table:: : ``GMP::SolverSession`` functions and procedures

	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Execute <GMP::SolverSession::Execute>`\ (*solverSession*)                                                                                   |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`AsynchronousExecute <GMP::SolverSession::AsynchronousExecute>`\ (*solverSession*)                                                           |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`ExecutionStatus <GMP::SolverSession::ExecutionStatus>`\ (*solverSession*)\ :math:`\to`\ :any:`AllExecutionStatuses`                         |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Interrupt <GMP::SolverSession::Interrupt>`\ (*solverSession*)                                                                               |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`WaitForCompletion <GMP::SolverSession::WaitForCompletion>`\ (*Objects*)                                                                     |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`WaitForSingleCompletion <GMP::SolverSession::WaitForSingleCompletion>`\ (*Objects*)\ :math:`\to`\ :any:`AllSolverSessionCompletionObjects`  |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Delete <GMP::SolverSession::Delete>`\ (*solverSession*)                                                                                     |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateProgressCategory <GMP::SolverSession::CreateProgressCategory>`\ (*solverSession*\ [, *Name*][, *Size*])                               |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetOptionValue <GMP::SolverSession::GetOptionValue>`\ (*solverSession*, *optionName*)                                                       |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetOptionValue <GMP::SolverSession::SetOptionValue>`\ (*solverSession*, *optionName*, *value*)                                              |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetInstance <GMP::SolverSession::GetInstance>`\ (*solverSession*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                     |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetSolver <GMP::SolverSession::GetSolver>`\ (*solverSession*)\ :math:`\to`\ :any:`AllSolvers`                                               |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetIterationsUsed <GMP::SolverSession::GetIterationsUsed>`\ (*solverSession*)                                                               |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetMemoryUsed <GMP::SolverSession::GetMemoryUsed>`\ (*solverSession*)                                                                       |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetTimeUsed <GMP::SolverSession::GetTimeUsed>`\ (*solverSession*)                                                                           |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetBestBound <GMP::SolverSession::GetBestBound>`\ (*solverSession*)                                                                         |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetCandidateObjective <GMP::SolverSession::GetCandidateObjective>`\ (*solverSession*)                                                       |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetObjective <GMP::SolverSession::GetObjective>`\ (*solverSession*)                                                                         |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetProgramStatus <GMP::SolverSession::GetProgramStatus>`\ (*solverSession*)\ :math:`\to`\ :any:`AllSolutionStates`                          |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetSolverStatus <GMP::SolverSession::GetSolverStatus>`\ (*solverSession*)\ :math:`\to`\ :any:`AllSolutionStates`                            |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetCallbackInterruptStatus <GMP::SolverSession::GetCallbackInterruptStatus>`\ (*solverSession*)\ :math:`\to`\ :any:`AllSolverInterrupts`    |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetAttributeValue <GMP::SolverSession::GetAttributeValue>`\ (*solverSession*, *attr*\ [, *objNo*])                                          |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GenerateCut <GMP::SolverSession::GenerateCut>`\ (*solverSession*, *row*\ [, *local*][, *purgeable*])                                        |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`RejectIncumbent <GMP::SolverSession::RejectIncumbent>`\ (*solverSession*)                                                                   |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNodeNumber <GMP::SolverSession::GetNodeNumber>`\ (*solverSession*)                                                                       |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNodeObjective <GMP::SolverSession::GetNodeObjective>`\ (*solverSession*)                                                                 |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNodesLeft <GMP::SolverSession::GetNodesLeft>`\ (*solverSession*)                                                                         |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNodesUsed <GMP::SolverSession::GetNodesUsed>`\ (*solverSession*)                                                                         |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNumberOfBranchNodes <GMP::SolverSession::GetNumberOfBranchNodes>`\ (*solverSession*)                                                     |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetIIS <GMP::SolverSession::GetIIS>`\ (*solverSession*, *rowSet*, *colSet*)                                                                 |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Transfer <GMP::SolverSession::Transfer>`\ (*solverSession*, *GMP*)                                                                          |
	+---------------------------------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Solving a mathematical program instance

By calling the :any:`GMP::SolverSession::Execute` procedure, the given
solver session will take care of solving the associated mathematical
program instance in a blocking manner, i.e. the function will not return
until the solver has completed the solution process. This function is
called implicitly by the :any:`GMP::Instance::Solve` function or by the
``SOLVE`` statement.

.. rubric:: Asynchronous solve

Alternatively, you can solve a mathematical program instance in an
non-blocking manner by using the function
:any:`GMP::SolverSession::AsynchronousExecute`. Rather than waiting for the
solution process to complete, this function will dispatch the solution
process to a separate thread of execution, and return immediately. This
allows multiple mathematical program instances to be solved in parallel,
assuming your computer has multiple processors or a multi-core
processor. Note that requests for a synchronous solve through the
``SOLVE`` statement will fail if a AIMMS is still executing an
asynchronous solution process.

.. rubric:: Session synchronization

To allow your application to synchronize its execution when multiple
solver sessions are executed asynchronously, AIMMS offers the following
synchronization procedures

-  :any:`GMP::SolverSession::Interrupt`,

-  :any:`GMP::SolverSession::ExecutionStatus`,

-  :any:`GMP::SolverSession::WaitForCompletion`, and

-  :any:`GMP::SolverSession::WaitForSingleCompletion`.

Through the :any:`GMP::SolverSession::Interrupt` function you can request
AIMMS to interrupt a solver session that is executing (asynchronously).
You can call the function :any:`GMP::SolverSession::ExecutionStatus` to
check the status of a given solver session.

.. rubric:: Waiting for multiple completions

Using the function :any:`GMP::SolverSession::WaitForCompletion` you can
halt the main AIMMS thread of execution to wait until the entire set of
solver sessions passed as an argument to the function have completed.
You can use this function, for instance, to end the solution phase of
your model, prior to moving on to the post-processing phase of your
model.

.. rubric:: ...and for single completion

In addition, AIMMS offers a function
:any:`GMP::SolverSession::WaitForSingleCompletion` which returns as soon as
a single solver session from the given set of solver sessions has
completed its execution. The return value of the function is the
completed solver session that caused the function to return. You can use
``WaitForSingleCompletion``, for instance, to asynchronously solve the
next mathematical program instance from a queue of mathematical program
instances waiting to be solved.

.. rubric:: No solution transfer

Note that neither :any:`GMP::SolverSession::Execute` and
:any:`GMP::SolverSession::AsynchronousExecute` will copy the initial
solution into the solver, or copy the final solution back into solution
repository or model identifiers. When you use these functions you always
have to explicitly call functions from the ``GMP::Solution`` namespace
to accomplish these tasks.

.. rubric:: Support for callbacks

When callbacks for the mathematical program instance associated with a
solver session have been set (see also :ref:`sec:gmp.instance`), AIMMS
will make sure that the specified callback procedures in your model will
be called whenever appropriate. If you have specified a single callback
procedure for multiple callback reasons, you can call the procedure

-  :any:`GMP::SolverSession::GetCallbackInterruptStatus`

to retrieve the reason why your callback procedure was called. The
result is an element in the predeclared set :any:`AllSolverInterrupts`
which contains the elements

-  ``Candidate``,

-  ``Incumbent``,

-  ``AddCut``,

-  ``Iterations``,

-  ``Heuristic``,

-  ``StatusChange``, and

-  ``Finished``.

When the solver session has not yet been called, the status is ``"``
(empty element). During a callback, you can call the function

-  :any:`GMP::SolverSession::GetInstance`

if you need the mathematical program instance associated with the given
solver session, and you can retrieve the current objective values using
the functions

-  :any:`GMP::SolverSession::GetBestBound`,

-  :any:`GMP::SolverSession::GetObjective`.

.. rubric:: Synchronous nested solves allowed

During any callback you are allowed to generate and solve other
mathematical program instances *in a synchronous manner*. You can use
such nested solves, for instance, for finding a heuristic solution
during a ``Heuristic`` callback. Once you have found a heuristic
solution, you can pass it onto the running solver session using the
function :any:`GMP::Solution::SendToSolverSession`. Note that this
functionality is currently only supported by CPLEX and Gurobi.

.. rubric:: No asynchronous solves

During a callback AIMMS does not allow you to call the function
:any:`GMP::SolverSession::AsynchronousExecute` to solve another
mathematical program instance in an asynchronous manner. However, AIMMS
offers a special class of synchronization objects called *events*, which
allow you to notify the main thread of execution that some event has
occurred and act accordingly. When set during a callback, the main
thread of execution may respond, for instance, by generating a
mathematical program instance based on solver data set by the callback,
and solve that mathematical program instance in an asynchronous manner.
Events are discussed in full detail in :ref:`sec:gmp.event`.

.. rubric:: Adding cuts

During an ``AddCut`` callback you may use the procedure
:any:`GMP::SolverSession::GenerateCut` to generate a local or global cut. A
local cut will only be added to the current node in the solution process
and all its descendant nodes, while a global cut will remain to exist
for all nodes onwards. The result of the procedure will be the temporary
addition of row to the matrix, as if :any:`GMP::Row::Generate` had been
called. Note that this functionality is currently only supported by
CPLEX, Gurobi and ODH-CPLEX.

.. rubric:: Rejecting incumbents

During a ``Candidate`` callback you can reject the incumbent found by
the solver by calling the procedure
:any:`GMP::SolverSession::RejectIncumbent`. Note that this functionality is
currently only supported by CPLEX.

.. rubric:: Setting options

You can set options for a specific solver session associated through the
function :any:`GMP::SolverSession::SetOptionValue`. These option values
override the option values for the associated *GMP*, set through
:any:`GMP::Instance::SetOptionValue`, which in their turn override the
project options.

.. rubric:: Retrieving an irreducible infeasible set

If the generated math program appears to be infeasible then the procedure
:any:`GMP::SolverSession::GetIIS` can be used to retrieve an irreducible
infeasible set (IIS). This procedure returns the row and column numbers
of the rows and columns that are part of the IIS.

