.. _sec:exec.proc:

Procedural and Nonprocedural Execution
======================================

.. rubric:: Execution based on definitions

The definitions specified inside the declarations of sets and parameters
together form a system of functional relationships. As discussed in
:ref:`chap:nonproc` AIMMS automatically determines the dependency
between the identifiers that are used inside these relationships. Based
on the (required) *a-cyclic* dependency structure between identifiers
(see also :ref:`sec:nonproc.dep`), AIMMS knows the exact order in which
identifiers need to be computed. Execution based on definitions is not
controlled by the user, but takes place automatically when values are
needed.

.. rubric:: Execution based on procedures

Procedures are self-contained programs with a body consisting of
execution statements. These statements typically determine the value of
those identifiers which cannot be defined using a single functional
relationship. Execution using procedures proceeds according to the order
of execution statements encountered inside each procedure, and is
therefore controlled by the user.

.. rubric:: Relating definitions and procedures

Whenever a set or a parameter with a definition is used in an execution
statement inside a procedure, and its value is not up-to-date due to
previous data changes, AIMMS will compute its current value just prior
to executing the corresponding statement. This updating facility in
AIMMS forms the necessary and powerful connection between automatic
execution based on definitions and user-initiated execution based on
procedures.

.. rubric:: Definitions and algorithms

Procedural and nonprocedural execution both have their own natural role
in an AIMMS application. Identifier definitions are the most convenient
way to define unique functional relationships between various
identifiers in your model-and keep them up-to-date at all times.
Procedures provide a powerful tool to specify the algorithms that are
needed to compute the identifier values without a direct functional
relationship. Procedural statements are also required to communicate
data between AIMMS and external data sources such as files and
databases.

.. rubric:: Execution statements

AIMMS provides a rich set of execution statements that you can use to
compose your procedures. Available statements include a versatile
assignment statement, statements for data and option management, the
most common flow control statements, calls to other procedures, and a
powerful ``SOLVE`` statement to solve various types of optimization
programs.

.. _statement:

.. rubric:: Syntax

*statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 258.73066 227.2"
	   height="227.2"
	   width="258.73065"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,1480.2666)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 320,9800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,37,976)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/data-initialization-verification-and-control/data-control.html#data-control-statement">data-control-statement</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1620.48,9800 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.48,11000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path30"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 330.082,10400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g32"><text
	           id="text36"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,38.0082,1036)"><tspan
	             id="tspan34"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/flow-control-statements.html#flow-control-statement">flow-control-statement</a></tspan></text>
	</g><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1610.4,10400 50,-20 v 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.48,11000 -20,-50 h 40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 330.02,11000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g44"><text
	           id="text48"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,38.002,1096)"><tspan
	             id="tspan46"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/assignment-statements.html#assignment-statement">assignment-statement</a></tspan></text>
	</g><path
	         id="path50"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1610.46,11000 50,-20 v 40" /><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 496.762,10700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,54.6762,1066)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/optimization-modeling-components/solving-mathematical-programs/the-solve-statement.html#solve-statement">solve-statement</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1443.72,10700 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.48,11000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 473.359,10100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g70"><text
	           id="text74"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,52.3359,1006)"><tspan
	             id="tspan72"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/the-option-and-property-statements.html#option-statement">option-statement</a></tspan></text>
	</g><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1467.12,10100 50,-20 v 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.48,11000 -20,-50 h 40" /><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 540.141,9500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,59.0141,946)"><tspan
	             id="tspan86"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#procedure-call">procedure-call</a></tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1400.34,9500 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.48,11000 -20,-50 h 40" /><path
	         id="path94"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1940.48,11000 -50,20 v -40" /><path
	         id="path96"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,11000 h 120 m 0,0 V 9900 c 0,-55.23 44.773,-100 100,-100 v 0 h 100 v 100 H 1620.45 V 9800 9700 H 320 v 100 m 1300.48,0 h 100 v 0 c 55.23,0 100,44.77 100,100 v 1100 M 120,11000 v -500 c 0,-55.2 44.773,-100 100,-100 h 10.082 100 v 100 H 1610.37 v -100 -100 H 330.082 v 100 m 1280.318,0 h 100 10.08 c 55.23,0 100,44.8 100,100 v 500 M 120,11000 h 100 10.02 100 v 100 h 1280.41 v -100 -100 H 330.02 v 100 m 1280.44,0 h 100 110.02 M 120,11000 v -200 c 0,-55.2 44.773,-100 100,-100 h 176.762 100 v 100 H 1443.7 v -100 -100 H 496.762 v 100 m 946.958,0 h 100 176.76 c 55.23,0 100,44.8 100,100 v 200 M 120,11000 v -800 c 0,-55.2 44.773,-100 100,-100 h 153.359 100 v 100 H 1467.1 v -100 -100 H 473.359 v 100 m 993.761,0 h 100 153.36 c 55.23,0 100,44.8 100,100 v 800 M 120,11000 V 9600 c 0,-55.23 44.773,-100 100,-100 h 220.141 100 v 100 H 1400.32 V 9500 9400 H 540.141 v 100 m 860.199,0 h 100 220.14 c 55.23,0 100,44.77 100,100 v 1400 h 120" /></g></g></svg></div>