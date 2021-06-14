.. _sec:gmp.multiobjective:

Multi-objective Optimization
============================

.. rubric:: Multi-objective optimization

Multi-objective optimization deals with mathematical optimization
problems involving more than one objective function that have to be
optimized simultaneously. Optimal decisions need to take into account
the presence of trade-offs between two or more conflicting objectives.
For example, minimizing the travelling distance while minimizing the
travelling time (which might conflict if the shortest route is not the
fastest). AIMMS allows you to define multiple objectives for linear
models only. Multi-objective optimization in AIMMS is currently only
supported by CPLEX and Gurobi.

.. rubric:: Blended or lexicographic objective

You can define a mixture of blended and lexicographic (or hierarchical)
objectives. A blended objective consists of the linear combination of
several objectives with given weights. A lexicographic objective assumes
that the objectives can be ranked in order of importance. A solution is
considered lexicographically better than another solution if it is
better in the first objective where they differ (following the order).
For a minimization problem, an optimal solution is one that is
lexicographically minimal.

.. rubric:: The procedure :any:`GMP::Column::SetAsMultiObjective`

Currently, the only way to specify a multi-objective optimization model
is by using the GMP library. The procedure
:any:`GMP::Column::SetAsMultiObjective` can be used to mark a variable as
an objective used for multi-objective optimization. Typically, the
definition of such a variable defines the objective but the variable can
also be used in an equality constraint which then defines the objective.

.. rubric:: Example

Consider the following declarations

.. code-block:: aimms

	Variable TotalDistance {
	    Definition :  sum( (i,j), Distance(i,j) * X(i,j) );
	}
	Variable TotalTime {
	    Definition :  sum( (i,j), TravelTime(i,j) * X(i,j) );
	}

Here ``X(i,j)`` is a (binary) variable indicating whether the road
between :math:`i` and :math:`j` is used. The variables ``TotalDistance``
and ``TotalTime`` can be specified as objectives in a multi-objective
optimization model using:

.. code-block:: aimms

	GMP::Column::SetAsMultiObjective( genMP, TotalDistance, 2, 1.0, 0, 0.1 );
	GMP::Column::SetAsMultiObjective( genMP, TotalTime, 1, 1.0, 0, 0.0 );

In this example, AIMMS will only pass the coefficients of the variable
``X`` as the multi-objective coefficients to the solver, so
``Distance(i,j)`` for the first objective and ``TravelTime(i,j)`` for
the second objective. (In other words, the multi-objective variables
``TotalDistance`` and ``TotalTime`` will be substituted by their
definitions.) After solving the model, the objectives can be deleted by
calling the procedure :any:`GMP::Instance::DeleteMultiObjectives`.

.. rubric:: Priority and weight

The priority of the objective can be specified using the third argument
of the procedure :any:`GMP::Column::SetAsMultiObjective`. Its fourth
argument defines the weight by which the objective coefficients are
multiplied when forming a blended objective, i.e., if multiple
objectives have the same priority. The last two (optional) arguments
specify the absolute and relative tolerance respectively, which define
the amount by which a solution may deviate from the optimal value for
the objective.

.. rubric:: Mathematical program objective

In case of multi-objective optimization, the variable specified in the
``Objective`` attribute of the mathematical program will be treated as a
normal variable, that is, it will not be used as one of the
multi-objectives.