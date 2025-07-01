.. _sec:intern.proc:

Internal Procedures
===================

.. rubric:: AIMMS and internal procedures

Internal procedures are pieces of execution code to perform a dedicated
task. For most tasks, and particularly large ones, it is strongly
recommended that you use procedures to break your task into smaller,
purpose-specific tasks. This provides code structure which is easier to
maintain and run. Often it is appropriate to write procedures to obtain
input data from users, databases and files, to execute data consistency
checks, to perform side computations, to solve a mathematical program,
and to create selected reports. Procedures can be called both inside the
model text and inside the graphical user interface.

.. _procedure:

.. rubric:: Declaration and attributes

Procedures are added by inserting a special type of node in the model
tree. The attributes of a ``Procedure`` specify its arguments and
execution code. All possible attributes of a ``Procedure`` node are
given in :ref:`this table <table:intern.attr-proc>`.

.. _table:intern.attr-proc:

.. table:: 

	====================== ==================================================== =======================================
	Attribute              Value-type                                           See also page
	====================== ==================================================== =======================================
	``Arguments``          *argument-list*     
	``Property``           ``UndoSafe``        
	``Uses Runtime libs``  *list of comma-separated runtime libraries prefices* :ref:`rubric:runtime.usesruntimelibs` 
	``Body``               *statements*                                         :ref:`chap:exec`
	``Comment``            *comment string*    
	====================== ==================================================== =======================================
	
.. _procedure.arguments:

.. rubric:: Formal arguments

The arguments of a procedure are given as a parenthesized,
comma-separated list of formal argument names. These argument names are
only the formal identifier names without reference to their index
domains. AIMMS allows formal arguments of the following types:

-  simple sets and relations, and

-  scalar and indexed parameters (either element-valued, string-valued
   or numerical).

The type and dimension of every formal argument is not part of the
argument list, and must be specified as part of the argument's
(mandatory) local declaration in a declaration subnode of the procedure.

.. rubric:: Interactive support

When you add new formal arguments to a procedure in the AIMMS Model
Explorer, AIMMS provides support to automatically add these arguments as
local identifiers to the procedure. For all formal arguments which have
not yet been declared as local identifiers, AIMMS will pop up a dialog
box to let you choose from all supported identifier types. After
finishing the dialog box, all new arguments will be added as (scalar)
local identifiers of the indicated type. When an argument is indexed,
you still need to add the proper ``IndexDomain`` manually in the
attribute form of the argument declaration.

.. rubric:: Range checking

If the declaration of a formal argument of a procedure contains a
numerical range, AIMMS will automatically perform a range check on the
actual arguments based on the specified range of the formal argument.

.. _input:

.. _output:

.. _inout:

.. _optional_inout:

.. rubric:: Input or output

In the declaration of each argument you can specify its type by setting
one of the properties

-  ``Input``,

-  ``Output``,

-  ``InOut`` (default), or

-  ``Optional``.

AIMMS passes the values of any ``Input`` and ``InOut`` arguments when
entering the procedure, and passes back the values of ``Output`` and
``InOut`` arguments. For this reason an actual ``Input`` argument can be
any expression, but actual ``Output`` and ``InOut`` arguments must be
parameter references or set references.

.. rubric:: Optional arguments

An argument can be made optional by setting the property ``Optional`` in
its declaration. Optional arguments are always input, and must be
scalar. When an optional argument is not provided in a procedure call,
AIMMS will pass its default value as specified in its declaration.

.. _procedure.body:

.. rubric:: The ``Body`` attribute

In the ``Body`` attribute you can specify the sequence of AIMMS
execution statements that you want to be executed when the procedure is
run. All statements in the body of a procedure are executed in their
order of appearance.

.. rubric:: Example

The following example illustrates the declaration of a simple procedure
in AIMMS. The body of the procedure has only been outlined.

