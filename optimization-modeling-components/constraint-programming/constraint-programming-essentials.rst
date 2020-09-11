.. _sec:constraint.programming.essentials:

Constraint Programming Essentials
=================================

.. rubric:: Variables

In constraint programming, models are built using variables and
constraints, and as such is similar to integer programming. One
fundamental difference is that, in integer programming, the range of a
variable is specified and maintained as an interval, while in constraint
programming, the variable range is maintained explicitly as a set of
elements. Note that in the constraint programming literature, the range
of a variable is commonly referred to as its *domain*.

.. rubric:: Constraints

As a consequence of this explicit range representation, constraint
programming can offer a wide variety of constraint types. Most
constraint programming solvers allow constraints to be defined by
arbitrary expressions that combine algebraic or logical operators.
Moreover, meta-constraints can be formulated by interpreting the logical
value of an expression as a boolean value in a logical relation, or as a
binary value in an algebraic relation. For example, to express that
every two distinct tasks :math:`i` and :math:`j`, from a set of tasks
:math:`T` with respective starting times :math:`s_i,s_j` and durations
:math:`d_i, d_j`, should not overlap in time, we can use logical
disjunctions:

.. math::
   :label: eq:logical.disjunctions

   (s_i + d_i \leq s_j) \vee (s_j + d_j \leq s_i), \; \forall i,j \in T, i \neq j.

As another example, we can set a restriction such that no more than half
the variables from :math:`x_1, \dots, x_n` are assigned to a specific
value :math:`v` as :math:`\sum_{i=1}^n (x_i = v) \leq 0.5n`.

.. rubric:: Global constraints

In addition, constraint programming offers special symbolic constraints
that are called *global constraints*. These constraints can be defined
over an arbitrary set of variables, and encapsulate a combinatorial
structure that is exploited during the solving process. The constraint
:any:`cp::AllDifferent`\ :math:`(x_1  \dots, x_n)` is an example of such a
global constraint. This global constraint requires the variables
:math:`x_1  \dots, x_n` to take distinct values.

.. rubric:: Solving

The solving process underpinning constraint programming combines
systematic search with inference techniques. The systematic search
implicitly enumerates all possible variable-value combinations, thus
defining a search tree in which the root represents the original problem
to be solved. At each node in the search tree, an inference is made by
means of *domain filtering* and *constraint propagation*. Each
constraint in the model has an associated domain filtering algorithm
that removes provably inconsistent values from the variable domains.
Here, a domain value is inconsistent if it does not belong to any
solution of the constraint. The updated domains are then communicated to
the other constraints, whose domain filtering algorithms in turn become
active; this is the constraint propagation process. In practice, the
most effective filtering algorithms are those associated with global
constraints. Therefore, most practical applications that are to be
solved with constraint programming are formulated using global
constraints.

.. rubric:: Application domains

Constraint programming can be particularly effective with highly
combinatorial problem domains, such as timetabling or
resource-constrained scheduling. For such problems an integer
programming model may be non-intuitive to express. Moreover, the
associated continuous relaxation may be quite weak, which makes it much
harder to find a provably optimal solution. For example, again consider
two tasks :math:`A` and :math:`B` that must not overlap in time. In
integer programming one can introduce two binary variables,
:math:`y_{AB}` and :math:`y_{BA}`, representing that task :math:`A` must
be processed either before or after, task :math:`B`. The non-overlapping
constraint can then be expressed as :math:`y_{AB} + y_{BA} = 1`, for
which a continuous linear relaxation may assign a solution
:math:`y_{AB} = 
y_{BA} = 0.5`, which is not very informative. In contrast, the
non-overlapping requirement can be handled very effectively using a
specific 'sequential resource' scheduling constraint in constraint
programming that effectively groups together all pairwise logical
disjunctions in :eq:`eq:logical.disjunctions` above. Such a constraint
is also referred to as a disjunctive or unary constraint in the
constraint programming literature.

.. rubric:: Designing models

The expressiveness of constraint programming offers a powerful modeling
environment, albeit one that comes with a caveat. Namely, that different
syntactically equivalent formulations may yield quite different solving
times. For example, an alternative to the constraint
:any:`cp::AllDifferent`\ :math:`(x_1, x_2, \dots, x_n)` is its
decomposition into pairwise not-equal constraints :math:`x_i \neq x_j`
for :math:`1
\leq i < j \leq n`. The domain filtering algorithm for
:any:`cp::AllDifferent` provably removes more inconsistent domain values
than the individual not-equal constraints, which results in much smaller
search trees and faster solution times. Therefore, when designing a
constraint programming model, one should be aware of the effect that
different formulations can have on the solving time. In most situations,
it is advisable to apply global constraints to exploit their algorithmic
power.

