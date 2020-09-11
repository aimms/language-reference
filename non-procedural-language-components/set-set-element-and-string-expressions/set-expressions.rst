.. _sec:set-expr.set:

Set Expressions
===============

.. rubric:: Set expressions

Set expressions play an important role in the construction of index
domains of indexed identifiers, as well as in constructing the domain of
execution of particular indexed statements. The AIMMS language offers a
powerful set of set expressions, allowing you to express complex set
constructs in a clear and concise manner.

.. rubric:: Constant set expressions

A set expression is evaluated to yield the value of a set. As with all
expressions in AIMMS, set expressions come in two forms, *constant* and
*symbolic*. Constant set expressions refer to explicit set elements
directly, and are mainly intended for set initialization. The tabular
format of set initialization is treated in :ref:`sec:text.table`.

.. rubric:: Symbolic set expressions

Symbolic set expressions are formulas that can be executed to result in
a set. The contents of this set can vary throughout the execution of
your model depending on the values of the other model identifiers
referenced inside the symbolic formulas. Symbolic set expressions are
typically used for specifying index domains. In this section various
forms of set expressions will be treated.

.. _set-primary:

.. rubric:: Syntax

*set-primary:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 301.36534 267.19997"
	   height="267.19998"
	   width="301.36533"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,1746.9333)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,13000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 370,11200 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,43.4,1116)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 570,11200 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 690,11200 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,74,1116)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-expression">set-expression</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1570.24,11200 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1690.24,11200 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,175.424,1116)"><tspan
	             id="tspan40"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1890.24,11200 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2110.24,13000 -20,-50 h 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 826.68,13000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,87.668,1296)"><tspan
	             id="tspan52"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#reference">reference</a></tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1433.56,13000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,13000 -20,-50 h 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 659.941,12400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g62"><text
	           id="text66"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,70.9941,1236)"><tspan
	             id="tspan64"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#enumerated-set">enumerated-set</a></tspan></text>
	</g><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1600.3,12400 50,-20 v 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2110.24,13000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,13000 -20,-50 h 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 669.961,12100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g76"><text
	           id="text80"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,71.9961,1206)"><tspan
	             id="tspan78"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#constructed-set">constructed-set</a></tspan></text>
	</g><path
	         id="path82"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1590.28,12100 50,-20 v 40" /><path
	         id="path84"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2110.24,13000 -20,-50 h 40" /><path
	         id="path86"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,13000 -20,-50 h 40" /><path
	         id="path88"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 559.98,11800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g90"><text
	           id="text94"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,60.998,1176)"><tspan
	             id="tspan92"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#iterative-expression">iterative-expression</a></tspan></text>
	</g><path
	         id="path96"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.26,11800 50,-20 v 40" /><path
	         id="path98"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2110.24,13000 -20,-50 h 40" /><path
	         id="path100"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,13000 -20,-50 h 40" /><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 760.02,11500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g104"><text
	           id="text108"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,81.002,1146)"><tspan
	             id="tspan106"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#function-call">function-call</a></tspan></text>
	</g><path
	         id="path110"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1500.22,11500 50,-20 v 40" /><path
	         id="path112"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2110.24,13000 -20,-50 h 40" /><path
	         id="path114"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,13000 -20,-50 h 40" /><path
	         id="path116"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 556.621,12700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g118"><text
	           id="text122"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,60.6621,1266)"><tspan
	             id="tspan120"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path124"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1703.62,12700 50,-20 v 40" /><path
	         id="path126"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2110.24,13000 -20,-50 h 40" /><path
	         id="path128"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2260.24,13000 -50,20 v -40" /><path
	         id="path130"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,13000 h 150 m 0,0 v -1700 c 0,-55.2 44.773,-100 100,-100 v 0 h 120 v 0 c 0,55.2 44.773,100 100,100 v 0 c 55.227,0 100,-44.8 100,-100 v 0 0 c 0,-55.2 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.8 -100,100 v 0 m 200,0 h 120 v 100 h 880.22 v -100 -100 H 690 v 100 m 880.24,0 h 120 v 0 c 0,55.2 44.77,100 100,100 v 0 c 55.22,0 100,-44.8 100,-100 v 0 0 c 0,-55.2 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.8 -100,100 v 0 m 200,0 h 120 v 0 c 55.22,0 100,44.8 100,100 v 1700 M 150,13000 h 100 456.68 120 v 100 h 606.87 v -100 -100 H 826.68 v 100 m 606.88,0 h 120 556.68 M 150,13000 v -500 c 0,-55.2 44.773,-100 100,-100 h 289.941 120 v 100 h 940.339 v -100 -100 H 659.941 v 100 m 940.359,0 h 120 289.94 c 55.23,0 100,44.8 100,100 v 500 M 150,13000 v -800 c 0,-55.2 44.773,-100 100,-100 h 299.961 120 v 100 h 920.309 v -100 -100 H 669.961 v 100 m 920.319,0 h 120 299.96 c 55.22,0 100,44.8 100,100 v 800 M 150,13000 v -1100 c 0,-55.2 44.773,-100 100,-100 h 189.98 120 v 100 h 1140.25 v -100 -100 H 559.98 v 100 m 1140.28,0 h 120 189.98 c 55.22,0 100,44.8 100,100 v 1100 M 150,13000 v -1400 c 0,-55.2 44.773,-100 100,-100 h 390.02 120 v 100 h 740.18 v -100 -100 H 760.02 v 100 m 740.2,0 h 120 390.02 c 55.22,0 100,44.8 100,100 v 1400 M 150,13000 v -200 c 0,-55.2 44.773,-100 100,-100 h 186.621 120 v 100 H 1703.59 v -100 -100 H 556.621 v 100 m 1146.999,0 h 120 186.62 c 55.23,0 100,44.8 100,100 v 200 h 150" /></g></g></svg></div>

