.. _sec:set.decl:

``Set`` Declaration and Attributes
==================================

.. _set:

.. rubric:: Set attributes

Each set has an optional list of attributes which further specify its
intended behavior in the model. The attributes of sets are given in
:numref:`table:set.attr-set`. The attributes ``IndexDomain`` is only
relevant to indexed sets.

.. _table:set.attr-set:

.. table:: 

	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| Attribute       | Value-type                                                  | See also                                                  |
	+=================+=============================================================+===========================================================+
	| ``IndexDomain`` | *index-domain*                                              | :ref:`The IndexDomain attribute <attr:set.index-domain>`  |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``SubsetOf``    | *subset-domain*                                             |                                                           |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``Index``       | *identifier-list*                                           |                                                           |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``Parameter``   | *identifier-list*                                           |                                                           |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``Text``        | *string*                                                    | :ref:`The Text and Comment attributes <attr:prelim.text>` |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``Comment``     | *comment string*                                            | :ref:`The Text and Comment attributes <attr:prelim.text>` |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``Property``    | ``NoSave``, ``ElementsAreNumerical``, ``ElementsAreLabels`` |                                                           |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``Definition``  | *set-expression*                                            |                                                           |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	| ``OrderBy``     | *expression-list*                                           |                                                           |
	+-----------------+-------------------------------------------------------------+-----------------------------------------------------------+
	
.. _sec:set.simple:

Simple Sets
-----------

.. rubric:: Definition

A *simple* set in AIMMS is a finite collection of elements. These
elements are either strings or integers. Strings are typically used to
identify real-world objects such as products, locations, persons, etc.
Integers are typically used for algorithmic purposes. With every simple
set you can associate indices through which you can refer (in
succession) to all individual elements of that set in indexed statements
and expressions.

.. rubric:: Most basic example

An example of the most basic declaration for the set *Cities* from the
previous example follows.

.. code-block:: aimms

	Set Cities {
	    Index      : i,j;
	}

This declares the identifier ``Cities`` as a simple set, and binds the
identifiers ``i`` and ``j`` as indices to ``Cities`` throughout your
model text.

.. rubric:: More detailed example

Consider a set *SupplyCities* which is declared as follows:

.. code-block:: aimms

	Set SupplyCities {
	    SubsetOf   : Cities;
	    Parameter  : LargestSupplyCity;
	    Text       : The subset of cities that act as supply city;
	    Definition : {
	        { i | Exists( j | Transport(i,j) ) }
	    }
	    OrderBy    : i;
	}

The ``|`` operator used in the definition is to be read as "such that"
(it is explained in :ref:`chap:set-expr`). Thus, ``SupplyCities`` is
defined as the set of all cities from which there is transport to at
least one other city. All elements in the set are ordered
lexicographically. The set has no index of its own, but does have an
element parameter ``LargestSupplyCity`` that can hold any particular
element with a specific property. For instance, the following assignment
forms one way to specify the value of this element parameter:

.. code-block:: aimms

	LargestSupplyCity := ArgMax( i in SupplyCities, sum( j, Transport(i,j) ) );

Note that this assignment selects that particular element from the
subset of ``SupplyCities`` for which the total amount of ``Transport``
leaving that element is the largest.

.. rubric:: The ``SubsetOf`` attribute
   :name: attr:set.subset-of

.. _set.subset_of:

With the ``SubsetOf`` attribute you can tell AIMMS that the set at hand
is a subset of another set, called the *subset domain*. For simple sets,
such a subset domain is denoted by a single set identifier. During the
execution of the model AIMMS will assert that this subset relationship
is satisfied at all times.

.. rubric:: Root sets

Each simple set that is not a subset of another set is called a *root
set*. As will be explained later on, root sets have a special role in
AIMMS with respect to data storage and ordering.

.. rubric:: The ``Index`` attribute
   :name: attr:set.index

.. _set.index:

An index takes the value of *all* elements of a set successively and in
the order specified by its declaration. It is used in operations like
summation and indexed assignment over the elements of a set. With the
``Index`` attribute you can associate identifiers as indices into the
set at hand. The index attributes of all sets must be unique
identifiers, i.e. every index can be declared only once.

.. rubric:: The ``Parameter`` attribute
   :name: attr:set.parameter

.. _set.parameter:

A parameter declared in the ``Parameter`` attribute of a set takes the
value of a *specific* element of that set. Throughout the sequel we will
refer to such a parameter as an *element parameter*. It is a very useful
device for referring to set elements that have a special meaning in your
model (as illustrated in the previous example). In a later chapter you
will see that an element parameter can also be defined separately as a
parameter which has a set as its range.