Variables in Constraint Programming
-----------------------------------

.. rubric:: Variables of a constraint program

A constraint programming problem is made up of discrete variables and
constraints over these discrete variables. A discrete variable is a
variable that takes on a discrete value.

AIMMS supports two base types of discrete variables for constraint
programming. The first type of variable is the integer variable; an
ordinary variable with a range formulated such as ``{a..b}`` where ``a``
and ``b`` are numbers or references to parameters (see :ref:`chap:var`).
Such variables can also be used in ``MIP`` problems. The second type of
variable is the element variable, which will be further detailed in this
section. This type of variable can only be used in a constraint
programming problem. These two types of variable can be combined in a
third type, called an integer element variable, which supports the
operations that are defined for both the integer variable and the
element variable.

ElementVariable Declaration and Attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _element_variable:

An element variable is a variable that takes an element as its value. It
can have the attributes specified in
:numref:`table:cp.attr-element-variable`. The attributes
``IndexDomain``, ``Priority``, ``NonvarStatus``, ``Text``, ``Comment``
are the same as those for the variables introduced in :ref:`chap:var`.

.. _table:cp.attr-element-variable:

.. table:: 

	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| Attribute        | Value-type            | See also                                                                                                            |
	+==================+=======================+=====================================================================================================================+
	| ``IndexDomain``  | *index-domain*        | :ref:`attr:var.index-domain`                                                                                        |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Range``        | *named set*           |                                                                                                                     |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Default``      | *constant-expression* | :ref:`The Parameter Default attribute <attr:par.default>`, :ref:`The Variable Default attribute <attr:var.default>` |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Priority``     | *expression*          | :ref:`The Variable Priority attribute <attr:var.priority>`                                                          |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``NonvarStatus`` | *expression*          | :ref:`The Variable NonVar attribute <attr:var.nonvar>`                                                              |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Property``     | ``NoSave``            | :ref:`The Set Property attribute <attr:set.property>`                                                               |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Text``         | *string*              | :ref:`The Text and Comment attribute <attr:prelim.text>`                                                            |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Comment``      | *comment string*      | :ref:`The Text and Comment attribute <attr:prelim.comment>`                                                         |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	| ``Definition``   | *expression*          | :ref:`The Variable Definition attribute <attr:var.definition>`                                                      |
	+------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
	
.. _element_variable.range:

.. rubric:: The ``Range`` attribute

The range of an element variable is a one-dimensional set, similar to
the range of an element parameter. This attribute must be a set
identifier; and this permits the compiler to verify the semantics when
element variables are used in expressions. This attribute is mandatory.

.. _element_variable.default:

.. rubric:: The ``Default`` attribute

The attribute ``default`` of an element variable is a quoted element.
This attribute is not mandatory.

.. _element_variable.definition:

.. rubric:: The ``Definition`` attribute

The ``Definition`` attribute of an element variable is similar to the
definition attribute of a variable, see also
page :ref:`attr:var.definition`, except that its value is an element and
the resulting element must lie inside the range of the element variable.
This attribute is not mandatory.

.. _element_variable.property:

.. _EmptyElementAllowed:

.. rubric:: The ``Property`` attribute

The following properties are available to element variables:

**Nosave**
   When set, this property indicates that the element variable is not to
   be saved in cases.

**EmptyElementAllowed**
   ' When set, this property indicates that in a feasible solution, the
   value of this variable can, but need not, be the empty element ``"``.
   When the range of the element variable is a subset of the set
   :any:`Integers`, this property is not available. In the following
   example, for the element variable ``eV``, not selecting an element
   from ``S``, is a valid choice, but this choice forces the integer
   variable ``X`` to 0.

   .. code-block:: aimms
   
   	ElementVariable eV {
   	    Range       :  S;
   	    Property    :  EmptyElementAllowed;
   	}
   	Constraint Force_X_to_zero_when_no_choice_for_eV {
   	   Definition   :  if eV = '' then X = 0 endif;
   	}

This attribute is not mandatory.

.. rubric:: Element translation

