.. _sec:robust.uncertain:

Uncertain Parameters and Uncertainty Constraints
================================================

.. rubric:: Uncertain parameters

Uncertain parameters are modeled in AIMMS as numeric ``Parameters`` for
which the ``Uncertain`` property has been set (see also
:ref:`sec:par.decl`). When a parameter has been declared ``Uncertain``
AIMMS will create two new attributes ``Region`` and ``Uncertainty``.

.. rubric:: The ``Region`` attribute
   :name: attr:robust.region

The ``Region`` attribute of an uncertain parameter offers an easy way to
define the uncertainty set without the need to introduce additional
uncertain parameters. AIMMS supports a number of predefined regions
which you can enter here:

-  :math:`{\texttt{Box}}(l,u)`,

-  :math:`{\texttt{Ellipsoid}}(c,r)`, and

-  :math:`{\texttt{ConvexHull}}(s, v(s))`.

.. rubric:: ``Box`` example

If we want to specify that parameter ``A`` is uncertain and constrained
as follows:

.. math:: l(i,j) \leq A(i,j) \leq u(i,j)

then it suffices to specify the uncertainty set of ``A`` using its
``Region`` attribute as follows

.. code-block:: aimms

	Parameter A {
	    IndexDomain  : (i,j);
	    Property     : Uncertain;
	    Region       : Box( l(i,j), u(i,j) );
	}

where ``l(i,j)`` and ``u(i,j)`` are ordinary parameters in your model.

.. rubric:: ``Ellipsoid`` example

It is also possible to specify the region using an ``Ellipsoid`` region

.. code-block:: aimms

	Parameter A {
	    IndexDomain  : (i,j);
	    Property     : Uncertain;
	    Region       : Ellipsoid( A.level(i,j), r(i,j) );
	}

which leads to an uncertainty set for ``A`` defined as an ellipsoid
around the nominal value of ``A`` as follows:

.. math:: \sum_{i,j} \Bigg( \frac{A(i,j) - A.\mathit{level}(i,j)}{r(i,j)} \Bigg)^2 \leq 1.

.. rubric:: ``ConvexHull`` example

The region can also be defined as a ``ConvexHull`` region

.. code-block:: aimms

	Parameter A {
	    IndexDomain  : (i,j);
	    Property     : Uncertain;
	    Region          : ConvexHull( s, A_s(s,i,j) );
	}

which says that the uncertain parameter ``A`` belongs to an uncertainty
set that is described by the convex hull of the values of a collection
of values ``A_s`` for a given set of scenarios, i.e.,

.. math::

   \begin{align}
   A(i,j) &= \sum_s \lambda_s A_s(s,i,j)\\
       1      &=\sum_s \lambda_s, \qquad   \lambda_s \geq 0.
   \end{align}

.. rubric:: Dependencies

If there are two parameters ``A`` and ``B`` that both depend on
scenario-dependent data, then those scenarios can either be dependent or
independent. To differentiate between these two possibilities, AIMMS
uses the name of the binding index used in the ``ConvexHull`` operator.
If the names of the binding indices are identical, then AIMMS assumes
that the scenarios are dependent. If the index names are different,
*even if they refer to the same scenario set*, AIMMS assumes the
scenarios to be independent.

.. rubric:: Dependent scenarios example

Consider the following two declarations of uncertain parameters

.. code-block:: aimms

	Parameter A {
	    IndexDomain  :  (i,j);
	    Property     :  Uncertain;
	    Region       :  ConvexHull( s, A_s(s,i,j) );
	}
	Parameter B {
	    IndexDomain  :  (i,j);
	    Property     :  Uncertain;
	    Region       :  ConvexHull( s, B_s(s,i,j) );
	}

Based on these declarations AIMMS will generate a single convex hull as
follows

