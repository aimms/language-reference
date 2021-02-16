.. _sec:mp.suffix:

Suffices and Callbacks
======================

.. rubric:: Suffices

A mathematical program has a number of suffices which can be used for
various purposes. Typical examples are:

-  To obtain information about the solution process. This information is
   filled in by the solver at the end of the solution process. These
   suffixes are presented in :ref:`this table <table:mp.suffix-mp.Solver>`.

-  To determine when and how to activate a callback procedure. This
   information can be filled in between solution steps. See also
   :ref:`chap:gmp` where an alternative method for callbacks is
   presented. These suffixes are presented in
   :ref:`this table <table:mp.suffix-mp.User>`.

-  To get statistics of the generated mathematical program. These
   statistics are determined when the generated mathematical program is
   constructed. These suffixes are presented in
   :ref:`this table <table:mp.suffix-mp.Aimms>`.

.. _sumofinfeasibilities:

.. _numberofinfeasibilities:

.. _NumberOfFails:

.. _NumberOfBranches:

.. _solutiontime:

.. _gentime:

.. _nodes:

.. _iterations:

.. _solverstatus:

.. _programstatus:

.. _bestbound:

.. _incumbent:

.. _objective:

.. _table:mp.suffix-mp.Solver:

.. table:: Suffices of a mathematical program filled by the solver

   =========================== =======================================
   Suffix                      Meaning
   =========================== =======================================
   ``Objective``               Current objective value
   ``Incumbent``               Current incumbent value
   ``BestBound``               Best bound on objective value
   ``ProgramStatus``           Current program status
   ``SolverStatus``            Current solver status
   ``Iterations``              Current number of iterations
   ``Nodes``                   Current number of nodes
                               (``mip``, ``miqp``, and ``miqcp`` only)
   ``GenTime``                 Current generation time in [second]
   ``SolutionTime``            Current solution time in [second]
   ``NumberOfBranches``        Number of nodes visited by a CP solver
   ``NumberOfFails``           Number of leaf nodes without
                               solution in a CP search tree
   ``NumberOfInfeasibilities`` Final number of infeasibilities
   ``SumOfInfeasibilities``    Final sum of the infeasibilities
   =========================== =======================================

.. _callbackaoa:

.. _callbackreturnstatus:

.. _callbackaddcut:

.. _callbackincumbent:

.. _callbackstatuschange:

.. _callbacktime:

.. _callbackiterations:

.. _callbackprocedure:

.. _table:mp.suffix-mp.User:

.. table:: Suffices of a mathematical program stated by the user

   ======================== ================================
   Suffix                   Meaning
   ======================== ================================
   ``CallbackProcedure``    Name of callback procedure
   ``CallbackIterations``   Return to callback after this
                            number of iterations
   ``CallbackTime``         Name of callback procedure to be
                            called after some elapsed time
   ``CallbackStatusChange`` Name of callback procedure to be
                            called after a status change
   ``CallbackIncumbent``    Name of callback procedure to be
                            called for every new incumbent
   ``CallbackAddCut``       Name of callback procedure to be
                            called to add additional cuts
                            (CPLEX and GUROBI)
   ``CallbackReturnStatus`` Return status of callback
   ``CallbackAOA``          Name of AOA callback procedure
   ======================== ================================

.. _NumberOfNonlinearNonzeros:

.. _NumberOfNonlinearVariables:

.. _NumberOfNonlinearConstraints:

.. _NumberOfSOS2Constraints:

.. _NumberOfSOS1Constraints:

.. _NumberOfIndicatorConstraints:

.. _NumberOfIntegerVariables:

.. _numberofnonzeros:

.. _numberofvariables:

.. _numberofconstraints:

.. _solvercalls:

.. _table:mp.suffix-mp.Aimms:

