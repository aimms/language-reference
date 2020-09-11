.. _sec:robust.adjustable:

Adjustable Variables
====================

.. rubric:: Adjustable variables

An *adjustable variable* reflects a decision made after uncertain data
has been revealed. In robust optimization this is interpreted as the
adjustable variable taking some (explicit or implicit) functional form
in terms of the uncertain data on which it depends. In AIMMS, you
indicate that a ``Variable`` should be treated as adjustable by setting
its ``Adjustable`` property.

.. rubric:: The ``Dependency`` attribute
   :name: attr:robust.dependency

For any adjustable variable, AIMMS will create a ``Dependency``
attribute which you can use to specify on which uncertain parameters the
variable depends. The attribute value must be a comma-separated list of
mappings from an uncertain parameter to a binary parameter, indicating
for which combination of indices a dependency exists on that uncertain
parameter.

.. rubric:: Linear decision rule only

AIMMS currently only supports the *linear decision rule*, which means
any adjustable variable will be expressed as an affine relation in terms
of the uncertain parameters which it depends on. More explicitly, if an
adjustable variable :math:`x(t)` depends on uncertain parameters
:math:`d_r`, then, under the linear decision rule, AIMMS assumes that
:math:`x(t)` takes the form

.. math:: x(t) = X_0(t) + \sum_r X_r(t) d_r

where :math:`X_0(t)` and :math:`X_r(t)` are newly introduced
intermediate variables, the value of which is determined by solving the
robust counterpart. As such, the value of an adjustable variable is not
fully determined by the solver. It can be computed afterwards for a
given realization of the uncertain parameters. AIMMS will automatically
generate the affine relation based on the dependencies you indicated in
the ``Dependency`` attribute, without the need for you to introduce the
appropriate intermediate variables.

.. rubric:: Requirements for adjustable variables

In order for AIMMS to be able to generate the robust counterpart of a
robust optimization model, the model must satisfy the *fixed recourse*
condition, i.e., the coefficients of any adjustable variables in your
model must not depend on uncertain parameters. In addition, for AIMMS to
be able to generate the robust counterpart, adjustable variables may
*not* occur in chance constraints. Also, adjustable variables cannot be
integer.

.. rubric:: The ``.Adjustable`` suffix for variables

The collection of intermediate variables introduced during this process,
automatically becomes available through the ``.Adjustable`` attribute of
the adjustable variable at hand, followed by the name of the uncertain
parameter involved. That is, if an adjustable variable ``x(i)`` depends
on an uncertain parameter ``a(j)``, then the corresponding intermediate
variable is available as the expression ``x.Adjustable.a(i,j)``. In
addition, a variable ``x.Adjustable.Constant(i)`` will be created to
account for the constant part of the affine relation. If necessary, you
can bound these variables through the :ref:`.Lower` and :ref:`.Upper`
suffices, or you can formulate additional constraints on these
variables.

.. rubric:: Example

Consider the following declarations

.. code-block:: aimms

	Variable Stock {
	    IndexDomain  :  t;
	    Property     :  Adjustable;
	    Dependency   :  Demand(t2) : StockDemandDependency(t,t2);
	}
	Parameter Demand {
	    IndexDomain  :  t;
	    Property     :  Uncertain;
	}
	Parameter StockDemandDependency {
	    IndexDomain  :  (t,t2);
	    Definition   :  1 $ (t2 < t);
	}

These declarations yield that the adjustable variable ``Stock(t)``
depends on the uncertain parameter ``Demand(t2)`` for all elements
``t2`` smaller than ``t``. Given these declarations, AIMMS will generate
the following definition for ``Stock(t)``

.. code-block:: aimms

	Stock(t) = Stock.Adjustable.Constant(t) + 
	           sum(t2 | StockDemandDependency(t,t2), Stock.Adjustable.Demand(t,t2)*Demand(t2))

If the data for ``Demand(t)`` becomes available, you can use the
computed values of ``Stock.Adjustable.Demand(t,t2)`` and
``Stock.Adjustable.Constant`` to compute the value of ``Stock(t)``.

.. rubric:: Warning: using same indices

You should be aware that using the same indices in the ``Dependency``
attribute and the index domain of the adjustable variable will restrict
the dependencies that are generated. For example, assume we have the
following declarations

.. code-block:: aimms

	Variable Stock {
	    IndexDomain  :  t;
	    Property     :  Adjustable;
	    Dependency   :  Demand(t);
	}
	Parameter Demand {
	    IndexDomain  :  t;
	    Property     :  Uncertain;
	}

Given these declarations, AIMMS will generate the following definition
for ``Stock(t)``

.. code-block:: aimms

	Stock(t) = Stock.Adjustable.Constant(t) + Stock.Adjustable.Demand(t)*Demand(t)

If you want ``Stock(t)`` to depend on all possible ``Demand`` then you
should use a different index in the ``Dependency`` attribute, e.g.,

.. code-block:: aimms

	Variable Stock {
	    IndexDomain  :  t;
	    Property     :  Adjustable;
	    Dependency   :  Demand(t2);
	}

.. rubric:: Evaluating adjustable variables

To compute the values of an adjustable variable for a given realization
of the uncertain parameters of the robust optimization model, you do not
have to explicitly add the appropriate definitions to your model. AIMMS
offers the function :any:`GMP::Robust::EvaluateAdjustableVariables`,
discussed in :ref:`sec:gmp.robust`, to automatically compute these
values for you.