.. _sec:stoch.solve:

Solving Stochastic Models
=========================

.. rubric:: Solving stochastic models

After generating stochastic event data and a scenario tree, you can
generate and solve the stochastic model by using methods from the GMP
library discussed in :ref:`chap:gmp`. AIMMS supports two methods for
solving a stochastic model:

-  by solving its *deterministic equivalent*, or

-  using the Benders decomposition algorithm in CPLEX.

The Benders algorithm will decompose the stochastic model into
multiple smaller models, and thus is better suited to solve stochastic
models where the deterministic equivalent, either by the size of the
deterministic model or because of a huge number of scenarios, becomes
too big or time-consuming to solve at once. The Benders decomposition
algorithm in CPLEX can be used to solve stochastic models with integer
variables, as long as all integer variables are assigned to the first
stage. For more information see the CPLEX option ``Benders_strategy``.

Generating and Solving the Deterministic Equivalent
---------------------------------------------------

.. rubric:: Generating a stochastic model

The method for generating a stochastic model for a
``MathematicalProgram`` *MP* is

-  :any:`GMP::Instance::GenerateStochasticProgram`\ ( *MP*,
   *StochasticParameters*, *StochasticVariables*, *Scenarios*,
   *ScenarioProbability*, *ScenarioTreeMap*,
   *DeterministicScenarioName*\ [, *GenerationMode*][, *Name*])

The function returns an element into the set
:any:`AllGeneratedMathematicalPrograms`. This generated math program
instance contains a memory-efficient representation of the technology
matrix of the stochastic model and the stochastic event data, and can be
used to create a deterministic equivalent of the stochastic model, as
well as the submodels necessary for a stochastic Benders approach.

.. rubric:: Specifying stochastic identifiers

Through the arguments *StochasticParameters* and *StochasticVariables*
you indicate to AIMMS which stochastic parameters and variables you want
to take into consideration when generating this stochastic model. These
arguments must be subsets of the predefined sets
:any:`AllStochasticParameters` and :any:`AllStochasticVariables`,
respectively. You may want to use real subsets, for instance, when your
AIMMS project contains multiple stochastic models, each referring only
to a subset of the stochastic parameters and variables.

.. rubric:: Specifying scenarios

Through the *Scenarios*, *ScenarioProbability* and *ScenarioTreeMap*
arguments you specify the set of scenarios, their probabilities and the
mapping defining the scenario tree for which you want to generate the
stochastic model to AIMMS. Through the string argument
*DeterministicScenarioName*, you supply the name of the artificial
element that AIMMS will add to the predefined set
:any:`AllStochasticScenarios` (if not created already), and use to store
the solution of non-stochastic variables in their respective
:ref:`.Stochastic` suffices as explained in :ref:`sec:stoch.stoch`.

.. rubric:: Enforcing non-anticipativity constraints

Using the *GenerationMode* argument you can specify whether you want
AIMMS to explicitly add the non-anticipativity constraints to your
stochastic model, or whether you want non-anticipativity to be enforced
implicitly by substituting the representative scenario for every
non-representative scenario at every stage. *GenerationMode* is an
element parameter into the predefined set
:any:`AllStochasticGenerationModes`, with possible values

-  ``'CreateNonAnticipativityConstraints'``, and

-  ``'SubstituteStochasticVariables'`` (the default value).

.. rubric:: Name argument

With the optional *Name* argument you can explicitly specify a name for
the generated mathematical program. If you do not choose a name, AIMMS
will use the name of the underlying ``MathematicalProgram`` as the name
of the generated mathematical program as well. Please note, that AIMMS
will also use this name as the default name for solving the
deterministic model. Therefore, if you do not want the generated
mathematical program of the deterministic model to be deleted, then you
have to choose a non-default name.

.. rubric:: Solving the deterministic equivalent of a stochastic model

You can solve a stochastic model by using the regular GMP procedure

-  :any:`GMP::Instance::Solve`\ (*gmp*)

By applying this function to a generated mathematical program associated
with a stochastic model, AIMMS will create the deterministic equivalent
and pass it to the appropriate LP/MIP solver. The
:any:`GMP::Instance::Solve` method is discussed in full detail in
:ref:`sec:gmp.instance`.

.. rubric:: Changing the model input

Note that, when you adjust the scenario tree map, the stochastic data,
the scenario probabilities, or the value of the ``Stage`` attribute of
some variables after you generated the stochastic model, you should
regenerate the stochastic model again to reflect these changes.

.. rubric:: Example

Consider the following call to
:any:`GMP::Instance::GenerateStochasticProgram`

.. code-block:: aimms

	GMP::Instance::GenerateStochasticProgram(
	    TransportModel, AllStochasticParameters, AllStochasticVariables,
	    MyScenarios, MyScenarioProbability, MyScenarioTreeMap,
	    "TransportModel", 'SubstituteStochasticVariables', "StochasticTransportModel");

After solving the generated stochastic model, its solution will be
stored as follows, where ``sc`` is an index into ``MyScenarios``

-  the per-scenario solution of a stochastic variable ``Transport(i,j)``
   will be stored in ``Transport.Stochastic(sc,i,j)``,

-  the deterministic solution of a non-stochastic variable
   ``InitialStock(i)`` will be stored in
   ``InitialStock.Stochastic('TransportModel',i)``,

-  the weighted objective value for the objective variable ``TotalCost``
   will be stored in ``TotalObjective.Stochastic('TransportModel')``,
   while the contribution by every scenario is available through
   ``TotalCost.Stochastic(sc)``.

.. _sec:stoch.benders:

Using the Stochastic Benders Algorithm
--------------------------------------

The stochastic Benders Algorithm is no longer available in the latest AIMMS versions.
