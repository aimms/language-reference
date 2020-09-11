.. _sec:set.intro:

Sets and Indices
================

.. rubric:: General

Sets and indices give your AIMMS model dimension and depth by providing
a mechanism for grouping parameters, variables, and constraints. Sets
and indices are also used as driving mechanism in arithmetic operations
such as summation. The use of sets for indexing expressions helps to
describe large models in a concise and understandable way.

.. rubric:: Example

Consider a set of *Cities* and an identifier called *Transport* defined
between several pairs of cities :math:`(i,j)`, representing the amount
of product transported from supply city :math:`i` to destination city
:math:`j`. Suppose that you are interested in the quantities arriving in
each city. Rather than adding many individual terms, the following
mathematical notation, using sets and indices, concisely describes the
desired computation of these quantities.

.. math:: (\forall j \in Cities) \qquad Arrival_j = \sum_{i \in Cities} Transport_{ij}.

This multidimensional index notation forms the foundation of the AIMMS
modeling language, and can be used in all expressions. In this example,
*i* and *j* are indices that refer to individual *Cities*.

.. rubric:: Several types of sets

A set in AIMMS

-  has either *strings* or *integers* as elements,

-  is either a *simple* set, or a *relation*, and

-  is either *indexed* or *not indexed*.

.. rubric:: String versus integer

Sets can either have strings as elements (such as the set *Cities*
discussed above), or have integers as elements. An example of an integer
set could be a set of *Trials* represented by the numbers
:math:`1,\dots,n`. The resulting integer set can then be used to refer
to the results of each single experiment.

.. rubric:: Simple versus relation

A *simple* set is a one-dimensional set, such as the set *Cities*
mentioned above, while a *relation* or multidimensional set is the
Cartesian product of a number of simple sets or a subset thereof. An
example of a relation is the set of possible *Routes* between supply and
destination cities, which can be represented as a subset of the
Cartesian product *Cities* :math:`\times` *Cities*.

.. rubric:: Indexing as basic mechanism

Sets in AIMMS are the basis for creating multidimensional identifiers in
your model. Through indices into sets you have access to individual
values of these identifiers for each tuple of elements. In addition, the
indexing notation in AIMMS is your basic mechanism for expressing
iterative operations such as repeated addition, repeated multiplication,
sequential search for a maximum or minimum, etc.

.. rubric:: Indexed sets

Simple sets may be indexed. An indexed set is a family of sets defined
for every element in the index domain of the indexed set. An example of
an indexed set is the set of transport destination cities defined for
each supply city. On the other hand, the set *Cities* discussed above is
not an indexed set.

.. rubric:: Sorting of sets

The contents of any simple can be sorted in AIMMS. Sorting can take
place either automatically or manually. Automatic sorting is based on
the value of some expression defined for all elements of the set. By
using an index into a sorted subset, you can access any subselection of
data in the specified order. Such a subselection may be of interest in
your end-user interface or at a certain stage in your model.