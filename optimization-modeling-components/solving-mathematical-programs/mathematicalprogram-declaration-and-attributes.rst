.. _sec:mp.mp:

.. _ssec:decl:constr-mp:mp:

``MathematicalProgram`` Declaration and Attributes
==================================================

.. _mathematical_program:

.. rubric:: Attributes

The attributes of mathematical programs are listed in
:ref:`this table <table:mp.attr-mp>`.

.. _table:mp.attr-mp:

.. table:: 

	+----------------------+----------------------------+------------------------------------+
	| Attribute            | Value-type                 | See also page                      |
	+======================+============================+====================================+
	| ``Objective``        | *variable-identifier*      |                                    |
	+----------------------+----------------------------+------------------------------------+
	| ``Direction``        | ``minimize``, ``maximize`` |                                    |
	+----------------------+----------------------------+------------------------------------+
	| ``Variables``        | *variable-set*             |                                    |
	+----------------------+----------------------------+------------------------------------+
	| ``Constraints``      | *constraint-set*           |                                    |
	+----------------------+----------------------------+------------------------------------+
	| ``Type``             | *model-type*               |                                    |
	+----------------------+----------------------------+------------------------------------+
	| ``ViolationPenalty`` | *reference*                | :ref:`sec:mp.infeas`               |
	+----------------------+----------------------------+------------------------------------+
	| ``Text``             | *string*                   | :ref:`here <attr:prelim.text>`     |
	+----------------------+----------------------------+------------------------------------+
	| ``Comment``          | *comment string*           | :ref:`here <attr:prelim.comment>`  |
	+----------------------+----------------------------+------------------------------------+
	| ``Convention``       | *convention*               | :ref:`sec:units.convention`        |
	+----------------------+----------------------------+------------------------------------+
	
.. rubric:: Example

The following example illustrates a typical mathematical program.

.. code-block:: aimms

	MathematicalProgram TransportModel {
	    Objective   : TransportCost;
	    Direction   : minimize;
	    Constraints : AllConstraints;
	    Variables   : AllVariables;
	    Type        : lp;
	}

It defines the linear program ``TransportModel``, which is built up from
all constraints and variables in the model text. The variable
``TransportCost`` serves as the objective function to be minimized.

.. rubric:: The ``Objective`` attribute
   :name: attr:mp.objective

.. _mathematical_program.objective:

With the ``Objective`` attribute you can specify the objective of your
mathematical program. Its value must be a reference to a (defined)
variable or any other variable expression. When you want to use the
objective value in the end-user interface of your model, the
``Objective`` attribute must be a variable reference.

.. rubric:: Omitting the objective

If you do not specify an objective, your mathematical program will be
solved to find a feasible solution and it will then terminate.

.. rubric:: The ``Direction`` attribute
   :name: attr:mp.direction

.. _mathematical_program.direction:

In conjunction with an objective you must use the ``Direction``
attribute to indicate whether the solver should ``minimize`` or
``maximize`` the objective. During a ``SOLVE`` statement you can
override this direction by using a ``WHERE`` clause for the
``direction`` option.

.. rubric:: The ``Variables`` attribute
   :name: attr.mp.variables

.. _mathematical_program.variables:

.. _allvariables-LR:

With the ``Variables`` attribute you can specify which set of variables
are to be included in your mathematical program. Its must be either the
predefined set :any:`AllVariables` or a subset thereof. The set
:any:`AllVariables` is predefined by AIMMS, and it contains the names of
all the variables declared in your model. Its contents cannot be
changed. If you mathematical program contains an objective, AIMMS will
automatically add this to set of generated variables during generation.

.. rubric:: Variables as parameters

If the ``Variables`` attribute is assigned a subset of the set
:any:`AllVariables`, AIMMS will treat all the variables outside this set as
if they were parameters. That is, all occurrences of such variables will
not result in the generation of individual variables for the solver, but
will be accounted for in the right-hand side of the constraint according
to their value during generation.

.. rubric:: Compare to ``NonvarStatus``

The ``Variables`` attribute performs a similar function as the
``NonvarStatus`` attribute or the ``.NonVar`` suffix of a variable (see
also :ref:`sec:var.var`). The ``Variables`` attribute in a mathematical
program allows you to quickly change the status of an entire class of
variables, while the ``NonvarStatus`` (in a variable declaration) gives
much finer control at the individual level. As shown below, the latter
is very useful to perform model algebra.

.. rubric:: The ``Constraints`` attribute
   :name: attr:mp.constraints

.. _mathematical_program.constraints:

.. _allconstraints-LR:

With the ``Constraints`` attribute you can specify which constraints are
part of your mathematical program. Its value must be either the
predefined set :any:`AllConstraints` or a subset thereof. The set
:any:`AllConstraints` contains the names of all declared constraints plus
the names of all variables which have a definition attribute. Its
contents is computed at compile time, and cannot be changed.

-  If you specify the set :any:`AllConstraints`, AIMMS will generate
   individual constraints for all declared constraints and variables
   with a definition.

-  If you specify a subset of the set :any:`AllConstraints`, AIMMS will
   only generate individual constraints for the declared constraints and
   defined variables in that subset.

If you mathematical program has an objective which is a defined
variable, its definition is automatically added to the set of generated
constraints during generation.

.. rubric:: Defined variables

Variables with a nonempty definition attribute have a somewhat special
status. Namely, for every defined variable AIMMS will not only generate
this variable, but will also generate a constraint containing its
definition. Therefore, defined variables are contained in both the
predefined sets :any:`AllVariables` and :any:`AllConstraints`. You can add a
defined variable to the variable and constraint set of a mathematical
program independently.