.. _set-expression:

*set-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 254.272 67.199997"
	   height="67.199997"
	   width="254.27199"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,413.59999)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,3000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 370,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,42,266)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#operator-expression">operator-expression</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1537.04,2700 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1757.04,3000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 603.52,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,65.352,296)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-primary">set-primary</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1303.52,3000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1907.04,3000 -50,20 v -40" /><path
	         id="path40"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 150 m 0,0 v -200 c 0,-55.23 44.773,-100 100,-100 v 0 h 120 v 100 H 1537.01 V 2700 2600 H 370 v 100 m 1167.04,0 h 120 v 0 c 55.23,0 100,44.77 100,100 v 200 M 150,3000 h 100 233.52 120 v 100 H 1303.5 V 3000 2900 H 603.52 v 100 m 700,0 h 120 333.52 150" /></g></g></svg></div>

.. rubric:: Set references

The simplest form of set expression is the reference to a set. The
reference can be scalar or indexed, and evaluates to the current
contents of that set.

.. _sec:set-expr.set.enum:

Enumerated Sets
---------------

.. rubric:: Enumerated sets

An *enumerated* set is a set defined by an explicit enumeration of its
elements. Such an enumeration includes literal elements, set element
expressions, and (constant or symbolic) element ranges. An enumerated
set can be either a simple or a relation. If you use an *integer element
range*, an integer set will result.

.. rubric:: Constant enumerated sets

Enumerated sets come in two flavors: *constant* and *symbolic*. Constant
enumerated sets are preceded by the keyword ``DATA``, and must only
contain literal set elements. These set elements do not have to be
contained in single quotes unless they contain characters other than the
alpha-numeric characters, the underscore, the plus or the minus sign.

.. rubric:: Example
   :name: examp:set-expr.cities

The following simple set and relation assignments illustrate constant
enumerated set expressions.

.. code-block:: aimms

	Cities := DATA { Amsterdam, Rotterdam, 'The Hague', London, Paris, Berlin, Madrid } ;

	DutchRoutes := DATA { (Amsterdam, Rotterdam  ), (Amsterdam, 'The Hague'),
	                      (Rotterdam, Amsterdam  ), (Rotterdam, 'The Hague') } ;

.. rubric:: Symbolic enumerated sets

Any enumerated set not preceded by the keyword ``DATA`` is considered
symbolic. Symbolic enumerated sets can also contain element parameters.
In order to distinguish between literal set elements and element
parameters, all literal elements inside symbolic enumerated sets must be
quoted.

.. rubric:: Examples

The following two set assignments illustrate the use of enumerated sets
that depend on the value of the element parameters ``SmallestCity``,
``LargestCity`` and ``AirportCity``.

.. code-block:: aimms

	ExtremeCities := { SmallestCity, LargestCity } ;

	Routes        := { (LargestCity, SmallestCity), (AirportCity, LargestCity )  } ;

The following two set assignments contrast the semantics between
constant and symbolic enumerated sets.

.. code-block:: aimms

	SillyExtremes := DATA { SmallestCity, LargestCity } ;
	! contents equals { 'SmallestCity', 'LargestCity' }

	ExtremeCities := { SmallestCity, LargestCity, 'Amsterdam' };
	! contents equals e.g. { 'The Hague', 'London', 'Amsterdam' }

The syntax of enumerated set expressions is as follows.

.. _enumerated-set:

.. rubric:: Syntax

*enumerated-set:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 379.32802 93.866661"
	   height="93.866661"
	   width="379.328"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,320.26666)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 270,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,32,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">DATA</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 658,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 150,2000 -20,-50 h 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 778,2000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 928,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,99.2,196)"><tspan
	             id="tspan32"
	             y="0"
	             x="0">{</tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1128,2000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1398,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,144.8,196)"><tspan
	             id="tspan42"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#element-tuple">element-tuple</a></tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2224.96,2000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1278,2000 20,50 h -40" /><path
	         id="path50"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1711.48,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g52"><text
	           id="text56"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,177.548,226)"><tspan
	             id="tspan54"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1911.48,2300 50,-20 v 40" /><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2344.96,2000 20,50 h -40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2494.96,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,255.896,196)"><tspan
	             id="tspan66"
	             y="0"
	             x="0">}</tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2694.96,2000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2844.96,2000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 150 m 0,0 v 0 h 120 v 0 c 0,55.23 44.773,100 100,100 h 188 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 370 c -55.227,0 -100,44.77 -100,100 v 0 m 388,0 h 120 m -628,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 154 120 154 c 55.227,0 100,44.77 100,100 v 200 h 150 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 150 m 0,0 v 0 h 120 v 100 h 826.94 V 2000 1900 H 1398 v 100 m 826.96,0 h 120 M 1278,2000 v 200 c 0,55.23 44.77,100 100,100 h 213.48 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 213.48 c 55.23,0 100,-44.77 100,-100 v -200 h 150 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 150" /></g></g></svg></div>