.. _set.text:

.. _set.comment:

.. _attr:set.comment:

.. rubric:: The ``Text`` and ``Comment`` attributes
   :name: attr:set.text

With the ``Text`` attribute you can specify one line of descriptive text
for the end-user. This description can be made visible in the graphical
user interface when the data of an identifier is displayed in a page
object. You can use the ``Comment`` attribute to provide a longer
description of the identifier at hand. This description is intended for
the modeler and cannot be made visible to an end-user. The ``Comment``
attribute is a multi-line string attribute.

.. rubric:: Quoting identifier names in ``Comment``

You can make AIMMS aware that specific words in your comment text are
intended as identifier names by putting them in single quotes. This has
the advantage that AIMMS will update your comment when you change the
name of that identifier in the model editor, or, that AIMMS will warn
you when a quoted name does not refer to an existing identifier.

.. rubric:: The ``OrderBy`` attribute
   :name: attr:set.order-by

.. _set.order_by:

With the ``OrderBy`` attribute you can indicate that you want the
elements of a certain set to be ordered according to a single or
multiple ordering criteria. Only simple sets can be ordered.

.. rubric:: Ordering root sets

A special word of caution is in place with respect to specifying an
ordering principle for root sets. Root sets play a special role within
AIMMS because all data defined over a root set or any of its subsets is
stored in the original *data entry* order in which elements have been
added to that root set. Thus, the data entry order defines the natural
order of execution over a particular domain, and specifying the
``OrderBy`` attribute of a root set may influence overall execution
times of your model in a negative manner. :ref:`sec:eff.set.ordering`
discusses these efficiency aspects in more detail, and provides
alternative solutions.

.. rubric:: Ordering criteria

The value of the ``OrderBy`` attribute can be a comma-separated list of
one or more ordering criteria. The following ordering criteria (numeric,
string or user-defined) can be specified.

-  If the value of the ``OrderBy`` attribute is an indexed numerical
   expression defined over the elements of the set, AIMMS will order its
   elements in increasing order according to the numerical values of the
   expression.

-  If the value of the ``OrderBy`` attribute is either an index into the
   set, a set element-valued expression, or a string expression over the
   set, then its elements will be ordered lexicographically with respect
   to the strings associated with the expression. By preceding the
   expression with a minus sign, the elements will be ordered reverse
   lexicographically.

-  If the value of the ``OrderBy`` attribute is the keyword ``User``,
   the elements will be ordered according to the order in which they
   have been added to the subset, either by the user, the model, or by
   means of the ``Sort`` operator.

.. rubric:: Specifying multiple criteria

When applying a single ordering criterion, the resulting ordering may
not be unique. For instance, when you order according to the size of
transport taking place from a city, there may be multiple cities with
equal transport. You may want these cities to be ordered too. In this
case, you can enforce a more refined ordering principle by specifying
multiple criteria. AIMMS applies all criteria in succession, and will
order only those elements that could not be uniquely distinguished by
previous criteria.

.. rubric:: Example

The following set declarations give examples of various types of
automatic ordering. In the last declaration, the cities with equal
transport are placed in a lexicographical order.

.. code-block:: aimms

	Set LexicographicSupplyCities {
	    SubsetOf  : SupplyCities;
	    OrderBy   : i;
	}
	Set ReverseLexicographicSupplyCities {
	    SubsetOf  : SupplyCities;
	    OrderBy   : - i;
	}
	Set SupplyCitiesByIncreasingTransport {
	    SubsetOf  : SupplyCities;
	    OrderBy   : sum( j, Transport(i,j) );
	}
	Set SupplyCitiesByDecreasingTransportThenLexicographic {
	    SubsetOf  : SupplyCities;
	    OrderBy   : - sum( j, Transport(i,j) ), i;
	}

.. rubric:: The ``Property`` attribute
   :name: attr:set.property

.. _set.property:

.. _property:

In general, you can use the ``Property`` attribute to assign additional
properties to an identifier in your model. The applicable properties
depend on the identifier type. Sets, at the moment, only support a
single property.

-  The property ``NoSave`` specifies that the contents of the set at
   hand will never be stored in a case file. This can be useful, for
   instance, for intermediate sets that are necessary during the model's
   computation, but are never important to an end-user.

-  The properties ``ElementsAreNumerical`` and ``ElementsAreLabels`` are
   only relevant for integer sets (see also :ref:`sec:set.integer`).
   They will ignored for non-integer sets.