-  If you omit a defined variable from the variable set of a
   mathematical program, all occurrences of the variable will be fixed
   to its current value and accounted for in the right-hand side of all
   constraints.

-  If you omit a defined variable from the constraint set of a
   mathematical program, the defining constraint will not be generated.

.. rubric:: Performing model algebra

By changing the contents of the identifier sets that you have entered at
the ``Variables`` and ``Constraints`` attributes of a mathematical
program you can perform a simple form of *model algebra*. That is, you
can investigate the effects of adding or removing constraints from
within the graphical interface. Furthermore, it allows you to
reconfigure your model based on the value of your model data.

.. rubric:: Synchronizing variable and constraint sets

When changing the contents of either the variable or the constraint set
of a mathematical program, you may find that the contents of the other
set also needs some adjustment. For instance, adding a variable to a
mathematical program makes no sense if there are no constraints that
refer to it. AIMMS offers two special set-valued functions to help you
to accomplish this task.

.. _variableconstraints-LR:

.. rubric:: The function :any:`VariableConstraints`

The function :any:`VariableConstraints` takes a subset of the predefined
set :any:`AllVariables` as its argument, and returns a subset of the
predefined set :any:`AllConstraints`. The resulting constraint set contains
all constraints which use one or more of the variables in the argument
set.

.. _constraintvariables-LR:

.. rubric:: The function :any:`ConstraintVariables`

The function :any:`ConstraintVariables` performs the opposite task. It
takes a subset of the set :any:`AllConstraints` as its arguments, and
returns a subset of the set :any:`AllVariables`. The resulting variable set
contains all variables which are referred to in one or more constraints
in the argument set. Also included are all variables referred to in the
definitions of other variables inside the set.

.. rubric:: Example

Consider the use of the functions :any:`VariableConstraints` and
:any:`ConstraintVariables` in conjunction with the following declaration of
a mathematical program.

.. code-block:: aimms

	MathematicalProgram PartialTransportModel {
	    Objective   : TransportCost;
	    Direction   : minimize;
	    Constraints : PartialConstraintSet;
	    Variables   : PartialVariableSet;
	}

Assume that the set ``PartialVariableSet`` contains a subset of the
variables declared in the model. Further assume that you would like to
build up the contents of the set ``PartialConstraintSet`` together with
the required additions to ``PartialVariableSet`` so that the contents of
both sets are maximal. This is referred to as their transitive closure.
By successively calling the functions :any:`VariableConstraints` and
:any:`ConstraintVariables`, the following loop computes the transitive
closure of the variable and constraint sets.

.. code-block:: aimms

	repeat
	   PreviousCardinality  := Card( PartialVariableSet );
	   PartialConstraintSet := VariableConstraints( PartialVariableSet   );
	   PartialVariableSet   := ConstraintVariables( PartialConstraintSet );

	   break when Card( PartialVariableSet ) = PreviousCardinality;
	endrepeat ;

The ``break`` occurs when the set ``PartialVariableSet`` has not
increased in size.

.. rubric:: The ``Type`` attribute
   :name: attr:mp.type

.. _mathematical_program.type:

With the ``Type`` attribute of a mathematical program you can prescribe
a solution type. When the specified type is not compatible with the
generated mathematical program, AIMMS will return an error message. You
can override the type during a ``SOLVE`` statement using a ``WHERE``
clause for the ``type`` option. You can use this, for instance, to
easily switch between the ``mip`` and ``rmip`` types.

.. rubric:: Available types

A complete list of the mathematical program types available within AIMMS
is given in :ref:`this table <table:mp.types>`. Most are self-explanatory. When
the type ``rmip`` is specified, all integer variables are treated as
continuous within their bounds. The ``rmip`` type is the global version
of the ``Relax`` attribute associated with individual variables (see
also :ref:`sec:var.var`). The types ``ls`` and ``nls`` can only be
selected in the absence of the ``Objective`` attribute.

.. _table:mp.types:

.. table:: Available model types with AIMMS

   =========== ====================================================
   Type        Description
   =========== ====================================================
   ``lp``      linear program
   ``ls``      linear system
   ``qp``      quadratic program
   ``nlp``     nonlinear program
   ``nls``     nonlinear system
   ``mip``     mixed integer program
   ``rmip``    relaxed mixed integer program
   ``minlp``   mixed integer nonlinear program
   ``rminlp``  relaxed mixed integer nonlinear program
   ``qp``      quadratic program
   ``miqp``    mixed integer quadratic program
   ``qcp``     quadratic constraint program
   ``miqcp``   mixed integer quadratic constraint program
   ``network`` pure network program
   ``mcp``     mixed complementarity program
   ``mpcc``    mathematical program with complementarity constraint
   =========== ====================================================

.. _mathematical_program.convention:

.. rubric:: The ``Convention`` attribute

You can use the ``Convention`` attribute to specify the unit convention
that you want to be used for scaling the variables and constraints in
your mathematical program. For further details on this issue you are
referred to :ref:`sec:units.convention`.

.. _mathematical_program.violation_penalty:

.. rubric:: The ``ViolationPenalty`` attribute

With the ``ViolationPenalty`` attribute you can instruct AIMMS to
automatically add artificial terms to the constraints of your
mathematical program to help resolve and/or track infeasibilities in
your mathematical program. Infeasibility analysis and the use of the
``ViolationPenalty`` attribute is discussed in full detail in
:ref:`sec:mp.infeas`.