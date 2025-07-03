.. _sec:robust.chance:

Chance Constraints
==================

.. rubric:: Chance constraints

In the previous sections we assumed that each constraint with uncertain
data was satisfied with probability 1. In many situations, however, such
a requirement may lead to solutions that over-emphasize the worst-case.
In such cases, it is more natural to require that a candidate solution
has to satisfy a constraint with uncertain data for "nearly all"
realizations of the uncertain data. More specifically, in this approach
one requires that the robust solution has to satisfy the constraint with
probability at least :math:`1 - \epsilon`, where
:math:`\epsilon \in [0,1]` is a pre-specified small tolerance. Instead
of the deterministic constraint

.. math:: a^T x \leq b

we now require that the *chance constraint*

.. math:: \text{Prob} \left(x : a(\xi)^T x \le b \right) \geq 1 - \epsilon

be satisfied, where the probability is associated with the specific
distribution of the uncertain parameter(s) :math:`\xi`.

.. rubric:: Approximation

In general, (linear) problems with chance constraints are very hard to
solve even if the probability distribution of the uncertain data is
completely known. It is, however, possible to construct safe tractable
approximations of chance constraints using robust optimization (see, for
instance, Chapter 2 of :cite:`bib:BGN09`). The way a chance constraint is
approximated depends merely on the general characteristics of the data
distribution, rather than on precise specification of the distribution.
If more information is available about the distribution, this will
generally result in a tighter approximation. A tighter approximation,
however, could result in a more difficult solution process (for
instance, requiring second-order cone programming instead of just linear
programming).

.. rubric:: Chance constraints in AIMMS

The procedure to introduce chance constraints into your robust
optimization model is as follows:

-  indicate which parameters in your model should become random, and
   specify the properties of their distributions, and

-  specify which constraints should be considered chance constraints,
   and specify their probability and method of approximation.

.. rubric:: Random parameters
   :name: attr:robust.distribution

A probability distribution is modeled in AIMMS as a numeric
``Parameter`` for which the ``Random`` property has been set (see also
:ref:`sec:par.decl`). If the property ``Random`` is set, AIMMS will
create the mandatory ``Distribution`` attribute for this parameter which
must be used to specify the characteristics of the distribution to be
used for that parameter. All random parameters for which a distribution
has been specified are considered to be independent.

.. rubric:: Example

Consider the following declaration

.. code-block:: aimms

	Parameter Demand {
	    IndexDomain  : i;
	    Property     : Random;
	    Distribution : Bounded(Demand(i).level,0.1);
	}

This declaration states that parameter ``Demand`` corresponds to a
bounded probability distribution with a mean equal to the nominal value
of ``Demand`` and a support of 0.1.

.. rubric:: Supported distributions

AIMMS supports the distribution types listed in
:numref:`fig:robust.distributions`

.. _fig:robust.distributions:

