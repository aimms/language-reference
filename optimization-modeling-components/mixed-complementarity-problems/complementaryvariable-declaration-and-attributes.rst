.. _sec:compl.variable:

``ComplementaryVariable`` Declaration and Attributes
====================================================

.. _complementarity_variable:

.. rubric:: Complementarity variables

To support you in formulating a complementarity model, AIMMS provides a
special type of variable, the ``ComplementaryVariable``. The attributes
of a complementarity variable allow you to declare an (indexed) class of
variables in a complementarity model along with their associated
constraints. The attributes of a ``ComplementaryVariable`` are listed in
:numref:`table:compl.attr-compl`.

.. rubric:: Automatic sanity checks

By construction, this new variable type automatically ensures that every
variable in a complementarity model is associated with a single
constraint. Also, when AIMMS detects that the total number of (finite)
bounds on both the complementarity variable and its associated
constraint is not equal to two (as required above), a compilation error
will result. Thus, ``ComplementaryVariable`` will help to reduce the
most common declaration errors for this type of model.

.. _table:compl.attr-compl:

.. table:: 

	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| Attribute        | Value-type                 | See also page                                                                                                                         |
	+==================+============================+=======================================================================================================================================+
	| ``IndexDomain``  | *index-domain*             | :ref:`The Parameter IndexDomain attribute <attr:par.index-domain>`, :ref:`The Variable IndexDomain attribute <attr:var.index-domain>` |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``Range``        | *range*                    | :ref:`here <attr:var.range>`                                                                                                          |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``Unit``         | *unit-valued expression*   | :ref:`The Parameter Unit attribute <attr:par.unit>`, :ref:`The Variable Unit attribute <attr:var.unit>`                               |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``Text``         | *string*                   | :ref:`here <attr:prelim.text>`, :ref:`here <attr:par.text>`                                                                           |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``Comment``      | *comment string*           | :ref:`here <attr:prelim.comment>`                                                                                                     |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``Complement``   | *expression*               | :ref:`here <attr:var.constr.definition>`                                                                                              |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``NonvarStatus`` | *reference*                | :ref:`here <attr:var.nonvar>`                                                                                                         |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	| ``Property``     | ``NoSave``, ``Complement`` |                                                                                                                                       |
	+------------------+----------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
	
.. _complementarity_variable.index_domain:

.. rubric:: The ``IndexDomain`` attribute

Through the ``IndexDomain`` attribute of a complementarity variable you
can specify domain of tuples for which you want AIMMS to generate a
variable and its associated constraint. During generation, AIMMS will
only generate a variable for all tuples that satisfy all domain
restrictions that you have imposed on the domain.

.. _complementarity_variable.range:

.. rubric:: The ``Range`` attribute

In the ``Range`` attribute you can specify the lower and upper bound of
a complementarity variable, in a similar manner for ordinary
``Variables`` (see also :ref:`sec:var.var`). During generation, AIMMS
will perform a runtime check, for every individual tuple in the index
domain, whether the number of finite bounds specified here, plus the
number of finite bounds in the constraint specified in the
``Complement`` attribute, exactly equals two.

.. _complementarity_variable.complement:

.. rubric:: The ``Complement`` attribute

The ``Complement`` attribute allows you to specify the constraint that
must be associated with the complementarity variable at hand. With
:math:`f(x,\dots)` a general nonlinear function, the following types of
expressions are allowed

-  :math:`\phantom{a\leq{}}f(x,\dots)\geq a` (variable must have a
   single-sided ``Range``),

-  :math:`\phantom{a\leq{}}f(x,\dots)\leq a` (variable must have a
   single-sided ``Range``),

-  :math:`a \leq f(x,\dots) \leq b` (variable must be free),

-  :math:`\phantom{a\leq{}}f(x,\dots)= a` (variable must be free), or

-  :math:`\phantom{a\leq{}}f(x,\dots)\phantom{{}\leq b}` (variable must
   be bounded).

In addition, the ``Complement`` attribute can refer to an existing
``Constraint`` in your model, which then should hold a definition as one
of the cases above. The ``Complement`` attribute can also hold a scalar
element parameter into the set :any:`AllConstraints`, which offers the
possibility to assign different constraints to the complementarity
variable in sequential solves.

.. rubric:: Constraint listing

In the constraint listing, the constraints associated with a
complementarity variable will be listed with a generated name consisting
of the name of the ``ComplementarityVariable`` with an additional suffix
``_complement``.

.. _complementarity_variable.nonvar_status:

.. rubric:: The ``NonvarStatus`` attribute

With the ``NonvarStatus`` attribute you can indicate for which tuples
you want AIMMS to consider the complementarity variable as a parameter,
i.e. with the lower and upper bound set equal to the level value prior
to solving the model (see also :ref:`sec:var.var.solver-attr`). From the
mixed complementarity condition it follows that the function in the
corresponding constraint is then allowed to assume arbitrary values,
whence there is no strict need to generate the variable and constraint
for the solver.

.. rubric:: Positive and negative values

The value of the ``NonvarStatus`` attribute must be an expression in
some or all of the indices in the index list of the variable, allowing
you to change the nonvariable status of individual elements or groups of
elements at once. When the ``NonvarStatus`` assumes a positive value,
AIMMS will not generate the variable and its associated constraint. For
negative values, the variable and constraint will be generated, but
reduces to the second special case of the mixed complementarity
condition

.. math:: \hat{x}_i = x_i - x_i^0 = 0 \quad \text{and}\quad f_i(x) \text{ is "free"},

i.e. the function in the constraint will be allowed to assume arbitrary
values.

.. _complementarity_variable.unit:

.. rubric:: The Unit attribute

Providing a unit for a complementarity variable will help you in a
number of ways.

-  AIMMS will help you to check the consistency of all the constraints
   and assignments in your model (including the expression in the
   ``Complement`` attribute), and

-  AIMMS will use the units to scale the model that is sent to the
   solver.

Proper scaling of a model will generally result in a more accurate and
robust solution process. You can find more information on the definition
and use of units to scale mathematical programs in :ref:`chap:units`.

.. _complementarity_variable.property:

.. rubric:: The ``Property`` attribute

Complementarity variables support the properties ``NoSave`` and
``Complement``. With the property ``NoSave`` you indicate that you do
not want to store data associated with this variable in a case. The
``Complement`` property indicates that you are interested in the level
values of the constraint defined in the ``Complement`` attribute. When
this property is set, AIMMS will make the level value of this constraint
available through the :ref:`.Complement` suffix of the complementarity
variable at hand.

.. rubric:: Example

The declaration of the complementarity variable ``MembraneHeight``
expresses a complementarity condition for the height of a membrane in a
rectangular :math:`(x,y)`-grid, with a uniform external force acting on
each cell in the grid.

.. code-block:: aimms

	ComplementaryVariable MembraneHeight {
	    IndexDomain  : (x,y);
	    Range        : [MembraneLowerBound(x,y), MembraneUpperBound(x,y)];
	    Complement   : {
	        4*MembraneHeight(x,y)
	        - MembraneHeight(x+1,y) - MembraneHeight(x-1,y)
	        - MembraneHeight(x,y+1) - MembraneHeight(x,y-1)
	        - CellForce
	    }
	}

The complementarity condition expresses that either the membrane reaches
one its given bounds (for instance, an obstacle placed in the way of the
membrane), or the external force on the cell must be equal to the
internal forces acting on the cell caused by differences in height with
neighboring cells.