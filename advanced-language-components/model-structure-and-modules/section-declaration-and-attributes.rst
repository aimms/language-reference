.. _sec:module.section:

``Section`` Declaration and Attributes
======================================

.. _section:

.. rubric:: ``Section`` declaration and attributes

``Section`` nodes provide depth to the model tree, and offer facilities
to store parts of your model in separate source files. A ``Section``
node is always a child of the ``Model`` node, of another ``Section``
node, or of a ``Module`` node. The attributes of ``Section`` nodes are
listed in :numref:`table:module.attr-section`.

.. _table:module.attr-section:

.. table:: 

	============== ================ ============================================================
	Attribute      Value-type       See also page
	============== ================ ============================================================
	``SourceFile`` *string*            
	``Property``   ``NoSave``          
	``Comment``    *comment string* :ref:`The Text and Comment attributes <attr:prelim.comment>`
	============== ================ ============================================================

.. _section.source_file:

.. _attr:module.source-file:

.. rubric:: The ``SourceFile`` attribute

With the ``SourceFile`` attribute you can indicate that the contents of
a ``Section`` node in your model is linked to the specified source file.
As a consequence, AIMMS will read the contents of the ``Section`` node
from the specified file during compilation of the model. Any
modifications to the part of the model contained in such a ``Section``
node will also be stored in this source file when you save the model.
When you select an existing source file for the ``SourceFile`` attribute
of a ``Section`` node in the **Model Explorer** (see also
Section 4.2 of the `User's Guide <https://documentation.aimms.com/_downloads/AIMMS_user.pdf>`__), any previous contents of
that section will be lost.

.. _attr:module.property:

.. rubric:: The ``Property`` attribute

In the ``property`` attribute the ``NoSave`` property can be specified.
When the property ``NoSave`` is set, none of the identifiers declared in
the section will be saved in cases.

.. rubric:: Section names as identifier subsets

Whenever you add a ``Section`` node to the model tree, the name of the
``Section`` node (with spaces replaced by underscores), will also be
available within your model as an implicit subset of the predeclared set
:any:`AllIdentifiers`. The contents of this subset is fixed, and is defined
as the set of all identifiers declared within the subtree corresponding
to the ``Section`` node. You can use this implicitly created set, for
instance, in the ``EMPTY`` statement to empty all section identifiers
using only a single statement.