.. _sec:units.unit-par:

Unit-valued Parameters
======================

.. rubric:: Parametrized units

In some cases not all entries of an indexed identifier have the same
associated unit. An example is the diet model where the nutritive value
of each nutrient for a single serving of a particular food type is
measured in a different unit.

.. _unit_parameter:

.. rubric:: Unit-valued parameters

In order to deal with such situations, AIMMS allows the declaration of
(indexed) *unit-valued* parameters which you can use in the unit
definition of the other parameters and variables in your model. In the
model tree, unit-valued parameters are available as a special type of
parameter declaration, with attributes as given in
:numref:`table:units.attr-unit-par`.

.. _table:units.attr-unit-par:

.. table:: 

	+-----------------+-------------------+--------------------------------------------------------------+
	| Attribute       | Value-type        | See also page                                                |
	+=================+===================+==============================================================+
	| ``IndexDomain`` | *index-domain*    |                                                              |
	+-----------------+-------------------+--------------------------------------------------------------+
	| ``Quantity``    | *quantity*        |                                                              |
	+-----------------+-------------------+--------------------------------------------------------------+
	| ``Default``     | *unit-expression* |                                                              |
	+-----------------+-------------------+--------------------------------------------------------------+
	| ``Property``    | ``NoSave``        | :ref:`The Property attribute <attr:module.property>`         |
	+-----------------+-------------------+--------------------------------------------------------------+
	| ``Text``        | *string*          | :ref:`The Text and Comment attributes <attr:prelim.comment>` |
	+-----------------+-------------------+--------------------------------------------------------------+
	| ``Comment``     | *comment string*  | :ref:`The Text and Comment attributes <attr:prelim.comment>` |
	+-----------------+-------------------+--------------------------------------------------------------+
	| ``Definition``  | *unit-expression* |                                                              |
	+-----------------+-------------------+--------------------------------------------------------------+
	
.. _unit_parameter.quantity:

.. rubric:: The ``Quantity`` attribute

You should specify the ``Quantity`` attribute if all unit values stored
in the unit parameter can be associated with a single quantity declared
in your model. The effect of specifying a quantity in the ``Quantity``
attribute of a unit parameter is twofold:

-  during assignments to the unit parameter, AIMMS will verify whether
   the assigned unit values are commensurate with the base unit of
   specified quantity, and

-  AIMMS will modify its (compile-time) unit analysis to use the
   specified quantity rather than an artificial quantity based on the
   name of the unit parameter (see below).

.. _unit_parameter.default:

.. _unit_parameter.defintion:

.. rubric:: The ``Default`` and ``Definition`` attributes

The ``Default`` and ``Definition`` attributes of a unit parameter have
the same purpose as the ``Default`` and ``Definition`` attribute of
ordinary parameters, except that the resulting values must be unit
expressions (see :ref:`sec:units.expr`). If you have specified a
quantity in the ``Quantity`` attribute, AIMMS will verify that these
unit expressions are commensurate with the specified quantity.

.. rubric:: Allowed unit values

All unit values read from an external data source, or assigned to a unit
parameter, either via an assignment or through its ``Definition``
attribute, must evaluate to existing unit symbols only. A compile- or
runtime error will occur, when a unit value refers to a unit symbol that
is not defined in any of the ``Quantity`` declarations contained in your
model.

.. rubric:: Use of unit parameters

With unit parameters you can create, store and manipulate scalar or
multidimensional collections of unit values. The unit values stored in a
unit parameter can be used, for instance:

-  to associate a parametrized (i.e. multidimensional) collection of
   units with a single multidimensional identifier (through its :any:`Unit`
   attribute), or

-  to specify a local unit override based on a unit (or collection of
   units) that is not known a priori.

.. rubric:: Unit analysis...

When a :any:`Unit` attribute of an identifier contains a reference to a
unit parameter, this can, but need not, modify the way in which AIMMS
conducts its usual unit analysis. There are two distinct scenarios, both
described below.

.. rubric:: ...with associated quantity

If the unit parameter has an associated quantity (specified through its
``Quantity`` attribute), all units stored in the unit parameter are
known to be commensurate with the base unit of the quantity, although
the individual scale factors may be different if the unit parameter is
multidimensional. In this case, AIMMS will base its unit analysis on the
associated quantity.

.. rubric:: ...without associated quantity

If there is no associated quantity, AIMMS will introduce an artificial
quantity solely on the basis of the symbolic name of the unit parameter
(i.e. without consideration of its dimension), and base all further unit
analysis on this artificial quantity only. If there is unit consistency
at the level of these artificial quantities, this automatically ensures,
for multidimensional unit parameters, unit consistency at the individual
level as well, regardless of the specific individual unit values stored
in it.

.. rubric:: Example

Consider the following declarations of unit-valued parameters, where
``f`` is an index into the set ``Foods`` and ``n`` an index into the set
``Nutrients``.