.. _element-tuple:

*element-tuple:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 297.83467 147.19999"
	   height="147.2"
	   width="297.83466"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,946.93331)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 80,7000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 260,6100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,32.4,606)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 460,6100 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 620,6100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67,606)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#tuple-component">tuple-component</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1613.76,6100 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 540,6100 20,50 h -40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1016.88,6400 -50.001,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,108.088,636)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1216.88,6400 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1693.76,6100 20,50 h -40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1773.76,6100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g52"><text
	           id="text56"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,183.776,606)"><tspan
	             id="tspan54"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1973.76,6100 50,-20 v 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2153.76,7000 -20,-50 h 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 543.379,7000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,59.3379,696)"><tspan
	             id="tspan66"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1690.38,7000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 80,7000 -20,-50 h 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 680.059,6700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g76"><text
	           id="text80"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,73.0059,666)"><tspan
	             id="tspan78"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#element-range">element-range</a></tspan></text>
	</g><path
	         id="path82"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1553.7,6700 50,-20 v 40" /><path
	         id="path84"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2153.76,7000 -20,-50 h 40" /><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2233.76,7000 -50,20 v -40" /><path
	         id="path88"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,7000 h 80 m 0,0 v -800 c 0,-55.23 44.773,-100 100,-100 v 0 h 80 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 80 m 0,0 v 0 h 80 v 100 h 993.74 V 6100 6000 H 620 v 100 m 993.76,0 h 80 M 540,6100 v 200 c 0,55.23 44.773,100 100,100 h 296.879 80.001 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 80 296.88 c 55.22,0 100,-44.77 100,-100 v -200 h 80 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 80 v 0 c 55.22,0 100,44.77 100,100 v 800 M 80,7000 h 100 283.379 80 v 100 H 1690.35 V 7000 6900 H 543.379 v 100 m 1147.001,0 h 80 383.38 M 80,7000 v -200 c 0,-55.23 44.773,-100 100,-100 h 420.059 80 v 100 H 1553.68 V 6700 6600 H 680.059 v 100 m 873.641,0 h 80 420.06 c 55.22,0 100,44.77 100,100 v 200 h 80" /></g></g></svg></div>

.. _tuple-component:

*tuple-component:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 318.26667 147.2"
	   height="147.2"
	   width="318.26666"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,813.59998)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 80,6000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 260,5100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,32.4,506)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">[</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 460,5100 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 620,5100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67,506)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1767,5100 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 540,5100 20,50 h -40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1093.5,5400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,115.75,536)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1293.5,5400 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1847,5100 20,50 h -40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1927,5100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g52"><text
	           id="text56"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,199.1,506)"><tspan
	             id="tspan54"
	             y="0"
	             x="0">]</tspan></text>
	</g><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2127,5100 50,-20 v 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2307,6000 -20,-50 h 40" /><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 80,6000 -20,-50 h 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 756.68,5700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g66"><text
	           id="text70"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,80.668,566)"><tspan
	             id="tspan68"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#element-range">element-range</a></tspan></text>
	</g><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1630.32,5700 50,-20 v 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2307,6000 -20,-50 h 40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 620,6000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g78"><text
	           id="text82"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67,596)"><tspan
	             id="tspan80"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path84"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1767,6000 50,-20 v 40" /><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2387,6000 -50,20 v -40" /><path
	         id="path88"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,6000 h 80 m 0,0 v -800 c 0,-55.23 44.773,-100 100,-100 v 0 h 80 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 80 m 0,0 v 0 h 80 v 100 H 1766.97 V 5100 5000 H 620 v 100 m 1147,0 h 80 m -1307,0 v 200 c 0,55.23 44.773,100 100,100 h 373.5 80 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 80 373.5 c 55.23,0 100,-44.77 100,-100 v -200 h 80 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 80 v 0 c 55.23,0 100,44.77 100,100 v 800 m -2227,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 496.68 80 v 100 H 1630.3 V 5700 5600 H 756.68 v 100 m 873.64,0 h 80 496.68 c 55.23,0 100,44.77 100,100 v 200 m -2227,0 h 100 360 80 v 100 H 1766.97 V 6000 5900 H 620 v 100 m 1147,0 h 80 460 80" /></g></g></svg></div>

All elements in an enumerated set must have the same dimension.

.. rubric:: Element range

By using the ``..`` operator, you can specify an *element range*. An
element range is a sequence of consecutively numbered elements. The
following set assignments illustrate both constant and symbolic element
ranges. Their difference is explained below.

