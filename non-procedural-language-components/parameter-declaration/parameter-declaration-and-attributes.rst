.. _sec:par.decl:

``Parameter`` Declaration and Attributes
========================================

.. _parameter:

.. _string_parameter:

.. _element_parameter:

.. rubric:: Declaration and attributes

There are four parameter types in AIMMS that can hold data of the
following four data types:

-  ``Parameter`` for numeric values,

-  ``StringParameter`` for strings,

-  ``ElementParameter`` for set elements, and

-  ``UnitParameter`` for unit expressions.

Prior to declaring a parameter in the model editor you need to decide on
its data type. In the model tree parameters of each type have their own
icon. The attributes of parameters are given in
:numref:`table:par.attr-param`.

.. _table:par.attr-param:

.. table:: 

	+------------------+-----------------------------+---------------------------------------------------------------+
	| Attribute        | Value-type                  | See also page                                                 |
	+==================+=============================+===============================================================+
	| ``IndexDomain``  | *index-domain*              |                                                               |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Range``        | *range*                     |                                                               |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Default``      | *constant-expression*       |                                                               |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| :any:`Unit`      | *unit-expression*           |                                                               |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Property``     | ``NoSave``, ``Stochastic``, |                                                               |
	+------------------+-----------------------------+---------------------------------------------------------------+
	|                  | ``Uncertain``, ``Random``,  |                                                               |
	+------------------+-----------------------------+---------------------------------------------------------------+
	|                  | *numeric-storage-property*  | :ref:`sec:par.uncertainty`                                    |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Text``         | *string*                    | :ref:`attr:prelim.text`                                       |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Comment``      | *comment string*            | :ref:`attr:prelim.comment`, :ref:`attr:set.comment`           |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Definiton``    | *expression*                | :ref:`attr:set.definition`                                    |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``InitialData``  | *data enumeration*          | :ref:`attr:par.initialdata`                                   |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Uncertainty``  | *expression*                | :ref:`attr:par.uncertainty`, :ref:`attr:robust.uncertainty`   |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Region``       | *expression*                | :ref:`attr:par.region`, :ref:`attr:robust.region`             |
	+------------------+-----------------------------+---------------------------------------------------------------+
	| ``Distribution`` | *expression*                | :ref:`attr:par.distribution`, :ref:`attr:robust.distribution` |
	+------------------+-----------------------------+---------------------------------------------------------------+
	
.. rubric:: Basic examples

The following declarations demonstrate some basic parameter declarations

.. code-block:: aimms

	Parameter Population {
	     IndexDomain  :  i;
	     Range        :  [0,inf);
	     Unit         :  [ 1000 ];
	     Text         :  Population of city i in thousands;
	}
	Parameter Distance {
	     IndexDomain  :  (i,j);
	     Range        :  [0,inf);
	     Unit         :  [ km ];
	     Text         :  Distance from city i to city j in km;
	}
	ElementParameter cityWithLargestPopulation {
	     Range        :  cities;
	     Definition   :  argMax( i, Population( i ) );
	}
	StringParameter emergencyMessage {
	     InitialData :  "Warning";
	}
	Quantity Currencies {
	     BaseUnit     :  dollar;
	     Conversions  :  euro -> dollar : # -> # * 1.3;
	}
	UnitParameter selectedCurrency {
	     InitialData :  [euro];
	}

.. rubric:: The ``IndexDomain`` attribute
   :name: attr:par.index-domain

.. _parameter.index_domain:

For each multidimensional identifier you need to specify its dimensions
by providing a list of index bindings at the ``IndexDomain`` attribute.
Identifiers without an ``IndexDomain`` are said to be *scalar*. In the
index domain you can specify default or local bindings to simple sets.
The totality of dimensions of all bindings determine the total dimension
of the identifier. Any references outside the index domain, either
through execution statements or from within the graphical user interface
are skipped.

.. rubric:: Domain condition

You can also use the ``IndexDomain`` attribute to specify a logical
expression which further restricts the valid tuples in the domain.
During execution, assignments to tuples that do not satisfy the domain
condition are ignored. Also, evaluation of references to such tuples in
expressions will result in the value zero. Note that, if the domain
condition contains references to other data in your model, the set of
valid tuples in the domain may change during a single interactive
session.

.. rubric:: Example

Consider the sets ``ConnectedCities`` with default index ``cc`` and
``DestinationCitiesFromSupply(i)`` from the previous chapter. The
following statements illustrate a number of possible declarations of the
two-dimensional identifier ``UnitTransportCost`` with varying index
domains.

.. code-block:: aimms

	Parameter UnitTransportCost {
	    IndexDomain : (i,j);
	}
	Parameter UnitTransportCostWithCondition {
	    IndexDomain : (i,j) in ConnectedCities;
	}
	Parameter UnitTransportCostWithIndexedDomain {
	    IndexDomain : (i, j in DestinationCitiesFromSupply(i)); 
	}

.. rubric:: Explanation

The identifiers defined in the previous example will behave as follows.

