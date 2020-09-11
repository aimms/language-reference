.. _sec:data.allidentifiers:

Working with the Set :any:`AllIdentifiers`
==========================================

.. rubric:: Working with :any:`AllIdentifiers`

Throughout your model you can use the predefined set :any:`AllIdentifiers`
to construct and work with dynamic collections of identifiers in your
model. Several operators in AIMMS support the use of a subset of
:any:`AllIdentifiers` instead of an explicit list of identifier names,
while other operators support the use of an index into
:any:`AllIdentifiers` instead of a single explicit identifier name.

.. rubric:: Constructing identifier sets

AIMMS offers a number of constructs that can help you to construct a
meaningful subset of :any:`AllIdentifiers`. They are:

-  set algebra with other predefined identifier subsets, and

-  dynamic selection based on model query functions.

.. rubric:: Predefined identifier sets

When compiling your model, AIMMS automatically creates an identifier set
for every section in your model. Each such set contains all the
identifier names that are declared in the corresponding section. In
addition, for every identifier type, AIMMS fills a predeclared set
``All``\ *IdentifierType* (e.g. :any:`AllParameters`, :any:`AllSets`) with all
the identifiers of that type. The complete list of identifier type
related sets defined by AIMMS can be found in the AIMMS Function
Reference. You can use both type of sets to perform set algebra to
construct particular identifier subsets of interest to your model.

.. rubric:: Example

If your model contains a section ``Unit Model``, you can assign the
collection of all parameters in that section to a subset
``UnitModelParameters`` of :any:`AllIdentifiers` through the assignment

.. code-block:: aimms

	UnitModelParameters := Unit_Model * AllParameters;

.. rubric:: Model query functions

Another method to construct meaningful subsets of :any:`AllIdentifiers`
consists of using the functions provided to query aspects of those
identifiers. Selected examples are:

-  the function :any:`IdentifierDimension` returning the dimension of the
   identifier,

-  the function :any:`IdentifierType` returning the type of the identifier
   as an element of :any:`AllIdentifierTypes`,

-  the function :any:`IdentifierText` returning the contents of the
   ``TEXT`` attribute, and

-  the function :any:`IdentifierUnit` returning the contents of the
   ``UNIT`` attribute.

These functions take as argument an element in the set
:any:`AllIdentifiers`.

.. rubric:: Functions accepting identifier index

In addition to the functions lists above, the functions :any:`Card` and
:any:`ActiveCard` also accept an index into the set :any:`AllIdentifiers`.
They will then return the cardinality of the identifier represented by
the index, or the cardinality of the active elements of that identifier,
respectively. You can also use these functions to dynamically construct
a subset of :any:`AllIdentifiers`.

.. rubric:: Example

The set expression

.. code-block:: aimms

	{ IndexIdentifiers in UnitModelParameters | 
	        IdentifierDimension( IndexIdentifier ) = 3 }

refers to the collection of all 3-dimensional parameter in the section
``Unit Model``.

.. rubric:: Working with identifier sets

The following operators in AIMMS support identifier subsets to represent
a collection of individual identifiers:

-  the ``READ`` and ``WRITE`` operators,

-  the ``EMPTY``, ``CLEANUP``, ``CLEANDEPENDENTS``, and ``REBUILD``
   operators.

If you are interested in the contents of an identifier subset, you can
use the ``DISPLAY`` operator, which will just print the identifier names
contained in the set, rather than the contents of the identifiers
referred to in the identifier set as is the case for the ``WRITE``
statement.

.. rubric:: Functions accepting identifier sets

In addition to the operators above, the following AIMMS functions also
operate on subsets of :any:`AllIdentifiers`:

-  :any:`GenerateXML`,

-  :any:`CaseCompareIdentifier`,

-  :any:`CaseCreateDifferenceFile`,

-  :any:`IdentifierMemory`,

-  :any:`GMP::Solution::SendToModelSelection`,

-  :any:`VariableConstraints`,

-  :any:`ConstraintVariables`,

-  :any:`ScalarValue`,

-  :any:`SectionIdentifiers`,

-  :any:`AttributeToString`,

-  :any:`IdentifierAttributes`.

See also :ref:`chap:model.query.functions` of the AIMMS `Function Reference <https://documentation.aimms.com/functionreference/>`__.