.. rubric:: Dynamic property selection

The properties selected in the ``Property`` attribute of an identifier
are ``on`` by default, while the nonselected properties are ``off`` by
default. During execution of your model you can also dynamically change
a property setting through the ``Property`` statement. The ``PROPERTY``
statement is discussed in :ref:`sec:exec.property`.

.. rubric:: The ``Definition`` attribute
   :name: attr:set.definition

.. _set.definition:

If an identifier can be uniquely defined throughout your model by a
single expression, you can (and should) use the ``Definition`` attribute
to specify this global relationship. AIMMS stores the result of a
``Definition`` and recomputes it only when necessary. For sets where a
global ``Definition`` is not possible, you can make assignments in
procedures and functions. The value of the ``Definition`` attribute must
be a valid expression of the appropriate type, as exemplified in the
declaration

.. code-block:: aimms

	Set SupplyCities {
	    SubsetOf   : Cities;
	    Definition : {
	        { i | Exists( j | Transport(i,j) ) }
	    }
	}

.. _sec:set.integer:

Integer Sets
------------

.. rubric:: Integer sets

A special type of simple set is an integer set. Such a set is
characterized by the fact that the value of the ``SubsetOf`` attribute
must be equal to the predefined set :any:`Integers` or a subset thereof.
Integer sets are most often used for algorithmic purposes.

.. rubric:: Usage in expressions

Elements of integer sets can also be used as integer values in numerical
expressions. In addition, the result of an integer-valued expression can
be added as an element to an integer set. Elements of non-integer sets
that represent numerical values cannot be used directly in numerical
expressions. To obtain the numerical value of such non-integer elements,
you can use the :any:`Val` function (see
:ref:`sec:set-expr.elem.functions`).

.. rubric:: Interpret values as integer or label?

The interpretation of integer set elements will as integer values in
numerical expressions, raises an ambiguity for certain types of
expressions. If ``anInteger`` is an element parameter into an integer
set ``anIntegerSet``,

-  how should AIMMS handle the expression

   .. code-block:: aimms
   
   	if (anInteger) then
   	    ...
   	endif;

   where ``anInteger`` holds the value ``'0'``. On the one hand, it is
   not the empty element, so if AIMMS would interpret this as a logical
   expression with a non-empty element parameter, the ``if`` statement
   would evaluate to true. If AIMMS would interpret this as a numerical
   expression, the element parameter would evaluate to the numerical
   value 0, and the ``if`` statement would evaluate to false.

-  how should AIMMS handle the assignment

   .. code-block:: aimms
   
   	anInteger := anInteger + 3;

   if the values in ``anIntegerSet`` are non-contiguous? If AIMMS would
   interpret ``anInteger`` as an ordinary element parameter, the ``+``
   operator would refer to a lead operator (see also
   :ref:`sec:set-expr.elem.lag-lead`), and the assignment would assign
   the third next element of ``anInteger`` in the set ``anIntegerSet``.
   If AIMMS would interpret ``anInteger`` as an numerical value, the
   assignment would assign the numerical value of ``anInteger`` plus 3,
   assuming that this is an element of ``anIntegerSet``.

You can resolve this ambiguity assigning one of the properties
``ElementsAreLabels`` and ``ElementsAreNumerical`` to ``anIntegerSet``.
If you don't assign either property, and you use one of these
expressions in your model, AIMMS will issue a warning about the
ambiguity, and the end result might be unpredictable.

.. rubric:: Construction

In order to fill an integer set AIMMS provides the special operator
``..`` to specify an entire range of integer elements. This powerful
feature is discussed in more detail in :ref:`sec:set-expr.set.enum`.

.. rubric:: Example

The following somewhat abstract example demonstrates some of the
features of integer sets. Consider the following declarations.

.. code-block:: aimms

	Parameter LowInt {
	    Range      : Integer;
	}
	Parameter HighInt {
	    Range      : Integer;
	}
	Set EvenNumbers {
	    SubsetOf    : Integers;
	    Index       : i;
	    Parameter   : LargestPolynomialValue;
	    OrderBy     : - i;
	}

The following statements illustrate some of the possibilities to compute
integer sets on the basis of integer expressions, or to use the elements
of an integer set in expressions.