.. code-block:: aimms

	NodeSet       := DATA { node1 .. node100 } ;

	FirstNode     := 1;
	LastNode      := 100;

	IntegerNodes  := { FirstNode .. LastNode } ;

The syntax of element ranges is as follows.

.. _element-range:

.. rubric:: Syntax

*element-range:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 566.53866 53.866665"
	   height="53.866665"
	   width="566.53864"
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
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#range-bound">range-bound</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 900.398,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1020.4,2000 -50.002,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,107.04,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">..</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1264.4,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1384.4,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,143.44,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#range-bound">range-bound</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2164.8,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2404.8,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,245.48,196)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">BY</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2648.8,2000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2768.8,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,281.88,196)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4009.04,2000 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2284.8,2000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4129.04,2000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4249.04,2000 -50,20 v -40" /><path
	         id="path70"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 v 100 H 900.383 V 2000 1900 H 120 v 100 m 780.398,0 H 1020.4 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 v 100 h 780.38 V 2000 1900 H 1384.4 v 100 m 780.4,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 v 100 H 4009 V 2000 1900 H 2768.8 v 100 m 1240.24,0 h 120 m -1844.24,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 762.12 120 762.12 c 55.22,0 100,44.77 100,100 v 200 h 120" /></g></g></svg></div>

.. _range-bound:

*range-bound:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 423.16801 107.2"
	   height="107.2"
	   width="423.168"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,680.26665)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 360,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,41,496)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#prefix-string">prefix-string</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1086.76,5000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 240,5000 -20,-50 h 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1206.76,5000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1326.76,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,137.676,496)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#integer">integer</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1793.6,5000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2033.6,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,208.36,496)"><tspan
	             id="tspan42"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#postfix-string">postfix-string</a></tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2813.76,5000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1913.6,5000 -20,-50 h 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2933.76,5000 -20,-50 h 40" /><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,5000 -20,-50 h 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 966.762,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,101.676,436)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2207,4400 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3053.76,5000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3173.76,5000 -50,20 v -40" /><path
	         id="path68"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5000 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 726.74 V 5000 4900 H 360 v 100 m 726.76,0 h 120 M 240,5000 v -200 c 0,-55.23 44.773,-100 100,-100 h 323.379 120 323.381 c 55.23,0 100,44.77 100,100 v 200 h 120 v 100 h 466.83 v -100 -100 h -466.83 v 100 m 466.84,0 h 120 m 0,0 v 0 h 120 v 100 h 780.14 V 5000 4900 H 2033.6 v 100 m 780.16,0 h 120 m -1020.16,0 v -200 c 0,-55.23 44.78,-100 100,-100 h 350.08 120 350.08 c 55.23,0 100,44.77 100,100 v 200 h 120 M 120,5000 v -500 c 0,-55.23 44.773,-100 100,-100 h 626.762 120 v 100 H 2206.97 V 4400 4300 H 966.762 v 100 M 2207,4400 h 120 626.76 c 55.23,0 100,44.77 100,100 v 500 h 120" /></g></g></svg></div>

.. _postfix-string:

.. _prefix-string:

.. rubric:: Prefix and postfix strings

A range bound must consists of an integer number, and can be preceded or
followed by a common prefix or postfix string, respectively. The prefix
and postfix strings used in the lower and upper range bounds must
coincide.

.. rubric:: Constant range

If you use an element range in a static enumerated set expression
(i.e. preceded by the keyword ``DATA``), the range can only refer to
explicitly numbered elements, which need not be quoted. By padding the
numbered elements with zeroes, you indicate that AIMMS should create all
elements with the same element length.

.. rubric:: Constant range versus :any:`ElementRange`

As the begin and end elements of a constant element range are literal
elements, you cannot use a constant element range to create sets with
dynamically changing border elements. If you want to accomplish this,
you should use the :any:`ElementRange` function, which is explained in
detail in :ref:`sec:set-expr.set.functions`. Its use in the following
example is self-explanatory. The following set assignments illustrate a
constant element range and its equivalent formulation using the
:any:`ElementRange` function.

.. code-block:: aimms

	NodeSet     := DATA { node1   .. node100 } ;
	PaddedNodes := DATA { node001 .. node100 } ;

	NodeSet     := ElementRange( 1, 100, prefix: "node", fill: 0 );
	PaddedNodes := ElementRange( 1, 100, prefix: "node", fill: 1 );

.. rubric:: Symbolic integer range

Element ranges in a symbolic enumerated set can be used to create
integer ranges. Now, both bounds can be numerical expressions. Such a
construct will result in the *dynamic* creation of a number of *integer*
elements based on the value of the numerical expressions at the range
bounds. Such integer element ranges can only be assigned to *integer*
sets (see :ref:`sec:set.integer`). An example of a dynamic integer range
follows.

.. code-block:: aimms

	IntegerNodes := { FirstNode .. LastNode } ;

In this example ``IntegerNodes`` must be an integer set.

.. _by:

.. rubric:: Nonconsecutive range

If the elements in the range are not consecutive but lie at regular
intervals from one another, you can indicate this by adding a ``BY``
modifier with the proper interval length. For static enumerated sets the
interval length must be a constant, for dynamic enumerated sets it can
be any numerical expression. The following set assignments illustrate a
constant and symbolic element range with nonconsecutive elements.