.. table:: Suffices of a mathematical program statistics from AIMMS

   ================================ ======================================
   Suffix                           Meaning
   ================================ ======================================
   ``SolverCalls``                  Total number of applied ``SOLVE``'s
   ``NumberOfConstraints``          Number of individual constraints
   ``NumberOfVariables``            Number of individual variables
   ``NumberOfNonzeros``             Number of nonzeros
   ``NumberOfIntegerVariables``     Number of individual integer variables
   ``NumberOfIndicatorConstraints`` Number of individual constraints
                                    with an activating condition
   ``NumberOfSOS1Constraints``      Number of individual SOS1 constraints
   ``NumberOfSOS2Constraints``      Number of individual SOS2 constraints
   ``NumberOfNonlinearConstraints`` Number of individual nonlinear
                                    constraints
   ``NumberOfNonlinearVariables``   Number of individual nonlinear
                                    variables
   ``NumberOfNonlinearNonzeros``    Number of nonlinear nonzeros
   ================================ ======================================

.. rubric:: Solver callbacks

After each iteration the external solver calls back to the AIMMS system
to offer AIMMS the opportunity to take control. AIMMS, in turn, allows
you to execute a procedure which is referred to as a *callback
procedure*. Once the callback procedure has finished, the control is
returned to the external solver to continue with the next iteration. By
including a callback procedure you can perform several tasks such as:

-  inspect the current status of the solution process,

-  update one or more model parameters, which can be used, for instance,
   to provide a graphical overview of the solution process,

-  retrieve (part of) the current solution, and

-  abort the solution process, and

You can nominate any procedure as a callback procedure by assigning its
name to the suffix ``CallbackProcedure`` of the associated mathematical
program as in:

.. code-block:: aimms

	TransportModel.CallbackProcedure := 'MyCallbackProcedure' ;

Note that values assigned to the suffix ``CallbackProcedure`` or any of
the other suffices holding the name of a callback procedure, must be
elements of the predefined set :any:`AllProcedures`. Therefore, if you
assign a literal procedure name to such a suffix, you should make sure
to quote it, as illustrated in the example above.

.. rubric:: When activated

Callback procedures under your control may cause a considerable
computational overhead, and should only be activated when necessary. To
give you control of the frequency of callbacks, AIMMS provide three
separate suffices to trigger a callback procedure. Specifically, a
callback procedure can be called

-  after a specified number of iterations,

-  after a specified number of seconds,

-  after a change of status of the solution process, or

-  at every new incumbent during the solution process of a mixed integer
   program.

.. rubric:: Activated after iterations

With the suffix ``CallbackIterations`` you can indicate after how many
iterations the callback procedure specified by the ``CallbackProcedure``
suffix must be called again. If you specify the number 0 (default), no
such callbacks will be made.

.. rubric:: Activated after time

With the suffix ``CallbackTime`` you specify the name of the callback
procedure to be called when a certain number of seconds has elapsed.
When not specified (the default), no such callbacks are made.

.. rubric:: Activated after status change

With the suffix ``CallbackStatusChange`` you specify the name of the
callback procedure to be performed when the status of the solution
process changes. When not specified (the default), no such callbacks are
made.

.. rubric:: Activated after new incumbent

With the suffix ``CallbackIncumbent`` you specify the name of the
callback procedure to be performed when the solver finds a new incumbent
during the solution process of a mixed integer program. When not
specified (the default), no such callbacks are made.

.. rubric:: Watch objective values

During a callback procedure you can access various objective values as
they are reported by the solver during a mixed integer program through
several suffices of the mathematical program at hand. The following
suffices provide information about the objective values:

-  through the suffix ``Incumbent`` you can obtain the objective value
   of the best integer solution found so far,

-  through the suffix ``BestBound`` you can obtain the best bound on the
   objective value during the branch-and-bound process, and

-  through the suffix ``Objective`` you can obtain the current objective
   value reported by the solver at the precise time of the callback.

For mixed integer programs the suffix ``Objective`` will be meaningless
in most cases during the solution process.

.. rubric:: Watch intermediate solution values

In a callback procedure you can access the current solution values of
the variables in the mathematical program, and assign these to other
identifiers in your model. One possible use of this feature is to store
multiple feasible integer solutions of a mixed integer linear program.

.. _retrievecurrentvariablevalues-LR:

.. rubric:: The procedure :any:`RetrieveCurrentVariableValues`

For some solvers there may be a considerable overhead involved to
retrieve the current variable values during the running solution
process. Therefore, AIMMS will only do so when you explicitly call the
procedure

   *:any:`RetrieveCurrentVariableValues`\ (VariableSet)*

