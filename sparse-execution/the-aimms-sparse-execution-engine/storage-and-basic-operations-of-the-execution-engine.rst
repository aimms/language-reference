.. _sec:sparse.basic:

Storage and Basic Operations of the Execution Engine
====================================================

In this section we present, in a step-by-step manner, the operations
that, when combined, build up the AIMMS sparse execution engine. The
data storage method with which these operations work is called an
*ordered view*.

.. rubric:: Ordered view

The AIMMS execution engine stores the data according to the concept of
an ordered view. An ordered view is an ordered, sparse collection of the
non-default elements of an identifier. The order is the lexicographical
order of the indices of that identifier. Because of this order:

-  the non-default elements of the identifier can be visited in a
   lexicographic order one at a time, and

-  a particular tuple can be found efficiently using values for the
   indices.

.. rubric:: Running example

The running example, used in this section and presented below, contains
the two parameters ``A(i,j)`` and ``B(i,j)``, where ``i`` and ``j`` are
indices in a set ``S`` containing the elements ``{a1..a5}``. The default
values of these parameters are 0.0, and they contain the following data:

.. code-block:: aimms

	A(i,j) := data table          B(i,j) := data table
	     a1 a2 a3 a4 a5                a1 a2 a3 a4 a5
	  !  -- -- -- -- --             !  -- -- -- -- --
	  a1     2        5             a1     3        2
	  a2  2     3  2                a2
	  a3                            a3  5     1  2
	  a4  4                         a4  4
	  a5                  ;         a5                  ;

The ordered views of ``A`` and ``B`` are presented in the composite
tables below:

.. code-block:: aimms

	Composite table:              Composite table:
	     i  j A                        i  j B
	  ! -- -- -                     ! -- -- -
	    a1 a2 2                       a1 a2 3
	    a1 a5 5                       a1 a5 2
	    a2 a1 2                       a3 a1 5
	    a2 a3 3                       a3 a3 1
	    a2 a4 2                       a3 a4 2
	    a4 a1 4 ;                     a4 a1 4 ;

.. rubric:: Like an index in relational databases

There is nothing really new here; an ordered view corresponds to an
relational table in database terminology, with a (database) index on the
primary keys ``i`` and ``j``. A characteristic of both representations
is that they can be easily searched given explicit values for ``i`` and
``j``.

.. rubric:: Basic operations

In the following sections, we will classify the algebraic operations in
AIMMS according to their behavior in the AIMMS sparse execution engine,
and discuss the effects of combining multiple operations or changing the
natural index order.

.. _subsec:sparse.basic.plus:

The ``+`` Operator: Union Behavior
----------------------------------

.. rubric:: First statement

The first statement in the running example is the simple addition of the
matching elements resulting in parameter ``C(i,j)``:

.. code-block:: aimms

	C(i,j) := A(i,j) + B(i,j);

.. rubric:: Merging rows

As illustrated in :numref:`fig:sparse.union`, this statement can be
executed in a sparse manner by merging the ordered views of ``A`` and
``B`` and adding the values as one progresses.

.. figure:: storage-and-basic-operations-of-the-execution-engine-pspic1.svg
   :name: fig:sparse.union
   :height: 161 px
   :width: 217 px
   :scale: 150 %

.. rubric:: Union behavior

In this figure, each arrow represents a computed result. The behavior of
the ``+`` operator is referred to as *sparse union* behavior: the union
of rows from ``A`` and ``B`` is taken to form the rows of ``C`` and it
is sparse because we do not need to consider those tuples ``(i,j)`` for
which ``A(i,j)`` and ``B(i,j)`` are both 0.0.

.. rubric:: Similar operators

Other operators, such as ``OR``, ``XOR``, ``<``, ``>`` and ``<>`` have a
similar behavior. They can also be implemented using the union of rows
and performing the appropriate operation.

.. _subsec:sparse.basic.mult:

The ``*`` Operator: Intersection Behavior
-----------------------------------------

.. rubric:: Second statement

The second statement in the running example is the simple multiplication
of the matching elements resulting in parameter ``D(i,j)``:

.. code-block:: aimms

	D(i,j) := A(i,j) * B(i,j);

.. rubric:: Matching rows

This statement can be executed in a sparse manner by intersecting the
ordered views of ``A`` and ``B`` and multiplying the corresponding
values. Intersection is sufficient because only for those tuples
``(i,j)`` for which both ``A(i,j)`` and ``B(i,j)`` are non-zero, will a
non-zero be computed. This is illustrated in the
:numref:`fig:sparse.intersection`

.. figure:: storage-and-basic-operations-of-the-execution-engine-pspic2.svg
   :name: fig:sparse.intersection
   :height: 161 px
   :width: 380 px
   :scale: 150 %

.. rubric:: Intersection behavior

Note that the ordered views of both ``A`` and ``B`` are searchable and,
thus, finding the matching elements can be efficiently implemented. We
call this behavior *sparse intersection* behavior. Because only matching
rows need to be considered, sparse intersection operators are much more
efficient than sparse union operators.

.. rubric:: Similar operators

Other operators, such as the ``AND`` and ``$`` operators, exhibit
similar behavior. They can also be implemented using the intersection of
the rows and performing the appropriate operation.

.. _subsec:sparse.basic.equal:

The ``=`` Operator: Dense Behavior
----------------------------------

.. rubric:: Third statement

The third statement in the running example checks whether corresponding
values are equal.