.. code-block:: aimms

	EvenNodes         := DATA { node2 .. node100 by 2 } ;

	StepSize          := 2;
	EvenIntegerNodes  := { FirstNode .. LastNode by StepSize } ;

.. rubric:: Element tuples

When specifying element tuples in an enumerated set expression, it is
possible to create multiple tuples in a concise manner using cross
products. You can specify multiple elements for a particular tuple
component in the cross product either by grouping single elements using
the ``[`` and ``]`` operators or by using an element range, as shown
below.

.. code-block:: aimms

	DutchRoutes := DATA { ( Amsterdam, [Rotterdam, 'The Hague'] ),
	                      ( Rotterdam, [Amsterdam, 'The Hague'] )  } ;
	! creates  { ( 'Amsterdam', 'Rotterdam' ), ( 'Amsterdam', 'The Hague' ),
	!            ( 'Rotterdam', 'Amsterdam' ), ( 'Rotterdam', 'The Hague' ) }

	Network     := DATA { ( node1 .. node100, node1 .. node100 ) } ;

The assignment to the set ``Network`` will create a set with 10,000
elements.

.. _sec:set-expr.set.constructed:

Constructed Sets
----------------

.. rubric:: Constructed sets

A *constructed set* expression is one in which the selection of elements
is constructed through filtering on the basis of a particular condition.
When a constructed set expression contains an index, AIMMS will consider
the resulting tuples for every element in the binding set.

.. rubric:: Example

The following set assignments illustrate some constructed set
expressions, assuming that ``i`` and ``j`` are indices into the set
``Cities``.

.. code-block:: aimms

	LargeCities := { i | Population(i) > 500000 } ;

	Routes := { (i,j) | Distance(i,j) } ;

	RoutesFromLargestCity := { (LargestCity, j) in Routes } ;

In the latter assignment route tuples are constructed from
``LargestCity`` (an element-valued parameter) to every city ``j``, where
additionally each created tuple is required to lie in the set
``Routes``.

.. _constructed-set:

.. rubric:: Syntax

*constructed-set:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 240.04267 27.199999"
	   height="27.199999"
	   width="240.04266"
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
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,18.4,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">{</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 320,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 440,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,49,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-domain">binding-domain</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1360.32,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1480.32,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,154.432,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">}</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1680.32,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1800.32,1000 -50,20 v -40" /><path
	         id="path46"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 C 320,944.773 275.227,900 220,900 v 0 c -55.227,0 -100,44.773 -100,100 v 0 m 200,0 h 120 v 100 h 920.29 V 1000 900 H 440 v 100 m 920.32,0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.773 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. _binding-domain:

*binding-domain:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 558.83199 53.866665"
	   height="53.866665"
	   width="558.83197"
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
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-tuple">binding-tuple</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 907,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1147,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,119.7,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">IN</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1391,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1511,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,156.1,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-primary">set-primary</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2211,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1027,2000 -20,-50 h 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2331,2000 -20,-50 h 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2571,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,263.5,196)"><tspan
	             id="tspan52"
	             y="0"
	             x="0">|</tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2771,2000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2891,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,294.1,196)"><tspan
	             id="tspan62"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/logical-expressions.html#logical-expression">logical-expression</a></tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3951.24,2000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2451,2000 -20,-50 h 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4071.24,2000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4191.24,2000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 v 100 H 906.977 V 2000 1900 H 120 v 100 m 787,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 v 100 h 699.98 V 2000 1900 H 1511 v 100 m 700,0 h 120 m -1304,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 492 120 492 c 55.23,0 100,44.77 100,100 v 200 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 H 3951.21 V 2000 1900 H 2891 v 100 m 1060.24,0 h 120 M 2451,2000 v -200 c 0,-55.23 44.77,-100 100,-100 h 650.12 120 650.12 c 55.22,0 100,44.77 100,100 v 200 h 120" /></g></g></svg></div>

.. _binding-tuple:

*binding-tuple:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 303.15733 107.2"
	   height="107.2"
	   width="303.15732"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,680.26665)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 90,5000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 280,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,34.4,436)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 480,4400 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 660,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,71,436)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-element">binding-element</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1613.68,4400 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 570,4400 20,50 h -40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1036.84,4700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,110.084,466)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1236.84,4700 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1703.68,4400 20,50 h -40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1793.68,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g52"><text
	           id="text56"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,185.768,436)"><tspan
	             id="tspan54"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1993.68,4400 50,-20 v 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2183.68,5000 -20,-50 h 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 660,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,71,496)"><tspan
	             id="tspan66"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-element">binding-element</a></tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1613.68,5000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2273.68,5000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5000 h 90 m 0,0 v -500 c 0,-55.23 44.773,-100 100,-100 v 0 h 90 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 90 m 0,0 v 0 h 90 v 100 h 953.65 V 4400 4300 H 660 v 100 m 953.68,0 h 90 M 570,4400 v 200 c 0,55.23 44.773,100 100,100 h 276.84 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 276.84 c 55.23,0 100,-44.77 100,-100 v -200 h 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 v 0 c 55.23,0 100,44.77 100,100 v 500 M 90,5000 h 100 380 90 v 100 h 953.65 V 5000 4900 H 660 v 100 m 953.68,0 h 90 480 90" /></g></g></svg></div>

