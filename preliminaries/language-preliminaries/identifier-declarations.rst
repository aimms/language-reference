Identifier Declarations
=======================

.. _identifier:

.. rubric:: Identifier types

Identifiers are the unique names through which you can refer to entities
in your model. The most common identifier types in AIMMS are:

-  *set*-used for indexing parameters and variables,

-  *parameter*-for (multidimensional) data storage,

-  *variable* and *arc*-entities of constraints that must be determined,

-  *constraint* and *node*-relationships between variables or arcs,
   usually in the form of (in)equalities,

-  *mathematical program*-an objective and a collection of constraints,
   and

-  *procedure* and *function*-code segments to initiate execution.

.. rubric:: Declaration forms

The declarations of all identifiers, procedures and functions within an
AIMMS application can be provided by means of a uniform attribute
notation. For every node within the model tree you can view and change
the value of these attributes through a graphical declaration form. This
form will show all the attributes that are associated with a particular
identifier type, along with their values for the identifier at hand.

.. rubric:: Notation used in this manual

In this manual we have chosen to use a textual style representation of
all model declarations, which closely resembles the graphical
representation in the model tree. In view of the large number of
declarations in this manual, we found that a purely graphical
presentation in the text was visually distracting. In contrast, the
adopted textual representation is succinct and integrates well with the
surrounding text.

.. _attr:prelim.comment:

.. _text:

.. _comment:

.. rubric:: The ``Text`` and ``Comment`` attributes
   :name: attr:prelim.text

With every declaration in a model you can associate a ``Text`` and a
``Comment`` attribute. The ``Comment`` attribute is aimed at the
modeler, and can be used to describe the contents of a particular node
in the model tree, or make remarks that are relevant for later
reference. The ``Text`` attribute is intended for use in the graphical
user interface and reporting. It can contain a single line description
of the identifier at hand. Many objects in the AIMMS user interface
allow you to display this text along with the identifier value(s).

.. rubric:: Predefined identifiers

Not only does an AIMMS model consist of sets, parameters and variables
that have been defined by you, and thus are specific for your
application, AIMMS also provides a number of predefined system
identifiers. These identifiers characterize either

-  a set of *all* objects with a particular property, for instance the
   set of :any:`AllIdentifiers` or the set of :any:`AllCases`, or

-  the *current* value of a particular modeling aspect, for instance the
   parameter :any:`CurrentCase` or the parameter :any:`CurrentPageNumber`.

In most cases these identifiers are read-only, and get their value based
on the declarations and settings of your model.

.. rubric:: Section identifiers

The structuring sections in your model tree are also considered as AIMMS
identifiers. The blanks in a section description are replaced by
underscores to form a legal AIMMS identifier name. The identifier thus
formed is a subset of :any:`AllIdentifiers`. This subset contains all the
model identifiers that have been declared underneath the associated
node. You can conveniently use such sets in, for instance, the ``EMPTY``
statement to clean a entire group of identifiers in a single statement,
or to construct your own subsets of :any:`AllIdentifiers` using the set
operations available in AIMMS.