.. math::

   \begin{align}
   \begin{bmatrix}A(i,j)\\B(i,j)\end{bmatrix} = &\sum_s \lambda_s \begin{bmatrix}A_s(s,i,j)\\B_s(s,i,j)\end{bmatrix}\\
       \sum_s \lambda_s =& 1, \qquad \lambda_s \geq 0.
   \end{align}

If ``A`` and ``B`` consist of a single value each, and there are two
scenarios for ``s``, then the combined convex hull for ``A`` and ``B``
is depicted in :numref:`fig:robust.ch1`.

.. figure:: uncertain-parameters-and-uncertainty-constraints-pspic1.svg
   :name: fig:robust.ch1

   Combined convex hull for dependent scenarios

.. rubric:: Independent scenarios example

If, on the other hand, both declarations are given as

.. code-block:: aimms

	Parameter A {
	    IndexDomain  :  (i,j);
	    Property     :  Uncertain;
	    Region       :  ConvexHull( s, A_s(s,i,j) );
	}
	Parameter B {
	    IndexDomain  :  (i,j);
	    Property     :  Uncertain;
	    Region       :  ConvexHull( t, B_t(t,i,j) );
	}

then AIMMS will generate two separate convex hulls as follows

.. math::

   \begin{align}
   \begin{bmatrix}A(i,j)\\B(i,j)\end{bmatrix} = & 
             \begin{bmatrix}\sum_{s}\lambda_s A_s(s,i,j)\\\sum_{t}\mu_t B_t(t,i,j)\end{bmatrix}\\
           \sum_s \lambda_s=&\sum_t \mu_t = 1, \qquad \lambda_s \geq 0, \mu_t \geq 0.
   \end{align}

If ``A`` and ``B`` consist of a single value each, and there are two
scenarios for ``s`` and ``t`` each, then the combined convex hull for
``A`` and ``B`` is depicted in :numref:`fig:robust.ch2`.

.. figure:: uncertain-parameters-and-uncertainty-constraints-pspic2.svg
   :name: fig:robust.ch2

   Combined convex hull for independent scenarios

.. rubric:: ``ConvexHullEx``

The ``ConvexHull`` operator AIMMS can be used to express that an
uncertain parameter is defined as the convex combination of a certain
parameter on some set of scenarios. The ``ConvexHullEx`` operator is an
extension for which the user explicitly has to define the "lambda"
parameter as an uncertain parameter. For example:

.. code-block:: aimms

	Parameter A {
	    IndexDomain  : (i,j);
	    Property     : Uncertain;
	    Region          : ConvexHullEx( s, A_s(s,i,j), L(s,i) );
	}

which says that the uncertain parameter ``A`` belongs to an uncertainty
set that is described by the convex hull of the values of a collection
of values ``A_s`` for a given set of scenarios using the uncertain
parameter ``L``, i.e.,

.. math::

   \begin{align}
   A(i,j) &= \sum_s L_s(i) A_s(s,i,j)\\
       1      &=\sum_s L_s(i), \qquad   L_s(i) \geq 0.
   \end{align}

.. rubric:: More flexibility

The ``ConvexHullEx`` operator offers more flexibility as demonstrated by
the above example in which the *lambda* parameter ``L`` depends on the
indices ``s`` and ``i`` while the implicitly generated *lambda*
parameter in case of the ``ConvexHull`` operator only depends on the
index ``s``. Moreover, the *lambda* parameter can be used in the
``Dependency`` attribute of an adjustable variable (see
:ref:`sec:robust.adjustable`). The same *lambda* parameter can be used
in ``ConvexHullEx`` in regions of different uncertain parameters to
define a dependency between the uncertain parameters. As the *lambda*
parameter is not an ordinary uncertainty parameter, it cannot be used in
uncertainty constraints.

.. rubric:: The ``Uncertainty`` attribute
   :name: attr:robust.uncertainty

Through the ``Uncertainty`` attribute of an uncertain parameter you can
define a relation in term of other ordinary and uncertain parameters in
your model which must hold for the uncertain value of that parameter.

.. rubric:: Example

Consider the following declaration

