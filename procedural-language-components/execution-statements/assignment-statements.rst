.. _sec:exec.assign:

Assignment Statements
=====================

.. rubric:: Assignment

Assignment statements are used to set or change the values of sets,
parameters and variables during the execution of a procedure or a
function. The syntax of an assignment statement is straightforward.

.. _assignment-statement:

.. rubric:: Syntax

*assignment-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 470.34667 27.199999"
	   height="27.199999"
	   width="470.34665"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,146.93333)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/assignment-statements.html#data-selection">data-selection</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 967,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1087,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,113.7,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/assignment-statements.html#assignment-operator">assignment-operator</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2287.4,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2407.4,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,245.74,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3087.6,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3207.6,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,327.16,96)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3407.6,1000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3527.6,1000 -50,20 v -40" /><path
	         id="path56"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 v 100 H 966.98 V 1000 900 H 120 v 100 m 847,0 h 120 v 100 H 2287.37 V 1000 900 H 1087 v 100 m 1200.4,0 h 120 v 100 h 680.19 V 1000 900 H 2407.4 v 100 m 680.2,0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.773 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. _data-selection:

*data-selection:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 394.73601 53.866665"
	   height="53.866665"
	   width="394.73599"
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
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#identifier-part">identifier-part</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 920.199,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1160.2,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,122.42,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1360.2,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1480.2,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,153.02,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-domain">binding-domain</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2400.52,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2520.52,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,258.452,196)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2720.52,2000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1040.2,2000 -20,-50 h 40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2840.52,2000 -20,-50 h 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2960.52,2000 -50,20 v -40" /><path
	         id="path60"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 v 100 H 920.172 V 2000 1900 H 120 v 100 m 800.199,0 H 1040.2 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 920.29 V 2000 1900 H 1480.2 v 100 m 920.32,0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 m -1800.32,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 740.16 120 740.16 c 55.23,0 100,44.77 100,100 v 200 h 120" /></g></g></svg></div>

.. _assignment-operator:

.. rubric:: Assignment operators

AIMMS offers several assignment operators. The standard *replacement*
assignment operator ``:=`` replaces the value of all elements specified
on the left hand side with the value of the expression on the right hand
side. The *arithmetic* assignment operators ``+=``, ``-=``, ``*=``,
``/=`` and ``^=`` combine an assignment with an arithmetic operation.
Thus, the assignments

   ``a += b``, ``a -= b``, ``a *= b``, ``a /= b``, ``a ^= b``

form a shorthand notation for the assignments

   ``a := a + b``, ``a := a - b``, ``a := a * b``, ``a := a / b``, ``a := a ^ b``.

.. rubric:: Index binding

Assignment is an *index binding* statement. AIMMS also binds unbound
indices in (nested) references to element-valued parameters that are
used for indexing the left-hand side. AIMMS will execute the assignment
repeatedly for *all* elements in the binding domain, and in the order as
specified by the declaration(s) of the binding set(s). The precise rules
for index binding are explained in :ref:`sec:bind.rules`.

.. rubric:: Allowed binding domains

In contrast to the binding domain of iterative operators and the ``FOR``
statements, the binding domain of an indexed assignment can contain the
full range of element expressions:

-  references to unbound indices, which will be bound by the assignment,

-  references to scalar element parameters and bound indices,

-  references to indexed element parameters, for which any nested
   unbound index will be bound as well,

-  calls to element-valued functions, and

-  element-valued iterative operators.

If the element expression inside the binding domain of an indexed
assignment is too lengthy, it may be better to use an intermediate
element parameter to improve readability.

.. rubric:: Conditional assignments

Like any binding domain, the binding domain of an indexed assignment can
be subject to a logical condition. Such an assignment is referred to as
a *conditional assignment*, and is only executed for those elements in
the binding domain that satisfy the logical condition.

.. rubric:: Domain checking

In addition, if the identifier on the left-hand side of the assignment
has its own domain restriction, then the assignment is limited to those
elements of the binding domain that satisfy this restriction.
Assignments to elements outside the restricted domain are not
considered.

.. rubric:: Example

The following five examples illustrate some simple assignment
statements. In all examples we assume that ``i`` and ``j`` are unbound
indices into a set ``Cities``, and that ``LargestCity`` is an element
parameter into ``Cities``.

#. The first example illustrates a simple *scalar assignment*.

   .. code-block:: aimms
   
   	TotalTransportCost := sum[(i,j), UnitTransportCost(i,j)*Transport(i,j)];

   The value of the scalar identifier on the left-hand side is replaced
   with the value of the expression on the right-hand side.

#. The second example illustrates an *index binding assignment*.

   .. code-block:: aimms
   
   	UnitTransportCost(i,j) *= CostWeightFactor(i,j) ;

   For *all* cities ``i`` and ``j`` in the index domain of
   ``UnitTransportCost`` , the old values of the identifier
   ``UnitTransportCost(i,j)`` are multiplied with the values of the
   identifier ``CostWeightFactor(i,j)`` and then used to replace the old
   values.