-  The identifier ``UnitTransportCost`` is defined over the full
   Cartesian product ``Cities`` :math:`\times` ``Cities`` by means of
   the default bindings of the indices ``i`` and ``j``. You will be able
   to assign values to every pair of cities (``i``,\ ``j``), even though
   there is no connection between them.

-  The identifier ``UnitTransportCostWithCondition`` is defined over the
   same Cartesian product of sets. Its domain, however, is restricted by
   an additional condition ``(i,j) in ConnectedCities`` which will
   exclude assignments to tuples that do not satisfy this condition, or
   evaluate to zero when referenced.

-  Finally, the identifier ``UnitTransportCostWithIndexedDomain`` is
   defined over a subset of the Cartesian product ``Cities``
   :math:`\times` ``Cities``. The second element ``j`` must lie in the
   subset ``DestinationCities(i)`` associated with ``i``. AIMMS will
   produce a domain error if this condition is not satisfied.

.. rubric:: The ``Range`` attribute
   :name: attr:par.range

.. _parameter.range:

With the ``Range`` attribute you can restrict the values to certain
intervals or sets. The ``Range`` attribute is not applicable to a
``StringParameter`` nor to a ``UnitParameter``. The possible values for
the ``Range`` attribute are:

-  one of the predefined ranges ``Real``, ``Nonnegative``,
   ``Nonpositive``, ``Integer``, or ``Binary``,

-  any one of the interval expressions ``[``\ :math:`a,b`\ ``]``,
   ``[``\ :math:`a,b`\ ``)``, ``(``\ :math:`a,b`\ ``]``, or
   ``(``\ :math:`a,b`\ ``)``, where a square bracket implies inclusion
   into the interval and a round bracket implies exclusion,

-  any enumerated integer set expression, e.g. ``{``\ :math:`a` ``..``
   :math:`b`\ ``}`` covering all integers from :math:`a` until and
   including :math:`b`,

-  a set reference, if you want the values to be elements of that set.
   For set element-valued parameters this entry is mandatory.

The values for :math:`a` and :math:`b` can be a constant number,
``inf``, ``-inf``, or a parameter reference involving some or all of the
indices on the index domain of the declared identifier.

.. rubric:: Example

Consider the following declarations.

.. code-block:: aimms

	Parameter UnitTransportCost {
	    IndexDomain  :  (i,j);
	    Range        :  [ UnitLoadingCost(i), 100 ];
	}
	Parameter  DefaultUnitsShipped {
	    IndexDomain  :  (i,j);
	    Range        :  {
	        { MinShipment(i) .. MaxShipment(j) }
	    }
	}
	Set States {
	    Index        :  s;
	}
	Set adjacentStates {
	    SubsetOf     :  States;
	    IndexDomain  :  s;
	}
	ElementParameter nextState {
	    IndexDomain  :  s;
	    Range        :  adjacentStates(s);
	}

It limits the values of the identifier ``UnitTransportCost(i,j)`` to an
interval from ``UnitLoadingCost(i)`` to 100. Note that the lower bound
of the interval has a smaller dimension than the identifier itself. The
integer identifier ``DefaultUnitsShipped(i,j)`` is limited to an integer
range through an enumerated integer range inside the set brackets.

.. rubric:: The ``Default`` attribute
   :name: attr:par.default

.. _parameter.default:

In AIMMS, parameters that have not been assigned an explicit value are
given a default value automatically. You can specify the default value
with the ``Default`` attribute. The value of this attribute *must* be a
constant expression. If you do not provide a default value for the
parameter, AIMMS will assume the following defaults:

-  :math:`0` for numbers,

-  :math:`1` for unit-valued parameters,

-  the empty string ``""`` for strings, and

-  the empty element ``"`` for set elements.

.. rubric:: The ``Definition`` attribute
   :name: attr:par.definition

.. _parameter.definition:

The ``Definition`` attribute of a parameter can contain a valid
(indexed) numerical expression. Whenever a defined parameter is
referenced inside your model, AIMMS will, by default, recompute the
associated data if (data) changes to any of the identifiers referenced
in its definition make its current data out-of-date. In the definition
expression you can refer to any of the indices in the index domain as if
the definition was the right-hand side of an assignment statement to the
parameter at hand (see also :ref:`sec:exec.assign`).

.. rubric:: Example

The following declaration illustrates an indexed ``Definition``
attribute.

.. code-block:: aimms

	Parameter MaxTransportFrom {
	    IndexDomain  : i;
	    Definition   : Max(j, Transport(i,j));
	}

.. rubric:: Care when used in loops

Whenever you provide a definition for an *indexed* parameter, you should
carefully verify whether and how that parameter is used in the context
of one of AIMMS' loop statements (see also :ref:`sec:exec.flow`). When,
due to changes in only a slice of the dependent data of a definition
during a previous iteration, AIMMS (in fact) only needs to evaluate a
single slice of a defined parameter during the actual iteration, you
should probably not be using a defined parameter. AIMMS' automatic
evaluation scheme for defined identifiers will always recompute the data
for such identifiers *for the whole domain of definition*, which can
lead to severe inefficiencies for high-dimensional defined parameters.
You can find a more detailed discussion on this issue in
:ref:`sec:eff.definition`.