.. code-block:: aimms

	Parameter Demand {
	    IndexDomain  : (c,t);
	    Property     : Uncertain;
	    Uncertainty  : Demand.level(c,t) + Sum[k, D(c,t,k) * xi(k)];
	}

where ``D(c,t,k)`` is an ordinary parameter and ``xi`` an uncertain
parameter. The reference to ``Demand.level`` in the ``Uncertainty``
attribute refers to the deterministic (or nominal) value of ``Demand``.
The uncertain value of ``Demand`` is defined as its nominal value plus a
linear combination of some other uncertain parameter ``xi(k)``.

.. rubric:: Non-exclusive attributes

Note that the ``Region`` and ``Uncertainty`` attributes are
non-exclusive, i.e., you can use them in conjuction to each other. In
such a case, AIMMS will make sure that the solution is robust with
respect to both relations.

.. rubric:: Uncertainty constraints

The ``Region`` and the ``Uncertainty`` attribute of a uncertain
parameter can be used to specify possible realizations of the uncertain
parameters. In some cases, however, more flexibility is needed in
specifying special relations for one or more uncertain parameters. For
this purpose AIMMS allows you to specify ``UncertaintyConstraints``. An
``UncertaintyConstraint`` is a constraint that specifies the relation
between uncertain parameters. It is similar to an ordinary constraint in
which the uncertain parameters play the role for variables; the
definition of an ``UncertaintyConstraint`` may only refer to normal and
uncertain parameters, and not to variables.

.. rubric:: Example

The following example specifies a condition on an uncertain parameter
that cannot be expressed through its ``Region`` or ``Uncertainty``
attributes.

.. code-block:: aimms

	Parameter A {
	    IndexDomain  : (i,j);
	    Property     : Uncertain;
	}
	UncertaintyConstraint ConditionOnA {
	    IndexDomain  : i;
	    Definition   : Sum( j, A(i,j) ) <= 1;
	}

.. rubric:: The ``Constraints`` attribute
   :name: attr:robust.constraints

Through the ``Constraint`` attribute of an ``UncertaintyConstraint`` you
can specify to which (normal) constraints the ``UncertaintyConstraint``
should apply. In this way it is possible to use different uncertainty
sets for different constraints. If the ``Constraints`` attribute is
empty then the ``UncertaintyConstraint`` will be active for all
constraints.

.. rubric:: Example

Consider the following declarations

.. code-block:: aimms

	UncertaintyConstraint ConditionOnA {
	    IndexDomain  : i;
	    Constraints  : CapacityRestriction(j) : UncertaintyDependency(i,j);
	    Definition   : Sum( j, A(i,j) ) <= 1;
	}
	Constraint CapacityRestriction {
	    IndexDomain  : j;
	    Definition   : Sum( i, A(i,j) * Transport(i,j) ) <= Capacity(j);
	}
	Parameter UncertaintyDependency {
	    IndexDomain  : (i,j);
	    Definition   : 1 $ (i = j);
	}

These declarations yield that the uncertainty constraint
``ConditionOnA(i)`` is only active for constraint
``CapacityRestriction(j)`` for all elements ``j`` equal to ``i``.

.. rubric:: Generalized ellipsoid

Besides linear uncertainty constraints, AIMMS also allows you to
formulate the following uncertainty set for a uncertain parameter
:math:`\xi`, that generalizes the ellipsoidal uncertainty sets that can
be defined by using the ``Ellipsoid`` region:

.. math:: \xi^T Q_0 \xi + \sum_{m=1}^{M} \sqrt{\xi^T Q_m \xi} \le b,

where :math:`Q_0` and :math:`Q_m` should be positive semidefinite
matrices. If your model contains an ellipsoidal uncertainty constraint
then the robust counterpart will become a second-order cone program,
except if the ellipsoidal uncertainty constraints are of the form

.. math:: \sum_i \sqrt{\xi_i^2} \le b,

in which case the robust counterpart will be a linear program.