#. The third example illustrates a *conditional assignment*.

   .. code-block:: aimms
   
   	Transport((i,j) | UnitTransportCost(i,j) > 100) := 0;

   The zero assignment to ``Transport`` is made to only those cities
   ``i`` and ``j`` for which the ``UnitTransportCost`` is too high.

#. The fourth example illustrates a *sliced assignment*, i.e. an
   assignment that only changes the values of a lower-dimensional
   subspace of the index domain of the left-hand side identifier.

   .. code-block:: aimms
   
   	Transport(LargestCity,j) := 0;

   The sliced assignment in this example binds only the index ``j``. The
   values of the parameter ``Transport`` are set to zero from the city
   ``LargestCity`` to *every* city ``j``, but the values from every
   other city *i* to all cities ``j`` remain unchanged.

#. The fifth example illustrates a *nested index binding statement*.

   .. code-block:: aimms
   
   	PreviousCity( NextCity(i) ) := i;

   The index ``i`` is bound, because it is used in the nested reference
   of the element parameter ``NextCity(i)``, which in turn is used for
   indexing the identifier ``PreviousCity``. Note that, in a tour, city
   ``i`` by definition is the previous city of the specific (next) city
   it is linked with.

.. rubric:: Sequential execution

Indexed assignments are executed in a sequential manner, i.e. as if it
was replaced by a sequence of individual assignments to every element in
the binding domain. Thus, if ``Periods`` is the integer set ``{0 .. 3}``
with index ``t``, then the indexed assignment

.. code-block:: aimms

	Stock( t | t > 0 ) := Stock(t-1) + Supply(t) - Demand(t);

is executed (conceptually) as the sequence of individual statements

.. code-block:: aimms

	Stock(1) := Stock(0) + Supply(1) - Demand(1);
	Stock(2) := Stock(1) + Supply(2) - Demand(2);
	Stock(3) := Stock(2) + Supply(3) - Demand(3);

Therefore, in the right hand side expression it is possible to refer to
elements of the identifier on the left which have received their value
prior to the execution of the current individual assignment. This type
of behavior is typically observed and wanted in stock balance type
applications which use lag references as shown above. The same argument
also applies to assignments that use element parameters for indexing on
either the left- or right-hand side of the assignment.

.. rubric:: Indexed assignment versus ``FOR``

In addition to the indexed assignment, AIMMS also possesses a more
general ``FOR`` statement which repeatedly executes a group of
statements for all elements in its binding domain (see also
:ref:`sec:exec.flow.for`). If you are familiar with programming
languages like ``C`` or PASCAL you might be tempted to embed every
indexed assignment into one or more ``FOR`` statements with the proper
domain. Although this will conceptually produce the same results, we
strongly recommend against it for two reasons.

-  By omitting the ``FOR`` statements you improve to the readability and
   maintainability of your model code.

-  By including the ``FOR`` statement unnecessarily you are effectively
   degrading the performance of your model, because AIMMS can execute an
   indexed assignment much more efficiently than the equivalent ``FOR``
   statement.

Whenever you use a ``FOR`` statement unnecessarily, AIMMS will produce a
compile time warning to tell you that the code would be more efficient
by removing the ``FOR`` statement.

.. rubric:: Example

Consider the indexed assignment

   .. code-block:: aimms
   
   	Transport((i,j) | UnitTransportCost(i,j) > 100) := 0;

and the equivalent ``FOR`` statement

.. code-block:: aimms

	for ((i,j) | UnitTransportCost(i,j) > 100) do
	    Transport(i,j) := 0;
	endfor;

Notice that the indexed assignment is more compact than the ``FOR``
statement and is easier to read. In this example AIMMS will warn against
this use of the ``FOR`` statement, because it can be removed without any
change in semantics, and will lead to more efficient execution.

.. rubric:: Undefined left-hand references

When there are undefined references with lag and lead operators on the
left-hand side of an assignment (i.e. references that evaluate to the
empty element), the corresponding assignments will be skipped. The same
is true if the identifier on the left contains undefined references to
element parameters. Notice that this behavior is different from the
behavior of a reference containing undefined lag and lead expressions on
the right-hand side of an assignment. These evaluate to zero.

.. rubric:: Example

Consider the assignment to the parameter ``Stock`` above. It could also
have been written as

.. code-block:: aimms

	Stock(t+1) := Stock(t) + Supply(t+1) - Demand(t+1);

In this case, there is no need to add a condition to the assignment for
``t``\ :math:`{}=3`. The reference to ``t+1`` is undefined, and hence
the assignment will be skipped. Similarly, the assignment

.. code-block:: aimms

	PreviousCity( NextCity(i) ) := i;

will only be executed for those cities ``i`` for which ``NextCity(i)``
is defined.