.. code-block:: aimms

	! Fill the integer set with the even numbers between
	! LowInt and HighInt. The first term in the expression
	! ensures that the first integer is even.

	EvenNumbers := { (LowInt + mod(LowInt,2)) .. HighInt by 2 };

	! Next the square of each element i of EvenNumbers is added
	! to the set, if not already part of it (i.e. the union results)

	for ( i | i <= HighInt ) do
	    EvenNumbers += i^2;
	endfor;

	! Finally, compute that element of the set EvenNumbers, for
	! which the polynomial expression assumes the maximum value.

	LargestPolynomialValue := ArgMax( i, i^4 - 10*i^3 + 10*i^2 - 100*i );

.. rubric:: Ordering integer sets

By default, integer sets are ordered according to the numeric value of
their elements. Like with ordinary simple sets, you can override this
default ordering by using the ``OrderBy`` attribute. When you use an
index in specifying the order of an integer set, AIMMS will interpret it
as a numeric expression.

.. _sec:set.relation:

Relations
---------

.. rubric:: Relation

A *relation* or multidimensional set is the Cartesian product of a
number of simple sets or a subset thereof. Relations are typically used
as the domain space for multidimensional identifiers. Unlike simple
sets, the elements of a relation cannot be referenced using a single
index.

.. rubric:: Tuples and index components

An element of a relation is called a *tuple* and is denoted by the usual
mathematical notation, i.e. as a parenthesized list of comma-separated
elements. Throughout, the word *index component* will be used to denote
the index of a particular position inside a tuple.

.. rubric:: Index tuple

To reference an element in a relation, you can use an *index tuple*, in
which each tuple component contains an index corresponding to a simple
set.

.. rubric:: The ``SubsetOf`` attribute

The ``SubsetOf`` attribute is mandatory for relations, and must contain
the *subset domain* of the set. This subset domain is denoted either as
a parenthesized comma-separated list of simple set identifiers, or, if
it is a subset of another relation, just the name of that set.

.. rubric:: Example

The following example demonstrates some elementary declarations of a
relation, given the two-dimensional parameters ``Distance(i,j)`` and
``TransportCost(i,j)``. The following set declaration defines a
relation.

.. code-block:: aimms

	Set HighCostConnections {
	    SubsetOf   : (Cities, Cities);
	    Definition : {
	        { (i,j) | Distance(i,j) > 0 and TransportCost(i,j) > 100 }
	    }
	}

.. _sec:set.indexed:

Indexed Sets
------------

.. rubric:: Definition

An *indexed set* represents a family of sets defined for all elements in
another set, called the *index domain*. The elements of all members of
the family must be from a single (sub)set. Although membership tables
allow you to reach the same effect, indexed sets often make it possible
to express certain operations very concisely and intuitively.

.. rubric:: The ``IndexDomain`` attribute
   :name: attr:set.index-domain

.. _set.index_domain:

A set becomes an indexed set by specifying a value for the
``IndexDomain`` attribute. The value of this attribute must be a single
index or a tuple of indices, optionally followed by a logical condition.
The precise syntax of the ``IndexDomain`` attribute is discussed on
:ref:`attr:par.index-domain`.

.. rubric:: Example

The following declarations illustrate some indexed sets with a content
that varies for all elements in their respective index domains.

.. code-block:: aimms

	Set SupplyCitiesToDestination {
	    IndexDomain  : j;
	    SubsetOf     : Cities;
	    Definition   : {
	        { i | Transport(i,j) }
	    }
	}
	Set DestinationCitiesFromSupply {
	    IndexDomain  : i;
	    SubsetOf     : Cities;
	    Definition   : {
	        { j | Transport(i,j) }
	    }
	}
	Set IntermediateTransportCities {
	    IndexDomain  : (i,j);
	    SubsetOf     : Cities;
	    Definition   : DestinationCitiesFromSupply(i) * SupplyCitiesToDestination(j);
	    Comment      : {
	        All intermediate cities via which an indirect transport
	        from city i to city j with one intermediate city takes place
	    }
	}

The first two declarations both define a one-dimensional family of
subsets of ``Cities``, while the third declaration defines a
two-dimensional family of subsets of ``Cities``. Note that the ``*``
operator is applied to sets, and therefore denotes intersection.

.. rubric:: Subset domains

The subset domain of an indexed set family can be either a simple set
identifier, or another family of indexed simple sets of the same or
lower dimension. The subset domain of an indexed set *cannot* be a
relation.

.. rubric:: No default indices

Declarations of indexed sets do not allow you to specify either the
``Index`` or ``Parameter`` attribute. Consequently, if you want to use
an indexed set for indexing, you must locally bind an index to it. For
more details on the use of indices and index binding refer to
:ref:`sec:set.index` and :ref:`sec:bind.rules`.