.. code-block:: aimms

	Procedure ComputeShortestDistance {
	    Arguments  : (City, DistanceMatrix, Distance);
	    Comment    : {
	        "This procedure computes the distance along the shortest path
	        from City to any other city j, given DistanceMatrix."
	    }
	    Body: {
	        Distance(j) := DistanceMatrix(City,j);

	        for ( j | not Distance(j) ) do
	            /*
	             *  Compute the shortest path and the corresponding distance
	             *  for cities j without a direct connection to City.
	             */
	        endfor
	    }
	}

The procedure ``ComputeShortestDistance`` has three formal arguments,
which must be declared in a declaration subnode of the procedure. Their
declarations within this subnode could be as follows.

.. code-block:: aimms

	ElementParameter City {
	    Range        : Cities;
	    Property     : Input;
	}
	Parameter DistanceMatrix {
	    IndexDomain  : (i,j);
	    Property     : Input;
	}
	Parameter Distance {
	    IndexDomain  : j;
	    Property     : Output;
	}

From these declarations (and not from the argument list itself) AIMMS
can deduce that

-  the first actual (input) argument in a call to
   ``ComputeShortestDistance`` must be an element of the (global) set
   ``Cities``,

-  the second (input) argument must be a two-dimensional parameter over
   ``Cities``\ :math:`{}\times{}`\ ``Cities``, and

-  the third (output) arguments must be a one-dimensional parameter over
   ``Cities``.

.. rubric:: Arguments declared over global sets

As in the example above, arguments of procedures can be indexed
identifiers declared over global sets. An advantage is that no local
sets need to be defined. A disadvantage is that the corresponding
procedure is not generic. Procedures with arguments declared over global
sets are preferred when the procedure is uniquely designed for the
application at hand, and direct references to global sets add to the
overall understandability and maintainability.

.. rubric:: Arguments declared over local sets

The index domain or range of a procedure argument need not always be
defined in terms of global sets. Also sets that are declared locally
within the procedure can be used as index domain or range of that
procedure. When a procedure with such arguments is called, AIMMS will
examine the actual arguments, and pass the global domain set to the
local set identifier *by reference*. This allows you to implement
procedures performing generic functionality for which a priori knowledge
of the index domain or range of the arguments is not relevant.

.. rubric:: Local sets are read-only

When you pass arguments defined over local sets, AIMMS does not allow
you to modify the contents of these local sets during the execution of
the procedure. Because such local sets are passed by reference, this
will prevent you from inadvertently modifying the contents of the global
domain sets. When you do want to modify the contents of the global
domain sets, you should pass these sets as explicit arguments as well.

.. rubric:: Unit analysis of arguments

Whenever your model contains one or more ``Quantity`` declarations (see
:ref:`sec:units.quantity`), AIMMS allows you to associate units of
measurements with every argument. Similarly as the index domains of
multidimensional arguments can be expressed either in terms of global
sets, or in terms of local sets that are determined at runtime, the
units of measurements of function and procedure arguments can also be
expressed either in terms of globally defined units, or in terms of
local unit parameters that are determined runtime by AIMMS. The unit
analysis of procedure arguments is discussed in full detail in
:ref:`sec:units.analysis.arg`.

.. rubric:: Local identifiers

Besides the arguments, you can also declare other local scalar or
indexed identifiers in a declaration subnode of a procedure or function
in AIMMS. Local identifiers cannot have a definition, and their scope is
limited to the procedure or function itself.

.. _retainsvalue:

.. rubric:: The property ``RetainsValue``

For each local identifier of a procedure or function that is not a
formal argument, you can specify the option ``RetainsValue``. With it
you can indicate that such a local identifier must retain its last
assigned value between successive calls to that procedure or function.
You can use this feature, for instance, to retain local data that must
be initialized once and can be used during every subsequent call to the
procedure, or to keep track of the number of calls to a procedure.

.. rubric:: Top-down implementation

