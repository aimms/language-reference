.. _sec:expr.macro:

``MACRO`` Declaration and Attributes
====================================

.. rubric:: ``Macro`` facility

The ``MACRO`` facility offers a mechanism for parameterizing
expressions. Macros are useful for enhancing the readability of models,
and avoiding inconsistencies in frequently used expressions.

.. _macro:

.. rubric:: Declaration and attributes

Macros are declared as ordinary identifiers in your model. They can have
arguments. The attributes of a ``Macro`` declaration are listed in
:numref:`table:expr.attr-macro`.

.. _table:expr.attr-macro:

.. table:: 

	============== ================ =======================================================
	Attribute      Value-type       See also page
	============== ================ =======================================================
	``Text``       *string*         :ref:`The Text attribute <attr:prelim.text>`
	``Arguments``  *argument-list*     
	``Comment``    *comment string* :ref:`The Comment attribute <attr:prelim.comment>`
	``Definition`` *expression*     :ref:`The Definition attribute <attr:set.definition>`
	============== ================ =======================================================
	
.. _macro.definition:

.. _macro.arguments:

.. rubric:: The ``Definition`` attribute

The ``Definiton`` attribute of a macro declaration is the replacement
text that is substituted when a macro is used in the model text. The
(optional) ``Arguments`` of a macro must be scalar entities. Unlike
function arguments, however, you do not have to declare ``Macro``
arguments as local identifiers. The ``Definition`` of a macro must be a
valid expression in its arguments.

.. rubric:: Example

When you define a macro with arguments, the actual replacement text
depends on the arguments that are supplied to it, as illustrated in the
following example. Using the macro declaration

.. code-block:: aimms

	Macro MyAverage {
	    Arguments  : (dom, expr);
	    Definition : Sum(dom, expr) / Count(dom);
	}

the assignments

.. code-block:: aimms

	AverageTransport   := MyAverage( (i,j), Transport(i,j) );
	AverageNZTransport := MyAverage( (i,j) | Transport(i,j),  Transport(i,j) );

are compiled as if they read:

.. code-block:: aimms

	AverageTransport   := Sum( (i,j), Transport(i,j) ) / Count( (i,j) );
	AverageNZTransport :=
	       Sum  ( (i,j) | Transport(i,j),  Transport(i,j) ) /
	       Count( (i,j) | Transport(i,j) );

.. rubric:: Expression substitution

When you use a macro with arguments, the actual arguments *must* be
valid expressions. As a result, there is no need to add additional
braces to the replacement text of the macro, like, for instance, in the
``C`` programming language. The following example illustrates this
point.

.. code-block:: aimms

	Macro MyMult {
	    Arguments  : (x,y);
	    Definition : x*y;
	}

Using this macro, the expression

.. code-block:: aimms

	a + MyMult(b+c,d+e) + f

will evaluate to

.. code-block:: aimms

	a + ((b+c)*(d+ e)) + f

instead of

.. code-block:: aimms

	a + b + c*d + e + f

.. rubric:: Macro versus defined parameters

In many execution statements you have a choice to use either macros or
defined parameters as a mechanism to replace complicated expressions by
descriptive names. While a macro is purely substituted by its
replacement text, the current value of a defined parameter is stored and
looked up when needed. When deciding whether to use a macro or a defined
parameter, you should consider both storage and computational
consequences. Macros are recomputed every time they are referenced, and
therefore there may be an unnecessary time penalty if the macro is
called with identical arguments in more than one place within your
model. When storage considerations are important, a macro may be
attractive since it does not introduce additional parameters.

.. rubric:: Macro versus defined variables

You should also consider your choices when you use a macro with
variables as arguments in a constraint. In this case, you also have the
option to use a defined variable, or a defined ``Inline`` variable (see
also :ref:`sec:var.var`). The following considerations are of interest.

-  A macro can produce different expressions of the same structure for
   different identifier arguments, but does not allow you to specify a
   domain restriction that will reduce the number of generated columns
   in the matrix.

-  Defined and ``Inline`` variables support an index domain to restrict
   the number of generated columns, but only allow an expression in
   terms of fixed identifiers. Compared to a macro or an ``Inline``
   variable, the number of rows and columns increases for a defined
   variable, but if the variable is referenced more than once in the
   other constraints, it will result in a smaller number of nonzeros.

-  An advantage of variables (both defined and ``Inline``) over macros
   is that their final values are stored by AIMMS, and can be retrieved
   in other execution statements or in the graphical user interface,
   whereas a macro has to be recomputed all the time.