.. _binding-element:

*binding-element:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 300.10667 107.2"
	   height="107.2"
	   width="300.10666"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,680.26665)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 90,5000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 280,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,33,436)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-declaration/index-declaration-and-attributes.html#index">index</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 666.801,4400 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 846.801,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,89.6801,436)"><tspan
	             id="tspan30"
	             y="0"
	             x="0">IN</tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1090.8,4400 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1180.8,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,123.08,436)"><tspan
	             id="tspan40"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-primary">set-primary</a></tspan></text>
	</g><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1880.8,4400 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 756.801,4400 20,50 h -40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1970.8,4400 20,50 h -40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2160.8,5000 -20,-50 h 40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 551.902,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g54"><text
	           id="text58"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,60.1902,496)"><tspan
	             id="tspan56"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1698.9,5000 50,-20 v 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2250.8,5000 -50,20 v -40" /><path
	         id="path64"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5000 h 90 m 0,0 v -500 c 0,-55.23 44.773,-100 100,-100 v 0 h 90 v 100 H 666.793 V 4400 4300 H 280 v 100 m 386.801,0 h 90 m 0,0 v 0 h 90 v 0 c 0,55.23 44.773,100 100,100 h 44 c 55.229,0 99.999,-44.77 99.999,-100 v 0 0 c 0,-55.23 -44.77,-100 -99.999,-100 h -44 c -55.227,0 -100,44.77 -100,100 v 0 m 243.999,0 h 90 v 100 h 699.98 V 4400 4300 H 1180.8 v 100 m 700,0 h 90 m -1213.999,0 v 200 c 0,55.23 44.773,100 100,100 h 461.999 90 462 c 55.23,0 100,-44.77 100,-100 v -200 h 90 v 0 c 55.23,0 100,44.77 100,100 v 500 M 90,5000 h 100 271.902 90 v 100 H 1698.88 V 5000 4900 H 551.902 v 100 m 1146.998,0 h 90 371.9 90" /></g></g></svg></div>

.. rubric:: Binding domain

The tuple selection in a constructed set expression behaves exactly the
same as the tuple selection on the left-hand side of an assignment to an
indexed parameter. This means that all tuple components can be either an
explicit quoted set element, a general set element expression, or a
binding index. The tuple can be subject to a logical condition, further
restricting the number of elements constructed.

.. _sec:set-expr.set.operators:

Set Operators
-------------

.. _cross:

.. _set-operator:

.. rubric:: Four set operators

There are four binary set operators in AIMMS: Cartesian product,
intersection, union, and difference. Their notation and precedence are
given in :numref:`table:set-expr.set-op`. Expressions containing these
set operators are read from left to right and the operands can be any
set expression. There are no unary set operators.

.. _table:set-expr.set-op:

.. table:: Set operators

   +-----------------------+-----------------------+-----------------------+
   | Operator              | Notation              | Precedence            |
   +=======================+=======================+=======================+
   | intersection          | ``*``                 |    3 (high)           |
   +-----------------------+-----------------------+-----------------------+
   | difference            | ``-``                 |    2                  |
   +-----------------------+-----------------------+-----------------------+
   | union                 | ``+``                 |    2                  |
   +-----------------------+-----------------------+-----------------------+
   | Cartesian product     | ``CROSS``             |    1 (low)            |
   +-----------------------+-----------------------+-----------------------+

.. rubric:: Example

The following set assignments to integer sets and Cartesian products of
integer sets illustrate the use of all available set operators.

.. code-block:: aimms

	S := {1,2,3,4} * {3,4,5,6} ;     ! Intersection of integer sets: {3,4}.

	S := {1,2} + {3,4} ;             ! Union of simple sets:
	S := {1,3,4} + {2} + {1,2} ;     ! {1,2,3,4}

	S := {1,2,3,4} - {2,4,5,7} ;     ! Difference of integer sets: {1,3}.

	T := {1,2} cross {1,2} ;         ! The cross of two integer sets:
	                                 ! {(1,1),(1,2),(2,1),(2,2)}.

The precedence and associativity of the operators is demonstrated by the
assignments

.. code-block:: aimms

	T := A cross B - C ;      ! Same as A cross (B - C).
	T := A - B * C + D ;      ! Same as (A - (B * C)) + D.
	T := A - B * C + D * E ;  ! Same as (A - (B * C)) + (D * E).

The operands of union, difference, and intersection must have the same
dimensions.

.. code-block:: aimms

	T := {(1,2),(1,3)} * {(1,3)} ;              ! Same as {(1,3)}.

	T := {(1,2),(1,3)} + {(i,j) | a(i,j) > 1} ; ! Union of enumerated
	                                            ! and constructed set of
	                                            ! the same dimension.

	T := {(1,2),(1,3)} + {(1,2,3)} ;            ! ERROR: dimensions differ.

