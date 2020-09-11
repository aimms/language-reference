.. _sec:set.index:

``INDEX`` Declaration and Attributes
====================================

.. rubric:: Direct versus indirect declaration

Every index used in your model must be declared exactly once. You can
declare indices *indirectly*, through the ``Index`` attribute of a
simple set, or *directly* using an ``Index`` declaration. Note that all
previous examples show indirect declaration of indices.

.. _index:

.. rubric:: ``Index`` declaration

When you choose to declare an index not as an attribute of a set
declaration, you can use the ``Index`` declaration. The attributes of
each single index declaration are given in
:numref:`table:set.attr-index`.

.. _table:set.attr-index:

.. table:: 

	=========== ================ ==========================================================
	Attribute   Value-type       See also page
	=========== ================ ==========================================================
	``Range``   *set-identifier*    
	``Text``    *string*         :ref:`The Text and Comment attribute <attr:prelim.text>`
	``Comment`` *comment string* :ref:`The Text and Comment attribute <attr:prelim.text>`
	=========== ================ ==========================================================
	
.. rubric:: The ``Range`` attribute
   :name: attr:set.index-range

.. _index.range:

You can assign a default binding with a specific set to directly
declared indices by specifying the ``Range`` attribute. If you omit this
``Range`` attribute, the index has no default binding to a specific set
and can only be used in the context of local or implicit index binding.
The details of index binding are discussed in :ref:`sec:bind.rules`.

.. rubric:: Example

The following declaration illustrates a direct ``Index`` declaration.

.. code-block:: aimms

	Index c {
	    Range : Customers;
	}