Constraint programming solvers only use integer variables, and AIMMS
translates an element variable, say ``eV`` with range the set ``S``
containing :math:`n` elements into a integer variable, say ``v``, with
range :math:`\{ 0 .. n-1\}`. By design, this translation leaves no room
for the empty element ``"``, and subsequently, in a feasible solution,
the empty element is no part of it. In order to permit the explicit
consideration of the empty element as part of a solution, the property
``EmptyElementAllowed`` can be set for ``eV``. In that case the range of
``v`` is :math:`\{ 0 .. n\}` whereby the value 0 corresponds to the
empty element.

Selecting a Variable Type
~~~~~~~~~~~~~~~~~~~~~~~~~

.. rubric:: Choosing variable type

When there are multiple types of objects, such as integer variables and
element variables in AIMMS, the following two questions naturally arise:

#. How to choose between the various types?

#. Can these types be combined?

The answers to these questions are as follows:

#. You may want to base the choice of types of variables on the
   operations that can be performed meaningfully on these types. Which
   operation is appropriate for which variable type is described below.

#. An identifier can have both the 'integer variable' and 'element
   variable' types and is then called an 'integer element variable'.
   This is created as an element variable with a named subset of the
   predeclared set :any:`Integers` as its range.

.. _cp.variable.operation:

.. rubric:: Operations on variables

The operations on variables that are interesting in constraint
programming are:

-  **Numeric** operations, such as multiplication, addition, and taking
   the absolute value. These operations are applicable to integer
   variables and to integer element variables.

-  **Index** operations; selecting an element of an indexed parameter or
   variable. An element variable ``eV`` can be an argument of a
   parameter ``P`` or a variable ``X`` in expressions such as ``P(eV)``
   or ``X(eV)``. These operations are applicable to all element
   variables. In the Constraint Programming literature, such operations
   are often implemented using so-called element constraints.

-  **Compare, subtract, min and max** operations. These operations are
   applicable to all discrete variables, including element variables.
   For element variables, AIMMS uses the ordering of sets, see
   :ref:`sec:set.decl`.

All of the above operations are available with integer element
variables.

.. rubric:: Contiguous range

In order to limit an element variable to a contiguous subset of its
named range, element valued suffixes ``.lower`` and ``.upper`` can be
used. In the example below, the assignment to ``eV.Lower`` restricts the
variable ``eV`` to the contiguous set ``{c..e}``.

.. code-block:: aimms

	Set someLetters {
	    Definition   : data { a, b, c, d, e };
	}
	ElementVariable eV {
	    Range        : someLetters;
	}
	Procedure Restrict_eV {
	    Body         : eV.lower := 'c';
	}

The specification of non-contiguous ranges, informally known as ranges
with holes, is detailed in the next subsection.

.. _cp:ss:global:

Constraints in Constraint Programming
-------------------------------------

.. rubric:: Introduction

The constraints in constraint programming allow a rich variety of
restrictions to be placed on the variables in a constraint program,
ranging from direct domain restrictions on the variables to global
constraints that come with powerful propagation algorithms.

.. rubric:: Domain restrictions

A domain restriction restricts the domain of a single variable, or of
multiple variables, and is specified using the ``IN`` operator. For
example, we can restrict the domain of an element variable ``eV`` as
follows:

.. code-block:: aimms

	Constraint DomRestr1 {
	    Definition   :  eV in setA;
	}

When we apply the ``IN`` operator to multiple variables, we can define a
constraint by explicitly listing all tuples that are allowed. For
example:

.. code-block:: aimms

	Constraint DomRestr2 {
	    Definition   :  (eV1, eV2, eV3) in ThreeDimRelation;
	    Comment      : "ThreeDimRelation contains all allowed tuples";
	}

.. code-block:: aimms

	Constraint DomRestr3 {
	    Definition   :  not( (eV1, eV2, eV3) in ComplementRelation );
	    Comment      : "ComplementRelation contains all forbidden tuples";
	}

In constraint ``DomRestr2`` above, the three element variables are
restricted to elements from the set of allowed tuples defined by
``ThreeDimRelation``. Alternatively, we can define such a restriction
using the complement, i.e., a list of forbidden tuples, as with
constraint ``DomRestr3``. In constraint programming, these constraints
are also known as *Table* constraints; the data for these constraints
resemble tables in a relational database.

.. rubric:: Algebraic restrictions