.. _sec:set-expr.set.functions:

Set Functions
-------------

.. rubric:: Set functions

A special type of set expression is a call to one of the following
set-valued functions

-  :any:`ElementRange`,

-  :any:`SubRange`,

-  :any:`ConstraintVariables`,

-  :any:`VariableConstraints`, or

-  A user-defined function.

The :any:`ElementRange` and :any:`SubRange` functions are discussed in this
section, while the functions :any:`ConstraintVariables` and
:any:`VariableConstraints` are discussed in :ref:`sec:mp.mp`. The syntax of
and use of tags in function calls is discussed in
:ref:`sec:intern.func`.

.. _elementrange-LR:

.. rubric:: The function :any:`ElementRange`

The :any:`ElementRange` function allows you to *dynamically* create or
change the contents of a set of non-integer elements based on the value
of integer-valued scalars expressions.

.. rubric:: Arguments

The :any:`ElementRange` function has two mandatory integer arguments.

-  *first*, the integer value for which the first element must be
   created, and

-  *last*, the integer value for which the last element must be created.

In addition, it allows the following four optional arguments.

-  *incr*, the integer-valued interval length between two consecutive
   elements (default value 1),

-  *prefix*, the prefix string for every element (by default, the empty
   string),

-  *postfix*, the postfix string (by default, the empty string), and

-  *fill*, a logical indicator (0 or 1) whether the numbers must be
   padded with zeroes (default value 1).

If you use any of the optional arguments you must use their formal
argument names as tags.

.. rubric:: Example

Consider the sets ``S`` and ``T`` initialized by the constant set
expressions

.. code-block:: aimms

	NodeSet     := DATA { node1   .. node100 } ;
	PaddedNodes := DATA { node001 .. node100 } ;
	EvenNodes   := DATA { node2   .. node100 by 2 } ;

These sets can also be created in a dynamic manner by the following
applications of the :any:`ElementRange` function.

.. code-block:: aimms

	NodeSet     := ElementRange( 1, 100, prefix: "node", fill: 0 );
	PaddedNodes := ElementRange( 1, 100, prefix: "node", fill: 1 );
	EvenNodes   := ElementRange( 2, 100, prefix: "node", fill: 0, incr: 2 );

.. _subrange-LR:

.. rubric:: The :any:`SubRange` function

The :any:`SubRange` function has three arguments:

-  a simple *set*,

-  the *first* element, and

-  the *last* element.

The result of the function is the subset ranging from the *first* to the
*last* element. If the first element is positioned after the last
element, the empty set will result.

.. rubric:: Example

Assume that the set ``Cities`` is organized such that all foreign cities
are consecutive, and that ``FirstForeignCity`` and ``LastForeignCity``
are element-valued parameters into the set ``Cities``. Then the
following assignment will create the subset ``ForeignCities`` of
``Cities``

.. code-block:: aimms

	ForeignCities := SubRange( Cities, FirstForeignCity, LastForeignCity ) ;

.. _sec:set-expr.set.iter:

.. _sec:set-expr.set.sort:

Iterative Set Operators
-----------------------

.. rubric:: Iterative operators

Iterative operators form an important class of operators that are
especially designed for indexed expressions in AIMMS. There are set,
element-valued, arithmetic, statistical, and logical iterative
operators. The syntax is always similar.

.. _iterative-expression:

.. rubric:: Syntax

*iterative-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 603.66402 80.533333"
	   height="80.533333"
	   width="603.664"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,306.93333)"
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
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#iterative-operator">iterative-operator</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1126.96,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1246.96,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,131.096,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1446.96,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1566.96,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,161.696,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-domain">binding-domain</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2487.28,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2847.28,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,291.128,196)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3047.28,2000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3167.28,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,321.728,196)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3847.48,2000 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2727.28,2000 20,50 h -40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3967.48,2000 20,50 h -40" /><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2607.28,2000 -20,-50 h 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4087.48,2000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4207.48,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g74"><text
	           id="text78"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,427.148,196)"><tspan
	             id="tspan76"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4407.48,2000 50,-20 v 40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4527.48,2000 -50,20 v -40" /><path
	         id="path84"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 v 100 H 1126.93 V 2000 1900 H 120 v 100 m 1006.96,0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 920.29 v -100 -100 h -920.29 v 100 m 920.32,0 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 680.19 v -100 -100 h -680.19 v 100 m 680.2,0 h 120 m -1240.2,0 v 200 c 0,55.23 44.77,100 100,100 h 460.1 120 460.1 c 55.23,0 100,-44.77 100,-100 v -200 h 120 m -1480.2,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 580.1 120 580.1 c 55.23,0 100,44.77 100,100 v 200 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. _iterative-operator:

.. rubric:: Explanation

The first argument of all iterative operators is a *binding domain*. It
consists of a single index or tuple of indices, optionally qualified by
a logical condition. The second argument and further arguments must be
expressions. These expressions are evaluated for every index or tuple in
the binding domain, and the result is input for the particular iterative
operator at hand. Indices in the expressions that are not part of the
binding domain of the iterative operators are referred to as *outer
indices*, and must be bound elsewhere.

