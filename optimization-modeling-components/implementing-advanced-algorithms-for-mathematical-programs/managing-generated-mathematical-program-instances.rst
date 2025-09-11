.. _sec:gmp.instance:

Managing Generated Mathematical Program Instances
=================================================

.. rubric:: Managing math program instances

The procedures and functions of the ``GMP::Instance`` namespace are
listed in :ref:`this table <table:gmp.instance>` and take care of the creation and
management of generated mathematical program instances. Mathematical
program instances also provide access to the solution repository and
solver sessions associated with the instance.

.. _table:gmp.instance:

.. table:: : Procedures and functions in the ``GMP::Instance`` namespace

	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Generate <GMP::Instance::Generate>`\ (*MP*, *name*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                                                                  |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Copy <GMP::Instance::Copy>`\ (*GMP*, *name*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                                                                         |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Rename <GMP::Instance::Rename>`\ (*GMP*, *name*)                                                                                                                                                                                                                                           |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Delete <GMP::Instance::Delete>`\ (*GMP*)                                                                                                                                                                                                                                                   |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GenerateRobustCounterpart <GMP::Instance::GenerateRobustCounterpart>`\ (*MP*, *UncertainParameters*, *UncertaintyConstraints*\ [, *Name*])\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                           |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GenerateStochasticProgram <GMP::Instance::GenerateStochasticProgram>`\ (*MP*, *StochasticParameters*, *StochasticVariables*, *Scenarios*, *ScenarioProbability*, *ScenarioTreeMap*, *RootScenario*\ [, *GenerationMode*][, *Name*])\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`  |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateMasterMIP <GMP::Instance::CreateMasterMIP>`\ (*GMP*, *name*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                                                   |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`FixColumns <GMP::Instance::FixColumns>`\ (*GMP1*, *GMP2*, *solNr*, *varSet*)                                                                                                                                                                                                               |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`AddIntegerEliminationRows <GMP::Instance::AddIntegerEliminationRows>`\ (*GMP*, *solNr*, *refNo*)                                                                                                                                                                                           |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`DeleteIntegerEliminationRows <GMP::Instance::DeleteIntegerEliminationRows>`\ (*GMP*, *refNo*)                                                                                                                                                                                              |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`AddLimitBinaryDeviationRow <GMP::Instance::AddLimitBinaryDeviationRow>`\ (*GMP*, *solNr*, *varSet*, *deviation*\ [, *refNo*])                                                                                                                                                              |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`DeleteLimitBinaryDeviationRow <GMP::Instance::DeleteLimitBinaryDeviationRow>`\ (*GMP*\ [, *refNo*])                                                                                                                                                                                        |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateBlockMatrices <GMP::Instance::CreateBlockMatrices>`\ (*GMP*, *colSet*, *blockValue*, *prefix*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                 |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateDual <GMP::Instance::CreateDual>`\ (*GMP*, *name*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                                                             |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateFeasibility <GMP::Instance::CreateFeasibility>`\ (*GMP*\ [, *name*][, *useMinMax*])\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                            |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreatePresolved <GMP::Instance::CreatePresolved>`\ (*GMP*, *name*)\ :math:`\to`\ :any:`AllGeneratedMathematicalPrograms`                                                                                                                                                                   |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetSymbolicMathematicalProgram <GMP::Instance::GetSymbolicMathematicalProgram>`\ (*GMP*)\ :math:`\to`\ :any:`AllMathematicalPrograms`                                                                                                                                                      |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetInfeasibleData <GMP::Instance::GetInfeasibleData>`\ (*GMP*, *parSet*, *message*\ [, *method*][, *effort*][, *textFormat*])                                                                                                                                                              |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNumberOfRows <GMP::Instance::GetNumberOfRows>`\ (*GMP*)                                                                                                                                                                                                                                 |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNumberOfColumns <GMP::Instance::GetNumberOfColumns>`\ (*GMP*)                                                                                                                                                                                                                           |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetNumberOfNonzeros <GMP::Instance::GetNumberOfNonzeros>`\ (*GMP*)                                                                                                                                                                                                                         |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetDirection <GMP::Instance::GetDirection>`\ (*GMP*)\ :math:`\to`\ :any:`AllMatrixManipulationDirections`                                                                                                                                                                                  |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetDirection <GMP::Instance::SetDirection>`\ (*GMP*, *dir*)                                                                                                                                                                                                                                |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetOptionValue <GMP::Instance::GetOptionValue>`\ (*GMP*, *OptionName*)                                                                                                                                                                                                                     |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetOptionValue <GMP::Instance::SetOptionValue>`\ (*GMP*, *OptionName*, *Value*)                                                                                                                                                                                                            |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateProgressCategory <GMP::Instance::CreateProgressCategory>`\ (*GMP*\ [, *Name*])\ :math:`\to`\ :any:`AllProgressCategories`                                                                                                                                                            |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetMathematicalProgrammingType <GMP::Instance::GetMathematicalProgrammingType>`\ (*GMP*)\ :math:`\to`\ :any:`AllMathematicalProgrammingTypes`                                                                                                                                              |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetMathematicalProgrammingType <GMP::Instance::SetMathematicalProgrammingType>`\ (*GMP*, *type*)                                                                                                                                                                                           |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetSolver <GMP::Instance::GetSolver>`\ (*GMP*)\ :math:`\to`\ :any:`AllSolvers`                                                  | :any:`SetSolver <GMP::Instance::SetSolver>`\ (*GMP*, *solver*)                                                                                           |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetCallbackAddCut <GMP::Instance::SetCallbackAddCut>`\ (*GMP*, *CB*)                                                            | :any:`SetCallbackAddLazyConstraint <GMP::Instance::SetCallbackAddLazyConstraint>`\ (*GMP*, *CB*)                                                         |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetCallbackBranch <GMP::Instance::SetCallbackBranch>`\ (*GMP*, *CB*)                                                            | :any:`SetCallbackCandidate <GMP::Instance::SetCallbackCandidate>`\ (*GMP*, *CB*)                                                                         |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetCallbackIncumbent <GMP::Instance::SetCallbackIncumbent>`\ (*GMP*, *CB*)                                                      | :any:`SetCallbackStatusChange <GMP::Instance::SetCallbackStatusChange>`\ (*GMP*, *CB*)                                                                   |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetCallbackHeuristic <GMP::Instance::SetCallbackHeuristic>`\ (*GMP*, *CB*)                                                      | :any:`SetCallbackIterations <GMP::Instance::SetCallbackIterations>`\ (*GMP*, *CB*, *nrIters*)                                                            |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetCallbackTime <GMP::Instance::SetCallbackTime>`\ (*GMP*, *CB*)                                                                |                                                                                                                                                          |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetIterationLimit <GMP::Instance::SetIterationLimit>`\ (*GMP*, *nrIters*)                                                       | :any:`SetMemoryLimit <GMP::Instance::SetMemoryLimit>`\ (*GMP*, *nrMB*)                                                                                   |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetTimeLimit <GMP::Instance::SetTimeLimit>`\ (*GMP*, *nrSeconds*)                                                               | :any:`SetCutoff <GMP::Instance::SetCutoff>`\ (*GMP*, *value*)                                                                                            |
	+---------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`Solve <GMP::Instance::Solve>`\ (*GMP*)                                                                                                                                                                                                                                                     |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetBestBound <GMP::Instance::GetBestBound>`\ (*GMP*)                                                                                                                                                                                                                                       |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetObjective <GMP::Instance::GetObjective>`\ (*GMP*)                                                                                                                                                                                                                                       |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetMemoryUsed <GMP::Instance::GetMemoryUsed>`\ (*GMP*)                                                                                                                                                                                                                                     |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`MemoryStatistics <GMP::Instance::MemoryStatistics>`\ (*GMPSet*, *OutputFileName*\ [, *optional-arguments* :math:`\dots`])                                                                                                                                                                  |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetAttributeValue <GMP::Instance::GetAttributeValue>`\ (*GMP*, *attr*\ [, *objNo*])                                                                                                                                                                                                        |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetColumnNumbers <GMP::Instance::GetColumnNumbers>`\ (*GMP*, *varSet*)\ :math:`\to`\ :any:`Integers`                                                                                                                                                                                       |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetRowNumbers <GMP::Instance::GetRowNumbers>`\ (*GMP*, *conSet*)\ :math:`\to`\ :any:`Integers`                                                                                                                                                                                             |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetObjectiveColumnNumber <GMP::Instance::GetObjectiveColumnNumber>`\ (*GMP*)\ :math:`\to`\ :any:`Integers`                                                                                                                                                                                 |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetObjectiveRowNumber <GMP::Instance::GetObjectiveRowNumber>`\ (*GMP*)\ :math:`\to`\ :any:`Integers`                                                                                                                                                                                       |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`DeleteMultiObjectives <GMP::Instance::DeleteMultiObjectives>`\ (*GMP*)                                                                                                                                                                                                                     |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`CreateSolverSession <GMP::Instance::CreateSolverSession>`\ (*GMP*\ [, *Name*][, *Solver*])\ :math:`\to`\ :any:`AllSolverSessions`                                                                                                                                                          |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| :any:`FindApproximatelyFeasibleSolution <GMP::Instance::FindApproximatelyFeasibleSolution>`\ (*GMP*, *sol1*, *sol2*, *nrIter*\ [, *maxIter*][, *feasTol*]\ [, *moveTol*][, *imprTol*][, *maxTime*][, *useSum*][, *augIter*][, *useBest*])                                                        |
	+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rubric:: Creation of mathematical program instances

New mathematical program instances can be created by calling

-  the ``SOLVE`` statement,

-  the :any:`GMP::Instance::Generate` function,

-  the :any:`GMP::Instance::GenerateRobustCounterpart` function,

-  the :any:`GMP::Instance::GenerateStochasticProgram` function,

-  the :any:`GMP::Instance::Copy` function,

-  the :any:`GMP::Instance::CreateBlockMatrices` function,

-  the :any:`GMP::Instance::CreateDual` function,

-  the :any:`GMP::Instance::CreateFeasibility` function,

-  the :any:`GMP::Instance::CreatePresolved` function,

-  the :any:`GMP::Instance::CreateMasterMIP` function,

-  the :any:`GMP::Stochastic::CreateBendersRootproblem` function,

-  the :any:`GMP::Stochastic::BendersFindFeasibilityReference` function, or

-  the :any:`GMP::Stochastic::BendersFindReference` function.

All mathematical program instances created through each of these calls,
are uniquely represented by elements in the predefined set
:any:`AllGeneratedMathematicalPrograms`. For the functions in the
``GMP::Instance`` namespace creating GMPs you can explicitly specify the
name of the associated set element to be created. When calling the
``SOLVE`` statement, AIMMS will generate an element with the same name
as the ``MathematicalProgram`` at hand. When the name of the element to
be created is already contained in the set
:any:`AllGeneratedMathematicalPrograms`, the mathematical program instance
associated with the existing element will be completely replaced by the
newly created mathematical program instance.

.. rubric:: Special math programming types

Stochastic programming and the use of the function
``GenerateStochasticProgram`` is discussed in :ref:`sec:stoch.solve`.
Robust optimization and the use of the function
``GenerateRobustCounterpart`` is explained in :ref:`sec:robust.solve`.
The functionality of the ``CreateDual`` function is explained in more
detail in :ref:`sec:gmp.instance.dual`. The function ``CreateMasterMIP``
is used by the AIMMS Outer Approximation solver, which is discussed in
full detail in :ref:`ch:aoa`. Presolving of mathematical programs is
discussed in :ref:`sec:nlp.presolve`.

.. rubric:: Deleting and renaming instances

Through the procedures :any:`GMP::Instance::Delete` and
:any:`GMP::Instance::Rename` you can delete and rename mathematical program
instances and their associated elements in the set
:any:`AllGeneratedMathematicalPrograms`. If you rename a mathematical
program instance to a name that already exists in the set
:any:`AllGeneratedMathematicalPrograms`, the associated mathematical
program instance will be deleted prior to renaming.

.. rubric:: CLEANDEPENDENTS statement

Note that also the ``CLEANDEPENDENTS`` statement may remove mathematical
program instances from memory when it affects any constraint or variable
referenced by that instance.

.. rubric:: Retrieving and setting basic properties

Through the functions

-  :any:`GMP::Instance::GetSymbolicMathematicalProgram`,

-  :any:`GMP::Instance::GetNumberOfRows`,

-  :any:`GMP::Instance::GetNumberOfColumns`,

-  :any:`GMP::Instance::GetNumberOfNonzeros`,

-  :any:`GMP::Instance::GetDirection`, and

-  :any:`GMP::Instance::GetMathematicalProgrammingType`

you can retrieve the current value of some basic properties of a
mathematical program instance. The number of rows, columns and nonzeros
can be changed by manipulating the matrix of the mathematical program
instance (see also :ref:`sec:gmp.matrix`). You can use the functions

-  :any:`GMP::Instance::SetDirection`, and

-  :any:`GMP::Instance::SetMathematicalProgrammingType`

to modify the optimization direction and mathematical programming type.
The type of a mathematical program must be a member of the set
``MathematicalProgrammingTypes`` (see also :ref:`sec:mp.mp`) The
direction associated with a mathematical program is either

-  ``'maximize'``,

-  ``'minimize'``, or

-  ``'none'``.

The direction ``'none'`` is the instruction to the solver to find a
feasible solution.

.. rubric:: Installing callbacks

For each mathematical program instance, you can set up to six callback
functions that will be called by any solver session associated with the
mathematical program instance at hand. Through the following procedures
you can install or uninstall a callback function for a mathematical
program instance.

-  :any:`GMP::Instance::SetCallbackAddCut`

-  :any:`GMP::Instance::SetCallbackAddLazyConstraint`

-  :any:`GMP::Instance::SetCallbackBranch`

-  :any:`GMP::Instance::SetCallbackCandidate`

-  :any:`GMP::Instance::SetCallbackIncumbent`

-  :any:`GMP::Instance::SetCallbackStatusChange`

-  :any:`GMP::Instance::SetCallbackHeuristic`

-  :any:`GMP::Instance::SetCallbackIterations`

-  :any:`GMP::Instance::SetCallbackTime`

Each of these procedures expects an element of the set
:any:`AllProcedures`, or an empty element ``"`` to uninstall the callback.

.. rubric:: Callback procedures

Callback procedures for each type of callback should be declared as
follows:

   ``AnExampleCallback(solverSession)``

where the *solverSession* argument should be a scalar input element
parameter into the set :any:`AllSolverSessions`. Callback procedures should
have a return value of

-  0, if you want the solver session to stop, or

-  1, if you want the solver session to continue.

As discussed before, each solver session can be uniquely associated with
a single mathematical program instance. You can find this instance by
calling the function :any:`GMP::SolverSession::GetInstance` (see also
:ref:`sec:gmp.solver`), and, within the callback procedure, use this
instance to get access to its associated properties.

.. rubric:: Example

The following example implements a callback procedure for the incumbent
callback. The callback procedure finds the associated mathematical
program instance, and stores all incumbents reported by the solver into
the next solution of the solution repository.

.. code-block:: aimms

	Procedure IncumbentCallBack {
	    Arguments  : solvSess;
	    Body       : {
	        theGMP := GMP::SolverSession::GetInstance( solvSess );
	        GMP::Solution::RetrieveFromSolverSession( solvSess, solutionNumber(theGMP) );
	        solutionNumber(theGMP) += 1;

	        return 1;   ! continue solving
	    }
	}

Note that the callback procedure uses the
:any:`GMP::Solution::RetrieveFromSolverSession` function (discussed in
:ref:`sec:gmp.solution`) to retrieve the solution from the solver.

.. rubric:: Solving mathematical program instances

In contrast to the ``SOLVE`` statement, the philosophy behind the GMP
library is to break down the optimization functionality in AIMMS to a
level which offers optimum support for implementing advanced algorithms
around a ``MathematicalProgram`` in your model. One of the consequences
of this philosophy is that the solution is never directly transferred
between the symbolic variables and constraints and the solver, but is
intermediately stored in a solution repository. Therefore, solving a
``MathematicalProgram`` using the GMP library breaks down into the
following basic steps:

#. generate a mathematical program instance for the
   ``MathematicalProgram``,

#. create a solver session for the mathematical program instance,

#. transfer the initial point from the model to the solution repository,

#. transfer the initial point from the solution repository to the solver
   session,

#. let the solver session solve the problem,

#. transfer the final solution from the solver session to the solution
   repository, and

#. transfer the final solution from the solution repository to the
   model.

.. rubric:: Solving the instance directly

For your convenience, however, the GMP library contains a procedure

-  :any:`GMP::Instance::Solve`

which, given a generated mathematical program instance, takes care of
all intermediate steps (i.e. steps 2-7) necessary to solve the
mathematical program instance. In case you need access to the solution
in the solution repository after calling the :any:`GMP::Instance::Solve`
call, you should notice that the :any:`GMP::Instance::Solve` procedure (as
well as the ``SOLVE`` statement) performs all of its solution transfer
through the fixed solution number 1 in the solution repository.

.. rubric:: Emulating the ``SOLVE`` statement

The following AIMMS code provides an emulation of the ``SOLVE``
statement in terms of ``GMP::Instance`` functions.

.. code-block:: aimms

	! Generate an instance of the mathematical program MPid and add
	! the element 'MPid' to the set AllGeneratedMathematicalPrograms.
	! This element is returned into the element parameter genGMP.
	genGMP := GMP::Instance::Generate(MPid, FormatString("%e", MPid));

	! Actually solve the problem using the solve procedure for an
	! instance (which communicates through solution number 1).
	GMP::Instance::Solve(genGMP);

.. rubric:: Multistart support

The function ``FindApproximatelyFeasibleSolution`` is used by the AIMMS
multistart algorithm (see :ref:`sec:nlp.multistart`) to compute an
approximately feasible solution for an NLP problem. The algorithm used
by this function to find the approximately feasible solution is
described in :cite:`bib:Ch04`.

.. rubric:: Creating solver sessions

For each generated mathematical program instance, you can explicitly
create and delete one or more solver sessions using the following
functions:

-  :any:`GMP::Instance::CreateSolverSession`, and

-  :any:`GMP::SolverSession::Delete`.

Once created, you can use the solver session to solve the generated
mathematical program

-  in a blocking manner by calling the :any:`GMP::SolverSession::Execute`
   function, or

-  in a non-blocking manner by calling the
   :any:`GMP::SolverSession::AsynchronousExecute` function.

Prior to calling the :any:`GMP::SolverSession::Execute` or
:any:`GMP::SolverSession::AsynchronousExecute` functions, you should call
the function :any:`GMP::Solution::SendToSolverSession` to initialize the
solver session with a solution stored in the solution repository. Using
an explicit solver session allows you, for instance, to solve an NLP
problem with several initial solutions stored in the solution
repository.

.. rubric:: Multiple sessions allowed

AIMMS allows you to create multiple solver sessions per mathematical
program instance, and solve them in parallel. You can solve multiple
mathematical program instances in parallel, by calling the function
:any:`GMP::SolverSession::AsynchronousExecute` multiple times. The function
starts a separate thread of execution to solve the math program instance
asynchronously, and returns immediately. To solve multiple mathematical
program instances in parallel, your computer should have multiple
processors or a multi-core processor.

.. rubric:: Deleting solver sessions

Once the function :any:`GMP::SolverSession::Execute` or
:any:`GMP::SolverSession::AsynchronousExecute` has been called, the
internal solver representation of the mathematical program instance will
be created. The solver representation will only be deleted-and its
associated resources freed-when the corresponding solver session has
been deleted by calling the procedure :any:`GMP::SolverSession::Delete`.

.. rubric:: Implementing the procedure ``GMP::Instance:: Solve``

The ``GMP:Instance::Solve`` procedure discussed previously can be
emulated using solver sessions, as illustrated in the equivalent code
below.

.. code-block:: aimms

	! Create a solver session for genMP, which will create an element
	! in the set AllSolverSessions, and assign the newly created element
	! to the element parameter session.
	session := GMP::Instance::CreateSolverSession(genMP);

	! Copy the initial solution from the variables in AIMMS to
	! solution number 1 of the generated mathematical program.
	GMP::Solution::RetrieveFromModel(genMP,1);

	! Send the solution stored in solution 1 to the solver session
	GMP::Solution::SendToSolverSession(session, 1);

	! Call the solver session to actually solve the problem.
	GMP::SolverSession::Execute(session);

	! Copy the solution from the solver session into solution 1.
	GMP::Solution::RetrieveFromSolverSession(session, 1);

	! Store this solution in the AIMMS variables and constraints.
	GMP::Solution::SendToModel(genMP, 1);

.. rubric:: Setting default solver session limits

You can use the following procedures to set various default limits that
apply to all solver sessions created through
:any:`GMP::Instance::CreateSolverSession`.

-  :any:`GMP::Instance::SetIterationLimit`

-  :any:`GMP::Instance::SetMemoryLimit`

-  :any:`GMP::Instance::SetTimeLimit`

-  :any:`GMP::Instance::SetCutoff`

.. rubric:: Setting GMP-specific options

For every *GMP* you can override the default project options using the
function :any:`GMP::Instance::SetOptionValue`. You can also set options for
a specific solver session associated with a *GMP* through the function
:any:`GMP::SolverSession::SetOptionValue`. In turn, option values set for a
specific solver session override the option values for the associated
*GMP*.

.. rubric:: Setting the default solver

Similarly, you can get and set the default solver that will be used by
all solver sessions created through
:any:`GMP::Instance::CreateSolverSession`.

-  :any:`GMP::Instance::GetSolver`

-  :any:`GMP::Instance::SetSolver`

.. rubric:: Outer approximation support

Through the functions

-  :any:`GMP::Instance::CreateMasterMIP`

-  :any:`GMP::Instance::FixColumns`

-  :any:`GMP::Instance::AddIntegerEliminationRows`

-  :any:`GMP::Instance::DeleteIntegerEliminationRows`

the GMP library offers support for solving mixed integer nonlinear
(MINLP) problems using a white box outer approximation approach. The
AIMMS Outer Approximation solver is discussed in full detail in
:ref:`ch:aoa`.

.. rubric:: Re-optimizing with limited impact on the solution

Imagine you have created a production plan based on optimizing some mathematical
program and that something unexpected happened that (partly) ruined the plan.
You now have to re-optimize the mathematical program, with some
changes, but would like the solution of the new optimization to be
close to the previous one. For that you can use the procedure

-  :any:`GMP::Instance::AddLimitBinaryDeviationRow`

which adds a constraint that limits the number of binary decision variables of which
the solution value is allowed to change. This constraint can be removed using the procedure

-  :any:`GMP::Instance::DeleteLimitBinaryDeviationRow`

.. _sec:gmp.instance.dual:

Dealing with Degeneracy and Non-Uniqueness
------------------------------------------

.. rubric:: Background

When solving a mathematical program, some practical difficulties may
arise when the optimal solution of the underlying model is either
degenerate and/or not unique (i.e. there are multiple optimal
solutions). These difficulties may concern both the primal and dual
solution (i.e. the shadow prices).

.. rubric:: Problems with degeneracy

In the case of degeneracy (see also
Section 4.2 of the AIMMS `Modeling Guide <https://documentation.aimms.com/_downloads/AIMMS_modeling.pdf>`__
for an explanation), the solution status of one or more variables is
"basic at bound". In the presence of degeneracy, shadow prices are no
longer unique, and their interpretation is therefore ambiguous. As a
result, if the shadow prices have an economic interpretation in the
application, the particular shadow prices found by the solver cannot be
presented to the end-user in a meaningful and reliable fashion.

.. rubric:: Problems with multiple solutions

In the case of multiple solutions, the situation is even worse. There
are multiple optimal bases, and the associated shadow prices differ
between these bases (just as with degeneracy). In addition, the solution
presented to the end-user is no longer unique, which may raise questions
by the end-user as to why a particular solution is presented.

.. rubric:: Degeneracy and multiple solutions

Both degeneracy and multiple solutions can occur at the same time,
having their combined effect on the non-uniqueness of both the primal
and the dual solution (the optimal shadow prices). The following two
paragraphs present possible solutions to deal with multiple primal and
dual solutions.

.. rubric:: Towards a unique primal solution

One way to deal with multiple solutions is to find a new and second
objective function specifically designed to deal with eliminating the
multiplicity of solutions. This might be accomplished, for instance, by
adding new sets of variables and constraints to cap some aspect of the
primal model, and the maximum cap could then be minimized. Or perhaps a
straightforward modification of the original objective function could
become the second auxiliary objective. It is important to note that this
second objective function is optimized only after the first objective
function is fixed at its previous optimal value and has been added as a
constraint.

.. rubric:: Implementing primal uniqueness

Using the functionality provided by the GMP library, constructing a
second objective function for a mathematical program is a
straightforward task:

-  generate and solve the original mathematical program,

-  use the matrix manipulations procedures discussed in
   :ref:`sec:gmp.matrix` to create a new objective and fix the original
   one in the associated mathematical program instance,

-  resolve the modified mathematical program instance.

.. rubric:: Towards a unique dual solution

In the presence of primal degeneracy and/or multiple primal solutions,
it is impossible to influence the selection of shadow prices, as this
decision is made by the solver. To give the control back to you as a
model developer, the only sensible step is to go directly to the dual
formulation, and work with the model expressed in terms of shadow
prices. It is then possible to construct a second auxiliary objective
function designed to produce economically meaningful shadow prices.
Again, it is important to note that this second objective function is
optimized only after the original objective function is fixed at the
optimal objective function value of the primal model, and has been added
as a constraint.

.. rubric:: Creating a dual mathematical program instance

To support the procedure for reaching dual uniqueness, the GMP library
contains the function

-  :any:`GMP::Instance::CreateDual`

which creates the dual mathematical program instance associated with a
given primal mathematical program instance.

.. rubric:: Standard dual formulation

For a mathematical program of the form

.. math::

   \begin{align}
   & \text{minimize} & & \sum_i c_ix_i \\
   & \text{subject to} & & \sum_i A_{ij}x_i \geq b_j & & \forall j \\
   &&& x_i \geq 0 & & \forall i \\ 
   \end{align}

the dual mathematical program can be formulated as follows

.. math::

   \begin{align}
   & \text{maximize} & & \sum_j b_j\lambda_j \\
   & \text{subject to} & & \sum_j A_{ij}\lambda_j \leq c_i & & \forall i \\
   &&& \lambda_j \geq 0 & & \forall j \\ 
   \end{align}

where the :math:`\lambda_j` represent the shadow prices of the
constraints of the primal formulation.

.. rubric:: Sign changes

If the primal formulation contains nonpositive or free variables, or
contains :math:`\leq` or equality constraints, a number of simple
substitution will bring the formulation back into the standard form
above, after which the above dual formulation can be used directly. The
resulting changes to the dual formulation are as follows:

-  a nonpositive variable :math:`x_i` corresponds to a dual :math:`\geq`
   constraint,

-  a free variable :math:`x_i` corresponds to a dual equality
   constraint,

-  a :math:`\leq` constraint corresponds to a nonpositive dual variable
   :math:`\lambda_j`, and

-  an equality constraint corresponds to a free dual variable
   :math:`\lambda_j`.

.. rubric:: Bounded variables and ranged constraints

However, such simple transformation are not possible anymore if the
primal model contains:

-  bounded variables, i.e. :math:`l_i \leq x_i \leq u_i`, or

-  ranged constraints, i.e. :math:`d_i \leq \sum_i A_{ij}x_i \leq b_j`.

In these cases, additional constraints (implicitly) have to be added as
follows to satisfy the above standard formulation:

-  :math:`x_i \geq l_i` whenever :math:`l_i \neq 0,-\infty`,

-  :math:`x_i \leq u_i` whenever :math:`u_i \neq 0, \infty`, and

-  :math:`\sum_i A_{ij}x_i \geq d_j`.

In the generated dual mathematical program, such implicit constraint
additions in the primal formulation will lead to the explicit
introduction of additional variables in the dual formulation. Such
variable additions to the dual formulation are taken care of by AIMMS
automatically, but will have consequences when you want to manipulate
the matrix of the dual mathematical program instance, as discussed in
:ref:`sec:matrix.extended`.

.. rubric:: Implementing dual uniqueness

Using the function :any:`GMP::Instance::CreateDual`, it is relatively
straightforward to implement the procedure outlined above to reach dual
uniqueness:

-  generate and solve the original mathematical program,

-  generate a dual mathematical program instance from the primal
   mathematical program instance,

-  use the matrix manipulations procedures discussed in
   :ref:`sec:gmp.matrix` to create a new dual objective and fix the
   original dual objective in the newly created dual mathematical
   program instance,

-  solve the modified dual mathematical program instance.

.. _sec:gmp.instance.explain:

Explainability
---------------

.. rubric:: Determining data causing infeasibility

A particular situation which requires explainability is when the mathematical optimization model is formulated correctly, but it becomes infeasible due to incorrect input data provided by the user. 
So, in this case the infeasibility is not inherent to the model formulation and it is not found as a modeling error during the model development phase, but rather during the model deployment phase 
due to some incorrect data instance which turns the model infeasible. 

Business applications including optimization should also consider infeasibilities and include support for dealing with the infeasibility
in this situation. More specifically, some valuable information about the cause of the infeasibility should be returned to the end user in a form which she/he can understand and use for correcting the
input data in order to make the model feasible again.

This goal can be achieved by calling the procedure :any:`GMP::Instance::GetInfeasibleData`. Under the assumption that an LP/MILP model is correctly formulated, this function performs in essence the following tasks:

- Calculate IIS or solve Feasibility Problem
- Remove constraints without `changeable` parameters
- Pinpoint the `changeable` parameters used in the constraints

After performing these steps, the function returns a message (as output argument) and fills the parameter suffix called ``.SuspicionLevel`` with one of the possible values: High, Normal, or Low.
The output message may be displayed in a suitable way into the graphical user interface in order to inform the user in a concise manner about the most likely cause of the infeasibility.

In turn, the values of the ``.SuspicionLevel`` parameter suffixes may be used to assign identifier annotations to the parameters of interest. Such annotations may be subsequently used in order to highlight
the suspicious values of those parameters in the graphical user interface and visually notify the user about potentially incorrect data values. For example, when such values are rendered in a table,
the cells of the suspicious values may be coloured in light pink, pink, or red, based on the suspicion levels Low, Normal, or High, respectively.

After adjusting the most critical values highlighted in the graphical user interface to more realistic numbers, the user may re-solve the model and observe the effect. If the model turns feasible, then the issue
has been resolved/explained. If the model still stays infeasible, then a new call to the procedure :any:`GMP::Instance::GetInfeasibleData` may reveal additional information about potentially incorrect data 
and the process may be repeated in a similar way until the model becomes feasible again. It could happen that a few iterations are required in order to fully explain the cause of the infeasibility and to 
resolve the issue with the incorrect user data completely.