The following operations are permitted on discrete variables, resulting
in expressions that can be used in constraint programming constraints:

#. The binary ``min(a,b)``, ``max(a,b)`` and the iterative
   ``min(i,x(i))``, ``max(i,x(i))`` can both be used,

#. multiplication ``*``, addition ``+``, subtraction ``-``, absolute
   value ``abs`` and square ``sqr``,

#. integer division ``div(a,b)``, integer modulo ``mod(a,b)``,

#. floating point division ``/``, and

#. indexing: an element variable is used as an argument of another
   parameter or variable, ``P(eV)``, ``V(eV)``,

Note that the operation must be meaningful for the variable type, see
:ref:`cp.variable.operation`.

These expressions can be compared, using the operators ``<=``, ``<``,
``=``, ``<>``, ``>``, and ``>=`` to create algebraic restrictions.
Simple examples of algebraic constraints, taken from Einstein's Logic
Puzzle, are presented below.

.. code-block:: aimms

	Constraint Clue15 {
	    Definition   :  abs( Smoke('Blends') - Drink('Water') ) = 1;
	    Comment      :  "The man who smokes Blends has a neighbor who drinks water.";
	}
	Constraint TheQuestion {
	    Definition   :  National(eV)=Pet('Fish');
	    Comment      :  "Who owns the pet fish? Result stored in element variable eV";
	}

.. rubric:: Combining restrictions

The constraints above can be combined to create other constraints called
meta-constraints. Meta-constraints can be formed by using the scalar
operators ``AND``, ``OR``, ``XOR``, ``NOT`` and ``IF-THEN-ELSE-ENDIF``.
For example:

.. code-block:: aimms

	Constraint OneTaskComesBeforeTheOther {
	    Definition   : {
	        ( StartA + DurA <= StartB ) or
	        ( StartB + DurB <= StartA )
	    }
	}

In addition, restrictions can be combined into meta-constraints using
the iterative operators ``FORALL`` and ``EXISTS``. Moreover,
restrictions can be counted using the iterative operator ``SUM`` and the
result compared with another value. Finally, meta-constraints are
restrictions themselves, they can be combined into even more complex
meta-constraints. The following example is a variable definition, in
which the collection of constraints ``(Finish(i) > Deadline(i))`` is
used to form a meta-constraint.

.. code-block:: aimms

	Variable TotalTardinessCost {
	    Definition  :  Sum( i, TardinessCost(i) | ( Finish(i) > Deadline(i) ) );
	}

In the following example, the binary variable ``y`` gets the value 1 if
each ``X(i)`` is greater than ``P(i)``.

.. code-block:: aimms

	Constraint Ydef {
	    Definition   :  y = FORALL( i, X(i) > P(i) );
	}

From the Steel Mill example, we can model that we do not want more than
two colors for each slab by the following nested usage of
meta-constraints:

.. code-block:: aimms

	Constraint EnhancedColorCst {
	    IndexDomain  :  (sl);
	    Definition   :  sum( c, EXISTS (o in ColorOrders(c), SlabOfOrder(o)=sl)) <= 2;
	}

.. rubric:: Global constraints

AIMMS supports the global constraints presented in
:numref:`table:constraint.programming.special.restrictions`. These
global constraints come with powerful filtering techniques that may
significantly reduce the search tree and thus the time needed to solve a
problem.

.. _table:constraint.programming.special.restrictions:

