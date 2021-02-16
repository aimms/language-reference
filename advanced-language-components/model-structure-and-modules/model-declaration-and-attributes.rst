.. _sec:module.model:

``Model`` Declaration and Attributes
====================================

.. _model:

.. rubric:: ``Model`` declaration and attributes

The ``Model`` node defines the root node of the entire model tree
associated with an AIMMS modeling project. The attributes of the main
``Model`` node are listed in :ref:`this table <table:module.attr-model>`. All
attributes of the ``Model`` node have a global impact on the entire
modeling project.

.. _table:module.attr-model:

.. table:: 

	+----------------+-----------------------------------+----------------------------+
	| Attribute      | Value-type                        | See also page              |
	+================+===================================+============================+
	| ``Convention`` | *convention*, *element-parameter* |                            |
	+----------------+-----------------------------------+----------------------------+
	| ``Comment``    | *comment string*                  | :ref:`attr:prelim.comment` |
	+----------------+-----------------------------------+----------------------------+
	
.. _model.convention:

.. rubric:: The ``Convention`` attribute

With the ``Convention`` attribute you can indicate that all I/O with
respect to identifiers in your model is to take place according to the
unit convention specified in this attribute. The value of this attribute
must be either a direct reference to a convention declared in your
model, an element parameter into the set :any:`AllConventions` or a string
parameter holding the name of a convention within your model. You can
find more detailed information about unit conventions and their usage in
:ref:`sec:units.convention`