.. table:: Supported distribution types for robust optimization

	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| Distribution                              | Meaning                                                                                       |
	+===========================================+===============================================================================================+
	| :math:`{\texttt{Bounded}}(m,s)`           | mean :math:`m` with range :math:`[m-s,m+s]`                                                   |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Bounded}}(m,l,u)`         | range :math:`[l,u]` and mean :math:`m` not in the center of the range                         |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Bounded}}(m_l,m_u,l,u)`   | range :math:`[l,u]` and mean in interval :math:`[m_l,m_u]`                                    |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Bounded}}(m_l,m_u,l,u,v)` | range :math:`[l,u]` and mean in interval :math:`[m_l,m_u]`, and variance bounded by :math:`v` |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Unimodal}}(c,s)`          | unimodal around :math:`c` with range :math:`[c-s,c+s]`                                        |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Symmetric}}(c,s)`         | symmetric around :math:`c` with range :math:`[c-s,c+s]`                                       |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Symmetric}}(c,s,v)`       | symmetric around :math:`c` with range :math:`[c-s,c+s]`, and variance bounded by :math:`v`    |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Support}}(l,u)`           | range :math:`[l,u]` (and no information about the mean)                                       |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+
	| :math:`{\texttt{Gaussian}}(m_l,m_u,v)`    | Gaussian with mean in interval :math:`[m_l,m_u]` and variance bounded by :math:`v`            |
	+-------------------------------------------+-----------------------------------------------------------------------------------------------+

All distributions in this table are bounded except the Gaussian
distribution. The distributions :math:`{\texttt{Bounded}}(m_l,m_u,l,u)`,
:math:`{\texttt{Bounded}}(m_l,m_u,l,u,v)` and
:math:`{\texttt{Symmetric}}(c,s,v)` are currently not implemented.

.. rubric:: Symmetric unimodal distribution

A distribution is called unimodal if its density function is
monotonically increasing up to a certain point :math:`c` and
monotonically decreasing afterwards. For symmetric distribution AIMMS
offers the possibility to mark it as unimodal by using the ``unimodal``
keyword:

.. code-block:: aimms

	Parameter Demand {
	    IndexDomain  : i;
	    Property     : Random;
	    Distribution : Symmetric(Demand(i).level,0.1), unimodal;
	}

The ``unimodal`` keyword can only be used in combination with a
symmetric distribution.

.. rubric:: Linear relation

In addition to specifying a random parameter using an independent
distribution, AIMMS also allows you to define a random parameter as a
linear combination of other random parameters (but not as combination of
uncertain parameters). For example,

.. code-block:: aimms

	Parameter Demand {
	    Property     : Random;
	    Distribution : Sum( i, xi(i) );
	}

where ``xi`` is an random parameter. To avoid cyclic definitions, AIMMS
requires that the distributions of random parameters cannot be specified
as an expression of other random parameters which are themselves defined
as an expression of random parameters.

.. rubric:: Chance constraints

A constraint in your mathematical program becomes a chance constraint in
the context of robust optimization by setting its ``Chance`` property.
The definition of a chance constraint may only contain random
parameters, normal parameters and variables. Uncertain parameters are
not allowed inside a chance constraint. When setting the ``Chance``
property for a constraint, you must specify two new attributes for the
constraint, the ``Probability`` attribute and the ``Approximation``
attribute. It is allowed to use chance constraints in a mixed-integer
program.

.. _attr:robust.chance.probability:

.. rubric:: The ``Probability`` attribute

The ``Probability`` attribute specifies the probability with which the
chance constraint should be satisfied when solving a robust optimization
model. The value of the ``Probability`` attribute should be a numerical
expression in the range :math:`[0,1]`. If the probability is 0, then
AIMMS will not generate the chance constraint. If the probability is 1,
then AIMMS will generate an uncertainty constraint.

.. _attr:robust.chance.approximation:

.. rubric:: The ``Approximation`` attribute

The ``Approximation`` attribute is used to define the approximation that
should be used to approximate the chance constraint. Its value should be
an element expression into the predefined set
``AllChanceApproximationTypes``.

.. rubric:: Supported approximation types

The approximations supported by AIMMS are:

-  *Ball*,

-  *Box*,

-  *Ball-box*,

-  *Budgeted*, and

-  *Automatic*.

A detailed mathematical definition of these approximation types can be
found in Chapter 2 of :cite:`bib:BGN09`. Whether or not a particular
approximation type is possible, depends on the characteristics of the
distributions used in the chance constraint, as explained below. By
specifying approximation type *Automatic* the most accurate
approximation possible will be used. In some cases it might be
beneficial to use a less tight approximation because it leads to a
robust counterpart that is easier to solve.

.. rubric:: Example

Consider the declaration

.. code-block:: aimms

	Constraint ChanceConstraint {
	    IndexDomain   : i;
	    Property      : Chance;
	    Definition    : Demand(i) * X(i) <= 10;
	    Probability   : prob(i);
	    Approximation : 'Ball';
	}

This declaration states that ``ChanceConstraint`` is a chance constraint
with probability ``prob(i)``, and that approximation type *Ball* is used
to approximate the chance constraint.

.. rubric:: Possible approximations per distribution

The :ref:`table <table:robust.chance-approximations>` below shows for each (supported)
distribution which approximation types are possible. It also shows
whether the approximation will result in a linear or a second-order cone
robust counterpart.

.. _table:robust.chance-approximations:

.. table:: Allowed approximations and their resulting problem type

	+----------------------------------------------+-----------+-------+--------+----------+----------+
	| Distribution                                 | Automatic | Ball  | Box    | Ball-box | Budgeted |
	+==============================================+===========+=======+========+==========+==========+
	| :math:`{\texttt{Bounded}}(m,s)`              | linear    | conic | linear | conic    | linear   |
	+----------------------------------------------+-----------+-------+--------+----------+----------+
	| :math:`{\texttt{Bounded}}(m,l,u)`            | conic     |       | linear |          |          |
	+----------------------------------------------+-----------+-------+--------+----------+----------+
	| :math:`{\texttt{Unimodal}}(c,s)`             | conic     |       | linear |          |          |
	+----------------------------------------------+-----------+-------+--------+----------+----------+
	| :math:`{\texttt{Symmetric}}(c,s)` (unimodal) | conic     | conic | linear | conic    | linear   |
	+----------------------------------------------+-----------+-------+--------+----------+----------+
	| :math:`{\texttt{Support}}(l,u)`              | linear    |       | linear |          |          |
	+----------------------------------------------+-----------+-------+--------+----------+----------+
	| :math:`{\texttt{Gaussian}}(m_l,m_u,v)`       | conic     |       |        |          |          |
	+----------------------------------------------+-----------+-------+--------+----------+----------+

For the :math:`{\texttt{Bounded}}(m,s)` distribution the automatic
approximation equals the *Budgeted* approximation, and the automatic
approximation of the :math:`{\texttt{Support}}(l,u)` distribution equals
the *Box* approximation. The non-unimodal
:math:`{\texttt{Symmetric}}(c,s)` distribution is treated as a
:math:`{\texttt{Bounded}}(m,s)` distribution.

.. rubric:: Combining distributions

A chance constraint cannot contain both bounded random parameters and
Gaussian random parameters. Different types of bounded random parameters
can be combined, in which case only a part of the available information
will be used. The possible combinations of bounded random parameters are
given in :ref:`this table <table:robust.distr-mix>`.

.. _table:robust.distr-mix:

.. table:: Resulting distribution type when combining distributions

	=== ============================================ = = = = =
	    Distribution                                 1 2 3 4 5
	=== ============================================ = = = = =
	1   :math:`{\texttt{Bounded}}(m,s)`              1 2 - 1 5
	2   :math:`{\texttt{Bounded}}(m,l,u)`            2 2 - 2 5
	3   :math:`{\texttt{Unimodal}}(c,s)`             - - 3 3 5
	4   :math:`{\texttt{Symmetric}}(c,s)` (unimodal) 1 2 3 4 5
	5   :math:`{\texttt{Support}}(l,u)`              5 5 5 5 5
	=== ============================================ = = = = =

.. rubric:: Explanation

If a random parameter with a :math:`{\texttt{Bounded}}(m,l,u)`
distribution and a random parameter with a
:math:`{\texttt{Support}}(l,u)` distribution are used in a single chance
constraint, then :ref:`this table <table:robust.distr-mix>` states that the
:math:`{\texttt{Bounded}}(m,l,u))` distribution of the first random
parameter will be treated as a :math:`{\texttt{Support}}(l,u)`
distribution. Unimodal distributions can only be mixed with unimodal
:math:`{\texttt{Symmetric}}(c,s)` and :math:`{\texttt{Support}}(l,u)`
distributions.