.. code-block:: aimms

	UnitParameter NutrientUnit {
	    IndexDomain  : n;
	}
	UnitParameter FoodUnit {
	    IndexDomain  : f;
	}

With these unit-valued parameters you can specify meaningful indexed
unit expressions for the :any:`Unit` attribute of the following parameters.

.. code-block:: aimms

	Parameter NutritiveValue {
	    IndexDomain  : (f,n);
	    Unit         : NutrientUnit(n)/FoodUnit(f);
	}
	Parameter NutrientMinimum {
	    IndexDomain  : n;
	    Unit         : NutrientUnit(n);
	}
	Variable Serving {
	    IndexDomain  : f,
	    Unit         : FoodUnit(f);
	}

With these declarations, you can now easily verify that all terms in the
definition of the following constraint are unit consistent at the
symbolic level.

.. code-block:: aimms

	Constraint NutrientRequirement {
	    IndexDomain  : n;
	    Unit         : NutrientUnit(n);
	    Definition   : sum[ f, Servings(f)*NutritiveValue(f,n) ] >=  NutrientMinimum(n);
	}

.. rubric:: Indexed scaling

When the :any:`Unit` attribute of an identifier is parametrized by means of
indexed unit parameter, AIMMS will correctly scale all data exchange
with external components (see :ref:`sec:units.scaling`). During data
exchange with an external component, AIMMS considers the specified units
at the individual (indexed) level, and will determine the proper scaling
for every individual index position. In addition, when a unit convention
is active, AIMMS will scale all individual entries according to that
convention, as applied to the corresponding individual entries of the
indexed unit parameter. As usual, all data of an identifier with a
parametrized associated unit will be stored internally in the
corresponding atomic unit of every individual index value.

.. rubric:: Example revisited

When AIMMS generates mathematical program which contains the variable
``Serving(f)``, each column corresponding to this variable will be
scaled according to the scale factor of the particular unit stored in
``FoodUnit(f)`` with respect to their corresponding atomic unit
expressions. Similarly, AIMMS will scale the columns corresponding to
the constraint ``NutrientRequirement(n)`` according the scale factors of
the units stored in ``NutrientUnit(n)`` with respect to their
corresponding atomic unit expressions.

.. rubric:: Initializing unit-valued parameters

You can initialize a unit-valued parameter through lists, tables, and
composite tables like you can initialize any other AIMMS parameter (see
:ref:`chap:text.data.file`). The values of the individual entries must
be valid unit constants (see :ref:`sec:units.expr`), and must be
surrounded by square brackets. For compound units constants you can
optionally indicate the associated quantity in a similar way as in the
unit definition of a parameter.

.. rubric:: Example

The following list initializes the unit-valued parameter
``NutrientUnit`` for a particular set of ``Nutrients``.

.. code-block:: aimms

	NutrientUnit := DATA { Energy  : [kJ]  ,
	                       Protein : [mg]  ,
	                       Iron    : [%RDA]  };

.. rubric:: Unit parameters and databases

In addition, AIMMS allows you to read the initial data of a unit
parameter from a database table, and write the values of a unit
parameter to a database table. The unit values in the database table
must be unit constants, and must be stored without square brackets.

.. rubric:: Simultaneous unit and data initialization

When a composite table in a data file, or a table in a database contains
both the values of a multidimensional unit parameter, and a
corresponding numeric parameter whose :any:`Unit` attribute references that
unit parameter, AIMMS allows you to read both identifiers in a single
pass. When reading both identifiers, AIMMS will make sure that the
numeric values are interpreted with respect to the corresponding unit
value that is read simultaneously.

.. rubric:: Constant versus parametrized units

AIMMS even allows you to make assignments from identifiers with a
constant unit to identifier slices of identifiers with a parametrized
unit and vice versa. If AIMMS detects this special situation during
compilation of your model, it will postpone the compile unit consistency
check whenever necessary, and replace it with a runtime consistency
check which is performed every time the assignment is executed. Because
all data is stored by AIMMS with respect to atomic units internally,
unit consistency again automatically implies scale consistency.

.. rubric:: Example

Given the declarations of the previous example, assume the existence of
an additional parameter ``EnergyContent(f)`` with a constant associated
unit, say ``Kcal``. Then, AIMMS will postpone the compile unit
consistency check for the following two statements, and replace it with
a runtime check.

.. code-block:: aimms

	NutritiveValue(f,'Energy') := EnergyContent(f);
	EnergyContent(f)           := NutritiveValue(f,'Energy');

The runtime unit consistency check will only succeed, whenever the unit
value of the unit parameter ``NutrientUnit('Energy')`` is commensurate
with the constant unit ``Kcal``.

.. rubric:: Restrictions

AIMMS will only replace a compile time with a runtime unit consistency
check if a unique unit can be associated with the right-hand side of the
assignment at compile time. If the assigned expression consists of
subexpressions which have different associated unit expressions at
compile time, a compile time error will result. This is even the case
when, at runtime, these unit expressions evaluate to units that are
commensurate with the unit of the left-hand side of the assignment.