.. rubric:: The :any:`Unit` attribute
   :name: attr:par.unit

.. _parameter.unit:

By associating a :any:`Unit` to every numerical identifier in your model,
you can let AIMMS help you check your model's consistency. AIMMS also
uses the :any:`Unit` attribute when presenting data and results in both the
output files of a model and the graphical user interface. You can find
more information on the use of units in :ref:`chap:units`.

.. rubric:: The ``Property`` attribute
   :name: attr:par.property

.. _parameter.property:

The ``Property`` attribute can hold various properties of the identifier
at hand. The allowed properties for a parameter are ``NoSave`` or one of
the numerical storage properties ``Integer``, ``Integer32``,
``Integer16``, ``Integer8`` or ``Double``, in addition to the properties
``Stochastic``, ``Uncertain``, ``Random`` which are discussed in
:ref:`sec:par.uncertainty`.

-  The property ``NoSave`` indicates whether the identifier values are
   stored in cases. It is discussed in detail in
   :ref:`attr:set.property`.

-  By default, the values of numeric parameters are stored as double
   precision floating point numbers. By specifying one of the storage
   properties ``Integer``, ``Integer32``, ``Integer16``, ``Integer8``,
   or ``Double`` AIMMS will store the values of the identifier as
   (signed) integers of default machine length, 4 bytes, 2 bytes or 1
   byte, or as a double precision floating point number respectively.
   These properties are only applicable to parameters with an integer
   range.

.. rubric:: The ``Property`` statement

During execution you can change the properties of a parameter through
the ``Property`` statement. The syntax of the ``Property`` statement and
examples of its use can be found in :ref:`sec:exec.property`.

.. rubric:: The ``Text`` attribute
   :name: attr:par.text

.. _parameter.text:

With the ``Text`` attribute you can provide one line of descriptive text
for the end-user. If the ``Text`` string of an indexed parameter or
variable contains a reference to one or more indices in the index
domain, then the corresponding elements are substituted for these
indices in any display of the identifier text.

.. _sec:par.uncertainty:

Properties and Attributes for Uncertain Data
--------------------------------------------

.. rubric:: Stochastic programming and robust optimization

The AIMMS modeling language allows you to specify both stochastic
programs and robust optimization models. Both methodologies are designed
to deal with models involving data uncertainty. In stochastic
programming the uncertainty is expressed by specifying multiple
scenarios, each of which can define scenario-specific values for certain
parameters in your model. Stochastic programming is discussed in full
detail in :ref:`chap:stoch`. For robust optimization, parameters can be
declared to not have a single fixed value, but to take their values from
an user-defined uncertainty set. Robust optimization is discussed in
:ref:`chap:robust`.

.. rubric:: Properties

The following ``Parameter`` properties are available in support of
stochastic programming and robust optimization models.

-  The property ``Stochastic`` indicates that the identifier can hold
   stochastic event data for a stochastic model. It is discussed in
   detail in :ref:`sec:stoch.stoch`.

-  The property ``Uncertain`` indicates that the identifier can hold
   uncertain values from an uncertainty set specified through the
   ``Uncertainty`` and/or ``Region`` attributes. Uncertain parameters
   are used in AIMMS' robust optimization facilities, and are discussed
   in detail in :ref:`sec:robust.uncertain`.

-  The property ``Random`` indicates that the identifier can hold random
   values with respect to a distribution with characteristics specified
   through the ``Distribution`` attribute. Random parameters are used in
   AIMMS' robust optimization facilities, and are discussed in detail in
   :ref:`sec:robust.chance`.

.. _attr:par.region:

.. _parameter.uncertainty:

.. _parameter.region:

.. rubric:: The ``Uncertainty`` and ``Region`` attributes
   :name: attr:par.uncertainty

The ``Uncertainty`` and ``Region`` attributes are available if the
parameter at hand has been declared uncertain using the ``Uncertain``
property. Uncertain parameters are used by AIMMS' robust optimization
framework, and are discussed in full detail in
:ref:`sec:robust.uncertain`. With the ``Region`` attribute you can
specify an uncertainty set using one of the predefined uncertainty sets
``Box``, ``ConvexHull`` or ``Ellipsoid``. The ``Uncertainty`` attribute
specifies a relationship between the uncertain parameter at hand, and
one or more other (uncertain) parameters in your model. The
``Uncertainty`` and ``Region`` attributes are not exclusive, i.e., you
are allowed to specify both, in which case AIMMS' generation process of
the robust counterpart will make sure that both conditions are satisfied
by the final solution.

.. rubric:: The ``Distribution`` attribute
   :name: attr:par.distribution

.. _parameter.distribution:

The ``Distribution`` attribute is available if the parameter at hand has
been declared random using the ``Random`` property. Random parameters
are used by AIMMS' robust optimization framework, and are discussed in
full detail in :ref:`sec:robust.chance`. With the ``Distribution``
attribute you can declare that the values for the random parameter at
hand adhere to one of the predefined distributions discussed in
:ref:`sec:robust.chance`.