By partitioning the body of a long procedure into several execution
subnodes, you can effectively implement the procedure in a
self-documenting top-down approach. While the body can just contain the
outermost structure of the procedure's execution, the implementation
details can be hidden behind subnode references with meaningful names.

.. _return:

.. rubric:: The ``RETURN`` statement

In some situations, you may want to return from a procedure or function
before the end of its execution has been reached. You use the ``RETURN``
statement for this purpose. It can be subject to a conditional ``WHEN``
clause similar to the ``SKIP`` and ``BREAK`` statements in loops. The
syntax follows.

.. _return-statement:

.. rubric:: Syntax

*return-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 549.39199 53.866665"
	   height="53.866665"
	   width="549.39197"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,280.26666)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">RETURN</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 652,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 892,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,94.2,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/internal-procedures.html#return-value">return-value</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1632.2,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 772,2000 -20,-50 h 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1752.2,2000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1992.2,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,204.22,196)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">WHEN</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2380.2,2000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2500.2,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,255.02,196)"><tspan
	             id="tspan52"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/logical-expressions.html#logical-expression">logical-expression</a></tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3560.44,2000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1872.2,2000 -20,-50 h 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3680.44,2000 -20,-50 h 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3800.44,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,386.444,196)"><tspan
	             id="tspan66"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4000.44,2000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4120.44,2000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 v 0 c 0,55.23 44.773,100 100,100 h 332 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 220 c -55.227,0 -100,44.77 -100,100 v 0 m 532,0 h 120 m 0,0 v 0 h 120 v 100 h 740.18 V 2000 1900 H 892 v 100 m 740.2,0 h 120 m -980.2,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 330.1 120 330.1 c 55.23,0 100,44.77 100,100 v 200 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 188 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -188 c -55.23,0 -100,44.77 -100,100 v 0 m 388,0 h 120 v 100 H 3560.41 V 2000 1900 H 2500.2 v 100 m 1060.24,0 h 120 m -1808.24,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 744.12 120 744.12 c 55.22,0 100,44.77 100,100 v 200 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. rubric:: Return value
   :name: proc.ret-val.decl

.. _return-value:

Procedures in AIMMS can have an (integer) return value, which you can
pass by means of the ``RETURN`` statement. You can use the return value
only in a limited sense: you can assign it to a scalar parameter, or use
it in a logical condition in, for instance, an ``IF`` statement. You
cannot use the return value in a compound numerical expression. For more
details, refer to :ref:`sec:intern.ref`.

.. _attr:undosafe:

.. _procedure.property:

.. rubric:: The ``Property`` attribute

In the ``Property`` attribute of internal procedures you can specify a
single property, ``UndoSafe``. With the ``UndoSafe`` property you can
indicate that the procedure, when called from a page within the
graphical end-user interface of a model, should leave the stack of
end-user undo actions intact. Normally, procedure calls made from within
the end-user interface will clear the undo stack, because such calls
usually make additional modifications to (global) data based on end-user
edits.

.. _procedure.usesruntimelibs:

.. rubric:: The ``Uses Runtime libs`` attribute

This attribute is available for non-predefined procedures.
It is a comma-separated list of prefices of runtime 
libraries, identifiers from which are used in the body of the procedure.
For more information please refer to the section 
:ref:`sec:module.runtime` and in particular rubric 
:ref:`rubric:runtime.usesruntimelibs`

.. rubric:: Procedures summarized

The following list summarizes the main characteristics of AIMMS
procedures.

-  The arguments of a procedure can be sets, set elements and
   parameters.

-  The arguments, together with their attributes, must be declared in a
   local declaration subnode.

-  The domain and range of indexed arguments can be in terms of either
   global or local sets.

-  Each argument is of type ``Input``, ``Output``, ``Optional`` or
   ``InOut`` (default).

-  Optional arguments must be scalar, and you must specify a default
   value. Optional arguments are always of type ``Input``.

-  AIMMS performs range checking on the actual arguments at runtime,
   based on the specified range of the formal arguments.