With the *VariableSet* argument you can specify the subset of the set
:any:`AllVariables` consisting of all (symbolic) variables for which you
want the current values to be retrieved. When you call this procedure
outside the context of a solver callback procedure, AIMMS will produce a
runtime error.

.. _GenerateCut-LR:

.. rubric:: Adding additional cuts

When you want to add additional cuts during the solution process of a
mixed integer program, you should install a callback procedure to
generate these constraints using the ``CallbackAddCut`` suffix. This
procedure is called at every node that has an LP-optimal solution with
an objective function value below the current cutoff and is integer
infeasible. The procedure allows you to add individual constraints using
the ``GenerateCut(row, local)`` function. The *row* argument should
always be a scalar reference to an existing constraint name in your
model. The *local* argument should be a scalar binary that indicates
whether the cut is a local cut (value 1) or a global one (value 0). The
*local* argument is an optional argument, and has a default of 1.

.. rubric:: Example

Consider a model with the following constraint.

.. code-block:: aimms

	Constraint Triangle_Cut {
	    IndexDomain  : (i1,i2,i3) | (i1 < i2) and (i2 < i3);
	    Definition   : x(i1) + x(i2) + x(i3) - y(i1,i2) - y(i1,i3) - y(i2,i3) <= 1;
	}

Then the following piece of code, when specified as the procedure body
of the ``CallbackAddCut`` procedure, will only add those triangle cuts
that are violated.

.. code-block:: aimms

	RetrieveCurrentVariableValues(AllVariables);

	for ( (i1,i2,i3) | (i1 < i2) and (i2 < i3) ) do
	    if ( x(i1) + x(i2) + x(i3) - y(i1,i2) - y(i1,i3) - y(i2,i3) > 1 + eps ) then
	        GenerateCut( Triangle_Cut(i1,i2,i3), 1 );
	    endif;
	endfor;

.. rubric:: Aborting the solution process

When you want to abort the solution process, you can set the suffix
``CallbackReturnStatus`` to ``'abort'`` during the execution of your
callback procedure, as in:

.. code-block:: aimms

	TransportModel.CallbackReturnStatus := 'abort' ;

After aborting the process, AIMMS will retrieve the current solution and
set the final solver status to ``UserInterrupt``.

.. rubric:: Example

Consider a mathematical program ``TransportModel`` which incorporates a
callback procedure. The following callback procedure will abort the
solution process if the total solution time exceeded 1800 seconds, and
if the progress is less than 1% compared to the last nonzero objective
function value.

.. code-block:: aimms

	if ( TransportModel.SolutionTime > 1800 [second] and PreviousObjective and
	     (TransportModel.Objective - PreviousObjective) < 0.01*PreviousObjective )
	then
	   TransportModel.CallbackReturnStatus := 'abort';
	else
	   PreviousObjective := TransportModel.Objective;
	endif;

.. _allsolutionstates-LR:

.. rubric:: Solver and program status

Both the ``ProgramStatus`` and the ``SolverStatus`` suffix take their
value in the predefined set :any:`AllSolutionStates` presented in
:ref:`this table <table:mp.status>`.

.. _table:mp.status:

.. table:: Mathematical program and solver status

   ========================== ========================
   Program status             Solver status
   ========================== ========================
   ``ProgramNotSolved``       ``SolverNotCalled``
   ``Optimal``                ``NormalCompletion``
   ``LocallyOptimal``         ``IterationInterrupt``
   ``Unbounded``              ``ResourceInterrupt``
   ``Infeasible``             ``TerminatedBySolver``
   ``LocallyInfeasible``      ``EvaluationErrorLimit``
   ``IntermediateInfeasible`` ``Unknown``
   ``IntermediateNonOptimal`` ``UserInterrupt``
   ``IntegerSolution``        ``PreprocessorError``
   ``IntermediateNonInteger`` ``SetupFailure``
   ``IntegerInfeasible``      ``SolverFailure``
   ``InfeasibleOrUnbounded``  ``InternalSolverError``
   ``UnknownError``           ``PostProcessorError``
   ``NoSolution``             ``SystemFailure``
   ========================== ========================