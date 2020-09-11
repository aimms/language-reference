.. _sec:exec.option:

.. _sec:exec.property:

The ``OPTION`` and ``PROPERTY`` Statements
==========================================

.. _option:

.. _property:

.. rubric:: Options

Options are directives to AIMMS or to the solvers to execute a task in a
particular manner. Options have a name and can assume a value that is
either numeric or string-valued. You can modify the value of an option
from within the graphical interface. The assigned value is stored along
with the project. All global options are set to their stored values at
the beginning of each session. During execution you can change option
settings using the ``OPTION`` statement.

.. _option-statement:

.. rubric:: Syntax

*option-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 384.41066 67.199997"
	   height="67.199997"
	   width="384.41064"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,186.93333)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,15,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">OPTION</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 632,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 832,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,88.2,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/the-option-and-property-statements.html#option">option</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1258.88,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1358.88,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,140.888,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">:=</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1602.88,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1702.88,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,175.288,96)"><tspan
	             id="tspan48"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2383.08,1000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 732,1000 20,50 h -40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1507.54,1300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g58"><text
	           id="text62"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,157.154,126)"><tspan
	             id="tspan60"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1707.54,1300 50,-20 v 40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2483.08,1000 20,50 h -40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2583.08,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g70"><text
	           id="text74"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,264.708,96)"><tspan
	             id="tspan72"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2783.08,1000 50,-20 v 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2883.08,1000 -50,20 v -40" /><path
	         id="path80"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 100 v 0 c 0,55.23 44.773,100 100,100 h 332 c 55.227,0 100,-44.77 100,-100 v 0 0 C 632,944.773 587.227,900 532,900 H 200 c -55.227,0 -100,44.773 -100,100 v 0 m 532,0 h 100 m 0,0 v 0 h 100 v 100 h 426.87 V 1000 900 H 832 v 100 m 426.88,0 h 100 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.773 -100,100 v 0 m 244,0 h 100 v 100 h 680.19 V 1000 900 h -680.19 v 100 m 680.2,0 h 100 M 732,1000 v 200 c 0,55.23 44.773,100 100,100 h 575.54 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 575.54 c 55.22,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.773 -100,100 v 0 m 200,0 h 100" /></g></g></svg></div>

You can find a complete list of global options for AIMMS and its solvers
in the help system.

.. rubric:: Option values

The right-hand side of an ``OPTION`` statement must be a scalar
expression of the proper type. If the option expects a string value,
AIMMS will accept both string- or element-valued expressions. An example
follows.

.. code-block:: aimms

	option  Bound_Tolerance  := 1.0e-6,
	        Iteration_Limit  := UserSettings('IterationLimit');

.. rubric:: Solver options

Some solver options are available for more than one solver. If you
modify such a solver option per se, AIMMS will modify the option for all
solver that support it. If you want to restrict the change to only a
single solver, you can prefix the option name by the name of the solver
followed by a dot ``.``, as illustrated in the example below.

.. code-block:: aimms

	option  'Cplex 12.9'.lp_method := 'dual simplex';

This statement will set the option ``lp_method`` of the solver that is
known to the system as ``'Cplex 12.9'`` equal to ``'dual simplex'``. The
solver name can be either a quoted solver name, or an element parameter
into the predefined set :any:`AllSolvers`.

.. rubric:: Identifier properties

Identifier properties can be turned ``on`` or ``off``. All properties
default to ``off``, unless they are turned on-either in the declaration
of the identifier or in a ``PROPERTY`` statement. During the execution
of your model you can dynamically change the default values of
properties through the ``PROPERTY`` execution statements.

.. _property-statement:

.. rubric:: Syntax

*property-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 541.0187 107.2"
	   height="107.2"
	   width="541.01868"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,453.59999)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,15,296)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">PROPERTY</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 776,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 976,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,102.6,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1529.48,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1629.48,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,169.348,296)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">.</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1829.48,3000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1929.48,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,197.948,296)"><tspan
	             id="tspan48"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-declaration/set-declaration-and-attributes.html#property">property</a></tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2469.64,3000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2569.64,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,261.964,296)"><tspan
	             id="tspan58"
	             y="0"
	             x="0">:=</tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2813.64,3000 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2913.64,3000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3113.64,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g68"><text
	           id="text72"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,316.364,266)"><tspan
	             id="tspan70"
	             y="0"
	             x="0">on</tspan></text>
	</g><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3357.64,2700 50,-20 v 40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3557.64,3000 -20,-50 h 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3077.64,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g80"><text
	           id="text84"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,312.764,296)"><tspan
	             id="tspan82"
	             y="0"
	             x="0">off</tspan></text>
	</g><path
	         id="path86"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3393.64,3000 50,-20 v 40" /><path
	         id="path88"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 876,3000 20,50 h -40" /><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2166.82,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g92"><text
	           id="text96"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,223.082,326)"><tspan
	             id="tspan94"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path98"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2366.82,3300 50,-20 v 40" /><path
	         id="path100"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3657.64,3000 20,50 h -40" /><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3757.64,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g104"><text
	           id="text108"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,382.164,296)"><tspan
	             id="tspan106"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path110"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3957.64,3000 50,-20 v 40" /><path
	         id="path112"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4057.64,3000 -50,20 v -40" /><path
	         id="path114"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 100 v 0 c 0,55.23 44.773,100 100,100 h 476 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 200 c -55.227,0 -100,44.77 -100,100 v 0 m 676,0 h 100 m 0,0 v 0 h 100 v 100 h 553.46 V 3000 2900 H 976 v 100 m 553.48,0 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 v 100 h 540.15 v -100 -100 h -540.15 v 100 m 540.16,0 h 100 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 100 m 0,0 v -200 c 0,-55.23 44.77,-100 100,-100 v 0 h 100 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 100 v 0 c 55.23,0 100,44.77 100,100 v 200 m -644,0 h 100 -36 100 v 0 c 0,55.23 44.77,100 100,100 h 116 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -116 c -55.23,0 -100,44.77 -100,100 v 0 m 316,0 h 100 64 100 M 876,3000 v 200 c 0,55.23 44.773,100 100,100 h 1090.82 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 1090.82 c 55.23,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100" /></g></g></svg></div>

.. rubric:: Resetting properties

The properties of all identifier types can be found in the identifier
declaration sections. Not all property settings can be changed, e.g. you
cannot dynamically change the ``Input`` or ``Output`` property of
arguments of functions and procedures. In such cases, AIMMS will produce
a runtime error. An example of the ``PROPERTY`` statement follows.

.. code-block:: aimms

	if ( Card(Cities) > 100 ) then
	   property IntermediateTransport.NoSave := on;
	endif;

Once the set of ``Cities`` contains more than 100 elements, the
identifier ``IntermediateTransport`` is no longer saved as part of a
case file.

.. rubric:: Multiple identifiers

When the ``PROPERTY`` statement is applied to an index into a subset of
the predefined set :any:`AllIdentifiers`, AIMMS will change the
corresponding property for all identifiers in that subset.

.. rubric:: Example

The following example illustrates how the ``PROPERTY`` statement can be
used to obtain additional sensitivity data for a set
``SensitivityVariables`` of (symbolic) variables that has been
previously determined.

.. code-block:: aimms

	for ( var in SensitivityVariables ) do
	    property var.CoefficientRanges := on;
	endfor;

Here, you request AIMMS to determine the smallest and largest values for
the objective coefficient of each variable in ``SensitivityVariables``
during the execution of a ``SOLVE`` statement such that the optimal
basis remains constant (see also :ref:`sec:var.properties`).