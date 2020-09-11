.. _sec:stoch.stoch:

Stochastic Parameters and Variables
===================================

.. rubric:: The set :any:`AllStochasticScenarios`

To allow the storage of scenario-dependent parameter and variable data
for multiple scenarios in a stochastic model, all such scenarios should
be added to the predefined set :any:`AllStochasticScenarios`. If your
application contains multiple stochastic models-each with different
scenario sets-the set :any:`AllStochasticScenarios` should be the union of
all these scenario sets. For each stochastic model you can then define
an associated subset of :any:`AllStochasticScenarios` to use with that
particular stochastic model.

.. rubric:: Stochastic parameters

Stochastic events are modeled in AIMMS as numeric ``Parameters`` for
which the ``Stochastic`` property has been set (see also
:ref:`sec:par.decl`). For stochastic parameters AIMMS provides an
additional :ref:`.Stochastic` suffix, which you can use to store
scenario-dependent stochastic event outcomes. The data stored in the
suffix is used by AIMMS when generating the stochastic model. The index
domain of the :ref:`.Stochastic` suffix is, therefore, the set
:any:`AllStochasticScenarios` plus the original domain of the parameter.

.. rubric:: Example

Consider the following declarations

.. code-block:: aimms

	Set MyScenarios {
	    SubsetOf     : AllStochasticScenarios;
	    Index        : sc;
	}
	Parameter Demand {
	    IndexDomain  : (c,t);
	    Property     : Stochastic;
	}

These declarations will cause AIMMS to create a :ref:`.Stochastic` suffix
for the parameter ``Demand(c,t)``. To use, or assign values to,
``Demand.Stochastic``, you must use an additional index into (a subset
of) :any:`AllStochasticScenarios`. The following statement provides an
example of such a statement.

.. code-block:: aimms

	Demand.Stochastic(sc,c,t) := Uniform(10,20);

If a constraint contains a reference to the parameter ``Demand``, AIMMS
will use the data in ``Demand.Stochastic`` to generate the appropriate
demand constraint for every scenario.

.. rubric:: Stochastic variables

By setting the ``Stochastic`` property for a ``Variable`` in your model,
you indicate to AIMMS that this variable may have multiple,
scenario-dependent, solutions when used in a stochastic model.
Consequently, when generating a matrix for the stochastic model, a
column will be generated conceptually for every single scenario.

.. rubric:: The ``Stage`` attribute

For stochastic variables you must also specify the mandatory ``Stage``
attribute. Through the ``Stage`` attribute you specify the stage at the
end of which the decision corresponding to the stochastic variable is to
be taken. The value of the ``Stage`` attribute must be an explicit
positive integer value, or a parameter reference involving some or all
of the indices on the index list of the declared variable.

.. rubric:: Non-anticipativity constraints...

As discussed in the previous section, for every scenario :math:`s_0`, a
stochastic variable :math:`x` gets its value :math:`x_{s_0}` at the end
of stage :math:`n` as specified in the ``Stage`` attribute of the
variable. In addition, its value is based on the specific outcomes of
the stochastic events for that scenario taking place during stages
:math:`1,\dots,n`, but only on the distribution of the stochastic event
outcomes for any further stages. Therefore, the value :math:`x_s` must
be equal to :math:`x_{s_0}` for every other scenario :math:`s` that
passes through the same node in the scenario tree at the end of stage
:math:`n` as :math:`s_0`. The constraints enforcing this equality are
called *non-anticipativity constraints*-they do not allow the solution
to anticipate on stochastic outcomes that lie beyond the stage as
specified by the ``Stage`` suffix.

.. rubric:: ...enforced explicitly or implicitly

When generating a stochastic model, AIMMS will automatically enforce the
non-anticipativity constraints, either by explicitly adding them to the
generated matrix, or implicitly by substituting a single representative
:math:`x_{s_0}` for every other variable :math:`x_s`. While enforcing
non-anticipativity in an implicit manner will drastically reduce the
matrix size, an explicit representation may be helpful for solvers able
to decompose the generated matrix.

.. rubric:: Non-stochastic variables

If a variable in a stochastic model has not been declared stochastic, it
is deterministic in the sense that it assumes the same value for every
scenario, as is the case with first stage variables.

.. rubric:: The :ref:`.Stochastic` suffix for variables

Variables can also have a :ref:`.Stochastic` suffix in AIMMS. It follows
the same rules for its index domain as the :ref:`.Stochastic` suffix of
parameters. AIMMS uses the :ref:`.Stochastic` suffix of variables to store
the solution data of a stochastic model after solving it. However,
contrary to stochastic parameters, AIMMS will not only create the
:ref:`.Stochastic` suffix for stochastic variables, but for *all* variables
that are involved in a stochastic model.

.. rubric:: Contents of :ref:`.Stochastic` suffix

The values stored in the :ref:`.Stochastic` suffix after solving a
stochastic model for each type of variable are as follows:

-  for stochastic variables, the :ref:`.Stochastic` suffix will contain the
   solution of the variable for each scenario,

-  for the objective variable, the :ref:`.Stochastic` suffix will contain
   the contribution to the objective of each scenario, as well as the
   weighted objective value of the stochastic model itself,

-  for any other non-stochastic variable, the :ref:`.Stochastic` suffix
   will contain the deterministic solution of that variable for the
   stochastic model.

As the solution of a stochastic model is entirely stored in the
:ref:`.Stochastic` suffix, the solution of the underlying deterministic
model remains completely intact after solving the stochastic model. This
makes it easy to visually, and/or programmatically, compare the
solutions of the deterministic and stochastic model.

.. rubric:: Non-stochastic solution data

As the objective value and solution of the non-stochastic variables of
the stochastic model cannot be coupled directly with one specific
scenario in the scenario set, AIMMS creates an extra element in the set
:any:`AllStochasticScenarios` for this purpose. You must specify the name
of this element when solving the stochastic model (see also
:ref:`sec:stoch.solve`).