.. table:: Global constraints

   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Global constraint                                                                        | Meaning                                                                                                                                                                                     |
   +==========================================================================================+=============================================================================================================================================================================================+
   | :any:`cp::AllDifferent` (:math:`i`, :math:`x_i`)                                         | The :math:`x_i` must have distinct values. :math:`\forall i,j| i \neq j: x_i \neq x_j`                                                                                                      |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`cp::Count` (:math:`i`, :math:`x_i`, :math:`c`, :math:`\otimes`, :math:`y`)         | The number of :math:`x_i` related to :math:`c` is :math:`y`. :math:`\sum_i (x_i=c) \otimes y` where :math:`\otimes \in \{\leq, \geq, =, >, <, \neq\}`                                       |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`cp::Cardinality` (:math:`i`, :math:`x_i`, :math:`j`, :math:`c_j`, :math:`y_j`)     | The number of :math:`x_i` equal to :math:`c_j` is :math:`y_j`. :math:`\forall j: \sum_i (x_i=c_j) = y_j`                                                                                    |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`cp::Sequence` (:math:`i`, :math:`x_i`, :math:`S`, :math:`q`, :math:`l`, :math:`u`) | The number of :math:`x_i\in S` for each subsequence of length :math:`q` is between :math:`l` and :math:`u`. :math:`\forall i=1..n-q+1:` :math:`l \leq \sum_{j=i}^{i+q-1} (x_j\in S) \leq u` |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`cp::Channel` (:math:`i`, :math:`x_i`, :math:`j`, :math:`y_j`)                      | Channel variable :math:`x_i\to J` to :math:`y_j\to I` :math:`\forall i,j: x_i=j \Leftrightarrow y_j=i`                                                                                      |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`cp::Lexicographic` (:math:`i`, :math:`x_i`, :math:`y_i`)                           | :math:`x` is lexicographically before :math:`y` :math:`\exists i: \forall j<i: x_j=y_j \wedge x_i<y_i`                                                                                      |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`cp::BinPacking` (:math:`i`, :math:`l_i`, :math:`j`, :math:`a_j`, :math:`s_j`)      | Assign object :math:`j` of known size :math:`s_j` to bin :math:`a_j \to I`. Size of bin :math:`i \in I` is :math:`l_i`. :math:`\forall i: \sum_{j \mid a_j = i} s_j \leq l_i`               |
   +------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

The example below illustrates the use of the global constraint
:any:`cp::AllDifferent` as used in the Latin square completion problem. A
Latin square of order :math:`n` is an :math:`n\times n` matrix where the
values are in the range :math:`\{1..n\}` and distinct over each row and
column.

.. code-block:: aimms

	Constraint RowsAllDifferent {
	    IndexDomain  :  r;
	    Definition   :  cp::AllDifferent( c, Entry(r, c) );
	}
	Constraint ColsAllDifferent {
	    IndexDomain  :  c;
	    Definition   :  cp::AllDifferent( r, Entry(r, c) );
	}

Additional examples of global constraints are present in the AIMMS
`Function Reference <https://documentation.aimms.com/functionreference/>`__. Unless stated otherwise in the function reference,
global constraints can also be used outside of constraints definitions,
for example in assignments or parameter definitions.

.. rubric:: Global constraint vector arguments

These global constraints have vectors as arguments. The size of a vector
is defined by a preceding index binding argument. Further information on
index binding can be found in the Chapter on Index :ref:`chap:bind`.
Such a vector can be a vector of elements, for example the fourth
argument of :any:`cp::Cardinality`. In a vector of elements, the empty
element ``"`` is not allowed; comparison of an element variable against
the empty element is not supported.

.. rubric:: Basic scheduling constraints

AIMMS offers support for both basic scheduling and advanced scheduling.
Advanced scheduling will be detailed in the next section but, for basic
scheduling, AIMMS offers the following two global constraints:

.. _cp::ParallelSchedule-LR:

.. _cp::SequentialSchedule-LR:

#. The global constraint :any:`cp::SequentialSchedule`\ (:math:`j`,
   :math:`s_j`, :math:`d_j`, :math:`e_j`) ensures that two distinct jobs
   do not overlap where job :math:`j` has start time :math:`s_j`,
   duration :math:`d_j` and end time :math:`e_j`. This constraint is
   equivalent to:

   -  :math:`\forall i,j,i \neq j:(s_i+d_i\leq s_j) \vee (s_j + d_j \leq s_i)`.

   -  :math:`\forall j: s_j + d_j = e_j`

   This and similar constraints are also known as ``unary`` or
   ``disjunctive`` constraints within the Constraint Programming
   literature.

#. The global constraint :any:`cp::ParallelSchedule`\ (:math:`l`,
   :math:`u`, :math:`j`, :math:`s_j`, :math:`d_j`, :math:`e_j`,
   :math:`h_j`) allows a single resource to handle multiple jobs, within
   limits :math:`l` and :math:`u`, at the same time. Here job :math:`j`
   has start time :math:`s_j`, duration :math:`d_j`, end time
   :math:`e_j` and resource consumption (height) :math:`h_j`. This
   constraint is equivalent to:

   -  :math:`\forall t: l\leq\sum_{j|s_j\leq{}t<e_j} h_j\leq u`.

   -  :math:`\forall j: s_j + d_j = e_j`

   This and similar constraints are also known as ``cumulative``
   constraints within the Constraint Programming literature.