.. code-block:: aimms

	E(i,j) := (A(i,j) = B(i,j));

.. rubric:: Comparing values

This statement is admittedly somewhat artificial. However, such
conditions are frequently part of larger expressions and must be
considered. The key observation is that the comparison ``0.0 = 0.0``
evaluates to true. In AIMMS the value 'true' is represented by the
numerical value 1.0. Therefore, the result of ``E(i,j)`` is:

.. code-block:: aimms

	E(i,j) := data table
	     a1 a2 a3 a4 a5
	  !  -- -- -- -- --
	  a1  1     1  1
	  a2     1        1
	  a3     1        1
	  a4  1  1  1  1  1
	  a5  1  1  1  1  1   ;

.. rubric:: Dense behavior

Given that the comparison of two zeros also results in a non-zero, all
possible combinations of ``(i,j)`` have to be considered. Therefore,
this operation exhibits *dense* behavior, i.e. the operation cannot be
performed in a sparse manner. Dense operators have the worst possible
efficiency.

.. rubric:: Similar operators

Other operators, such as ``/``, ``**``, ``<=`` and ``=>`` demonstrate
similar behavior. They also need to be implemented by considering all
the possibilities and evaluating as one progresses.

.. rubric:: Beware!

Increasing the number of indices, or increasing the size of the sets
will make the number of rows to be considered in such operations grow
rapidly. Large-dimensional dense operations are a potential cause of
performance glitches in an application.

.. _subsec:sparse.basic.combining:

Behavior of Combined Operations
-------------------------------

.. rubric:: Fourth statement

The fourth statement is a variation of the third statement:

.. code-block:: aimms

	EP(i,j) := ( A(i,j) = B(i,j) ) $ A(i,j);

.. rubric:: Speeding up

Although the operation ``=`` remains dense, the entire right hand side
of the assignment statement is limited to only those tuples ``(i,j)``
for which ``A(i,j)`` is non-zero. This is known as a domain condition on
the expression. The net effect on the expression is that this condition
speeds up efficient behavior by moving from dense to sparse behavior.
The result of this fourth assignment is:

.. code-block:: aimms

	EP(i,j) := data table
	     a1 a2 a3 a4 a5
	  !  -- -- -- -- --
	  a1
	  a2
	  a3
	  a4  1
	  a5                  ;

.. rubric:: Preventing dense behavior

If your model contains a statement that performs badly due to a dense
operation, using a domain condition can remedy the problem. Often, it is
possible to formulate a domain condition that does not alter the result
of the computation, but which does allow AIMMS to execute the statement
in a sparse manner.

.. _subsec:sparse.basic.summation:

Summation
---------

.. rubric:: Fifth statement

The fifth statement, as detailed below, is a step towards the sixth
statement and illustrates a language construct where sparse evaluation
is straightforward. This fifth statement is a simple aggregation of the
parameter ``A(i,j)`` in a parameter ``AI(i)``:

.. code-block:: aimms

	AI(i) := Sum( j, A(i,j) );

This operation is illustrated in :numref:`fig:sparse.aggr-i`.

.. figure:: storage-and-basic-operations-of-the-execution-engine-pspic3.svg
   :name: fig:sparse.aggr-i
   :height: 117 px
   :width: 76 px
   :scale: 150 %

.. rubric:: Running indices and identifier indices match

Each pairing represents a group of values corresponding to a particular
value of ``i``. As the elements in a group are adjacent in this ordered
view, the result of ``AI`` can be computed in a single pass over the
ordered view of ``A``. The order of the running indices in the statement
is ``[i,j]``. The first running index ``i`` is already part of the left
hand side of the assignment, and ``j`` is added to this list as part of
the sum.

.. rubric:: Single pass is sufficient

Because the order of the running indices matches the order of the
indices in the identifier ``A(i,j)``, the results of the sum can be
computed in a single pass over the ordered view of ``A(i,j)``.

.. _subsec:sparse.basic.reordered-views:

Reordered Views
---------------

.. rubric:: Sixth statement

The sixth statement is a small variation to the fifth statement above.
This sixth statement is an aggregation of the parameter ``A`` in a
parameter ``AJ(j)``:

.. code-block:: aimms

	AJ(j) := Sum( i, A(i,j) );

.. rubric:: Non-matching index order

This time, the elements that belong to the same group ``j`` are not
adjacent in the ordered view of ``A`` as the order of the indices in
this statement is ``[j,i]`` which does not match the order of the
indices in ``A(i,j)``.

.. rubric:: Reordered views

In order to regain adjacency of the elements in the same group, AIMMS
maintains other views of the parameter ``A`` known as *reordered views*.
A reordered view of an ordered view is a lexicographic order of the
elements such that the order of the indices in the identifier matches
the order of the running indices. A reordered view, and the grouping
according to this view, are illustrated in :numref:`fig:sparse.aggr-j`.

.. figure:: storage-and-basic-operations-of-the-execution-engine-pspic4.svg
   :name: fig:sparse.aggr-j
   :height: 117 px
   :width: 85 px
   :scale: 150 %

.. rubric:: Single pass is sufficient

Again, each pairing represents a group of values corresponding to a
particular value of ``j``. As the elements in a group are adjacent in
this reordered view, the results of ``AJ`` can be computed by a single
pass over this reordered view of ``A``. AIMMS generates and maintains
reordered views on an as needs basis. They do, however, take up memory.