.. _Sort:

.. rubric:: Set-related iterative operators

AIMMS possesses the following set-related iterative operators:

-  the ``Sort`` operator for sorting the elements in a domain,

-  the ``NBest`` operator for obtaining the :math:`n` best elements in a
   domain according to a certain criterion, and

-  the ``Intersection`` and ``Union`` operators for repeated
   intersection or union of indexed sets.

.. rubric:: Reordering your data

Sorting the elements of a set is a useful tool for controlling the flow
of execution and for presenting reordered data in the graphical user
interface. There are two mechanism available to you for sorting set
elements

-  the ``OrderBy`` attribute of a set, and

-  the ``Sort`` operator.

.. rubric:: Sorting semantics

The second and further operands of the ``Sort`` operator must be
numerical, element-valued or string expressions. The result of the
``Sort`` operator will consist of precisely those elements that satisfy
the domain condition, sorted according to the single or multiple
ordering criteria specified by the second and further operands.
:ref:`attr:set.order-by` discusses the expressions that can be used for
specifying an ordering principle.

.. rubric:: Receiving set

Note that the set to which the result of the ``Sort`` operator is
assigned must have the ``OrderBy`` attribute set to ``User`` (see also
:ref:`sec:set.simple`) for the operation to be useful. Without this
setting AIMMS will store the elements of the result set of the ``Sort``
operator, but will discard the underlying ordering.

.. rubric:: Example

The following assignments will result in the same set orderings as in
the example of the ``OrderBy`` attribute in :ref:`attr:set.order-by`.

.. code-block:: aimms

	LexicographicSupplyCities := Sort( i in SupplyCities, i ) ;

	ReverseLexicographicSupplyCities := Sort( i in SupplyCities, -i );

	SupplyCitiesByIncreasingTransport :=
	    Sort( i in SupplyCities, Sum( j, Transport(i,j) );

	SupplyCitiesByDecreasingTransportThenLexicographic :=
	    Sort( i in SupplyCities, - Sum( j, Transport(i,j) ), i );

.. rubric:: Sorting root sets

AIMMS will even allow you to sort the elements of a root set. Because
the entire execution system of AIMMS is built around a fixed ordering of
the root sets, sorting root sets may influence the overall execution in
a negative manner. :ref:`sec:eff.set.ordering` explains the efficiency
considerations regarding root set ordering in more detail.

.. _nbest:

.. rubric:: Obtaining the :math:`n` best elements

You can use the ``NBest`` operator, when you need the :math:`n` best
elements in a set according to a single ordering criterion. The syntax
of the ``NBest`` is similar to that of the ``Sort`` operator. The first
expression after the binding domain is the criterion with respect to
which you want elements in the binding domain to be ordered. The second
expression refers to the number of elements :math:`n` in which you are
interested.

.. rubric:: Example

The following assignment will, for every city ``i``, select the three
cities to which the largest transports emanating from ``i`` take place.
The result is stored in the indexed set ``LargestTransportCities(i)``.

.. code-block:: aimms

	LargestTransportCities(i) := NBest( j, Transport(i,j), 3 );

.. _intersection:

.. _union:

.. rubric:: Repeated intersection and union

With the ``Intersection`` and ``Union`` operators you can perform
repeated set intersection or union respectively. A typical application
is to take the repeated intersection or union of all instances of an
indexed set. However, any set valued expression can be used on the
second argument.

.. rubric:: Example

Consider the following indexed set declarations.

.. code-block:: aimms

	Set IndSet1 {
	    IndexDomain : s1;
	    SubsetOf    : S;
	}
	Set IndSet2 {
	    IndexDomain : s1;
	    SubsetOf    : S;
	}

With these declarations, the following assignments illustrate valid uses
of the ``Union`` and ``Intersection`` operators.

.. code-block:: aimms

	SubS := Union( s1, IndSet1(s1) );
	SubS := Intersection( s1, IndSet1(s1) + IndSet2(s1) );

.. _sec:set-expr.set.elem:

Set Element Expressions as Singleton Sets
-----------------------------------------

.. rubric:: Element expressions ...

Element expressions can be used in a set expression as well. In the
context of a set expression, AIMMS will interpret an element expression
as the singleton set containing only the element represented by the
element expression. Set element expressions are discussed in full detail
in :ref:`sec:set-expr.elem`.

.. rubric:: ...versus enumerated sets

Using an element expression as a set expression can equivalently be
expressed as a symbolic enumerated set containing the element expression
as its sole element. Whenever there is no need to group multiple
elements, AIMMS allows you to omit the surrounding braces.

.. rubric:: Example

The following set assignment illustrate some simple set element
expressions used as a singleton set expression.

.. code-block:: aimms

	! Remove LargestCity from the set of Cities
	Cities -= LargestCity ;

	! Remove first element from the set of Cities
	Cities -= Element(Cities,1) ;

	! Remove LargestCity and SmallestCity from Cities
	Cities -= LargestCity + SmallestCity ;

	! The set of Cities minus the CapitalCity
	NonCapitalCities := Cities - CapitalCity ;