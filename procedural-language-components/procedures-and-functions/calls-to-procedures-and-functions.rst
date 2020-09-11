.. _sec:intern.ref:

Calls to Procedures and Functions
=================================

.. rubric:: Consistency with prototype

Functions and procedures must be called from within AIMMS in accordance
with the prototype as specified in their declaration. For every call to
a function or procedure, AIMMS will verify not only the number of
arguments, but also whether the arguments and result are consistent with
the specified domains and ranges.

.. rubric:: Example procedure call

Consider the procedure ``ComputeShortestDistance`` defined in
:ref:`sec:intern.proc`. Further assume that ``DistanceMatrix`` and
``ShortestDistanceMatrix`` are two-dimensional identifiers defined over
``Cities``\ :math:`{}\times{}`\ ``Cities``. Then the following
assignment illustrates a valid procedure call.

.. code-block:: aimms

	for ( i ) do
	    ComputeShortestDistance(i, DistanceMatrix, ShortestDistanceMatrix(i,.)) ;
	endfor;

As you will see later on, the ``.`` notation used in the third
argument is a shorthand for the corresponding domain set. In this
instance, the corresponding domain set of
``ShortestDistanceMatrix(i,.)`` is the set ``Cities``.

.. rubric:: Domain checking of arguments

In analyzing the resulting domains of the arguments, AIMMS takes into
account the following considerations.

-  Due to the surrounding ``FOR`` statement the index ``i`` is bound, so
   that the first argument is indeed an element in the set ``Cities``.

-  The second argument ``DistanceMatrix`` is provided without an
   explicit domain. AIMMS will interpret this as offering the complete
   two-dimensional identifier ``DistanceMatrix``. As expected, the
   argument is defined over ``Cities``\ :math:`{}\times{}`\ ``Cities``.

-  Because of the binding of index ``i``, the third argument
   ``ShortestDistanceMatrix(i,.)`` results into the (expected)
   one-dimensional slice over the set ``Cities`` in which the result of
   the computation will be stored.

Thus, the domains of the actual arguments coincide with the domains of
the formal arguments, and AIMMS can correctly compute the result.

.. rubric:: Example function call

Now consider the function ``ShortestDistance`` defined in
:ref:`sec:intern.proc`. The following statement is equivalent to the
``FOR`` statement of the previous example.

.. code-block:: aimms

	ShortestDistanceMatrix(i,j) := ShortestDistance(i, DistanceMatrix)(j) ;

In this example index binding takes place through the indexed
assignment. Per city ``i`` AIMMS will call the function
``ShortestDistance`` once, and assign the one-dimensional result
(indexed by ``j``) to the one-dimensional slice
``ShortestDistanceMatrix(i,j)``.

.. rubric:: Call syntax

The general forms of procedure and function calls are identical, except
that a function reference can have additional indexing.

.. _procedure-call:

*procedure-call:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 393.87199 93.866661"
	   height="93.866661"
	   width="393.87198"
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
	         d="m 100,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,15,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/internal-procedures.html#procedure">procedure</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 740.238,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 940.238,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,100.424,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1140.24,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1340.24,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,139.024,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#tagged-argument">tagged-argument</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2354.04,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1240.24,2000 20,50 h -40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1747.14,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,181.114,226)"><tspan
	             id="tspan50"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1947.14,2300 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2454.04,2000 20,50 h -40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2554.04,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,261.804,196)"><tspan
	             id="tspan62"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2754.04,2000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 840.238,2000 -20,-50 h 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2854.04,2000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2954.04,2000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 100 v 100 H 740.227 V 2000 1900 H 100 v 100 m 640.238,0 h 100 m 0,0 v 0 h 100 v 0 c 0,55.23 44.774,100 100.002,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.228,0 -100.002,44.77 -100.002,100 v 0 m 200.002,0 h 100 m 0,0 v 0 h 100 v 100 H 2354.02 V 2000 1900 H 1340.24 v 100 m 1013.8,0 h 100 m -1213.8,0 v 200 c 0,55.23 44.77,100 100,100 h 306.9 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 306.9 c 55.22,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 m -2013.802,0 v -200 c 0,-55.23 44.774,-100 100,-100 h 856.902 100 856.9 c 55.22,0 100,44.77 100,100 v 200 h 100" /></g></g></svg></div>

.. _function-call:

*function-call:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 624.13869 93.866661"
	   height="93.866661"
	   width="624.13867"
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
	         d="m 75,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,12.5,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/internal-functions.html#function">function</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 595.238,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 745.238,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,80.9238,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 945.238,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1095.24,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,114.524,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#tagged-argument">tagged-argument</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2109.04,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1020.24,2000 20,50 h -40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1502.14,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,156.614,226)"><tspan
	             id="tspan50"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1702.14,2300 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2184.04,2000 20,50 h -40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2259.04,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,232.304,196)"><tspan
	             id="tspan62"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2459.04,2000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 670.238,2000 -20,-50 h 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2534.04,2000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2684.04,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g74"><text
	           id="text78"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,274.804,196)"><tspan
	             id="tspan76"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2884.04,2000 50,-20 v 40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3034.04,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,308.404,196)"><tspan
	             id="tspan86"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4181.04,2000 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2959.04,2000 20,50 h -40" /><path
	         id="path94"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3507.54,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g96"><text
	           id="text100"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,357.154,226)"><tspan
	             id="tspan98"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3707.54,2300 50,-20 v 40" /><path
	         id="path104"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4256.04,2000 20,50 h -40" /><path
	         id="path106"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4331.04,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g108"><text
	           id="text112"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,439.504,196)"><tspan
	             id="tspan110"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path114"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4531.04,2000 50,-20 v 40" /><path
	         id="path116"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2609.04,2000 -20,-50 h 40" /><path
	         id="path118"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4606.04,2000 -20,-50 h 40" /><path
	         id="path120"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4681.04,2000 -50,20 v -40" /><path
	         id="path122"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 75 v 100 H 595.23 V 2000 1900 H 75 v 100 m 520.238,0 h 75 m 0,0 v 0 h 75 v 0 c 0,55.23 44.774,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.226,0 -100,44.77 -100,100 v 0 m 200,0 h 75.002 m 0,0 v 0 h 75 v 100 H 2109.02 V 2000 1900 H 1095.24 v 100 m 1013.8,0 h 75 m -1163.8,0 v 200 c 0,55.23 44.77,100 100,100 h 306.9 75 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 75 306.9 c 55.22,0 100,-44.77 100,-100 v -200 h 75 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 75 m -1863.802,0 v -200 c 0,-55.23 44.774,-100 100,-100 h 794.402 75 794.4 c 55.22,0 100,44.77 100,100 v 200 h 75 m 0,0 v 0 h 75 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 75 m 0,0 v 0 h 75 v 100 H 4181.01 V 2000 1900 H 3034.04 v 100 m 1147,0 h 75 m -1297,0 v 200 c 0,55.23 44.77,100 100,100 h 373.5 75 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 75 373.5 c 55.22,0 100,-44.77 100,-100 v -200 h 75 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 75 m -1997,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 861 75 861 c 55.22,0 100,44.77 100,100 v 200 h 75" /></g></g></svg></div>

.. rubric:: Actual arguments

Each actual argument can be

-  any type of scalar expression for *scalar* arguments, and

-  a reference to an identifier slice of the proper dimensions for
   *non-scalar* arguments.

Actual arguments can be tagged with their formal argument name used
inside the declaration of the function or procedure. The syntax follows.

.. _tagged-argument:

*tagged-argument:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 315.62135 53.866665"
	   height="53.866665"
	   width="315.62134"
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
	         d="m 240,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,29,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#arg-tag">arg-tag</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 720.16,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 840.16,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,90.416,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1040.16,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,2000 -20,-50 h 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1160.16,2000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1280.16,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,133.016,196)"><tspan
	             id="tspan42"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#actual-argument">actual-argument</a></tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2247.16,2000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2367.16,2000 -50,20 v -40" /><path
	         id="path50"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 m 0,0 v 0 h 120 v 100 H 720.148 V 2000 1900 H 240 v 100 m 480.16,0 h 120 v 0 c 0,55.23 44.774,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.226,0 -100,44.77 -100,100 v 0 m 200,0 h 120 M 120,2000 v -200 c 0,-55.23 44.773,-100 100,-100 h 360.078 120 360.082 c 55.23,0 100,44.77 100,100 v 200 h 120 v 100 h 966.98 v -100 -100 h -966.98 v 100 m 967,0 h 120" /></g></g></svg></div>

.. _actual-argument:

*actual-argument:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 201.792 107.2"
	   height="107.2"
	   width="201.79199"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,546.93332)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,4000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 340,3400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,39,336)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#identifier-slice">identifier-slice</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1173.44,3400 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1393.44,4000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,4000 -20,-50 h 40" /><path
	         id="path30"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 316.602,3700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g32"><text
	           id="text36"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,36.6602,366)"><tspan
	             id="tspan34"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-expression">set-expression</a></tspan></text>
	</g><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1196.84,3700 50,-20 v 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1393.44,4000 -20,-50 h 40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 416.621,4000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g44"><text
	           id="text48"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,46.6621,396)"><tspan
	             id="tspan46"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path50"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1096.82,4000 50,-20 v 40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1513.44,4000 -50,20 v -40" /><path
	         id="path54"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,4000 h 120 m 0,0 v -500 c 0,-55.23 44.773,-100 100,-100 v 0 h 120 v 100 h 833.41 V 3400 3300 H 340 v 100 m 833.44,0 h 120 v 0 c 55.23,0 100,44.77 100,100 v 500 M 120,4000 v -200 c 0,-55.23 44.773,-100 100,-100 h -23.398 120 v 100 H 1196.82 V 3700 3600 H 316.602 v 100 m 880.238,0 h 120 -23.4 c 55.23,0 100,44.77 100,100 v 200 M 120,4000 h 100 76.621 120 v 100 H 1096.81 V 4000 3900 H 416.621 v 100 m 680.199,0 h 120 176.62 120" /></g></g></svg></div>

.. _identifier-slice:

*identifier-slice:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 424.05867 113.86666"
	   height="113.86666"
	   width="424.05865"
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
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,15,296)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#identifier-part">identifier-part</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 900.199,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1100.2,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,116.42,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1300.2,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1600.2,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,165.02,296)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#set-expression">set-expression</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2480.44,3000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1500.2,3000 -20,-50 h 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1940.32,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,200.432,266)"><tspan
	             id="tspan50"
	             y="0"
	             x="0">.</tspan></text>
	</g><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2140.32,2700 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2580.44,3000 -20,-50 h 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1400.2,3000 20,50 h -40" /><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1940.32,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g62"><text
	           id="text66"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,200.432,326)"><tspan
	             id="tspan64"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2140.32,3300 50,-20 v 40" /><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2680.44,3000 20,50 h -40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2780.44,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g74"><text
	           id="text78"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,284.444,296)"><tspan
	             id="tspan76"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2980.44,3000 50,-20 v 40" /><path
	         id="path82"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1000.2,3000 -20.001,-50 h 40.001" /><path
	         id="path84"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3080.44,3000 -20,-50 h 40" /><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3180.44,3000 -50,20 v -40" /><path
	         id="path88"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 100 v 100 H 900.172 V 3000 2900 H 100 v 100 m 800.199,0 H 1000.2 m 0,0 v 0 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 m 0,0 v 0 h 100 m 0,0 v 0 h 100 v 100 h 880.22 V 3000 2900 H 1600.2 v 100 m 880.24,0 h 100 m -1080.24,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 240.12 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 240.12 c 55.23,0 100,44.77 100,100 v 200 h 100 m -1280.24,0 v 200 c 0,55.23 44.77,100 100,100 h 340.12 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 340.12 c 55.23,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 m -2080.24,0 v -350 c 0,-55.23 44.77,-100 100,-100 h 890.12 100 890.12 c 55.23,0 100,44.77 100,100 v 350 h 100" /></g></g></svg></div>

.. rubric:: Scalar and set arguments

For scalar and set arguments that are of type ``Input`` you can enter
any scalar or set expression, respectively. Scalar and set arguments
that are of type ``InOut`` or ``Output`` must contain a reference to a
scalar parameter or set, or to a scalar slice of an indexed parameter or
set. The latter is necessary so that AIMMS knows where to store the
output value.

.. rubric:: No slices of indexed sets

Note that AIMMS does not allow you to pass slices of an indexed set as a
set arguments to functions and procedures. If you want to pass the
contents of a slice of an indexed set as an argument to a procedure or
function, you should assign the contents to a simple (sub)set instead,
and pass that set as an argument.

.. rubric:: Multidimensional arguments

For multidimensional actual arguments AIMMS only allows references to
identifiers or slices thereof. Such arguments can be indicated in two
manners.

-  If you just enter the name of a multidimensional identifier, AIMMS
   assumes that you want to pass the fully dimensioned data block
   associated with the identifier.

-  If you enter an identifier name plus

   -  a ``.``,

   -  a set element, or

   -  a set expression

   at each position in the index domain of the identifier, AIMMS will
   pass the corresponding identifier *slice* or *subdomain*.

.. rubric:: The ``.`` notation

When passing slices or subdomains of a multidimensional identifier
argument, you can use the ``.`` shorthand notation at a particular
position in the index domain. With it you indicate that AIMMS should use
the corresponding domain set of the identifier at hand at that index
position. Recall the argument ``ShortestDistanceMatrix(i,.)`` in the
call to the procedure ``ComputeShortestDistance`` discussed at the
beginning of this section. As the index domain of
``ShortestDistanceMatrix`` is the set ``Cities`` :math:`\times`
``Cities``, the ``.`` reference stands for a reference to the set
``Cities``.

.. rubric:: Slicing

By specifying an explicit set element or an element expression at a
certain index position of an actual argument, you will decrease the
dimension of the resulting slice by one. The call to the procedure
``ComputeShortestDistance`` discussed earlier in this section
illustrates an example of an actual argument containing a
one-dimensional slice of a two-dimensional parameter.

.. rubric:: Dimensions must match

Note that AIMMS requires that the dimensions of the formal and actual
arguments match exactly.

.. rubric:: Subdomains

By specifying a subset expression at a particular index position of an
indexed argument, you indicate to AIMMS that the procedure or function
should only consider the argument as defined over this subdomain.

.. rubric:: Example

Consider the Cobb-Douglas function discussed in the previous section,
and assume the existence of a parameter ``a(f)`` and a parameter
``c(f)``, both defined over a set ``Factors``. Then the statement

.. code-block:: aimms

	Result := CobbDouglas(a,c) ;

will compute the result by taking the product of exponents over all
factors ``f``. If ``SubFactors`` is a subset of ``Factors``, satisfying
the condition on the share parameter ``a(f)``, then the following call
will compute the result by only taking the product over factors ``f`` in
the subset ``SubFactors``.

.. code-block:: aimms

	Result := CobbDouglas( a(SubFactors), c(SubFactors) );

.. rubric:: Global subdomains

Whenever a formal argument refers to an indexed identifier defined over
global sets, it could be that an actual argument in a function or
procedure call refers to an identifier defined over a superset of one or
more of these global sets. In this case, AIMMS will automatically
restrict the domain of the actual argument to the domain of the formal
argument. Likewise, if an index set of an actual argument is a real
subset of the corresponding global index set of a formal argument, the
values of the formal argument, when referred to from within the body of
the procedure, will assume the default value of the formal argument in
the complement of the index (sub)set of actual argument.

.. rubric:: Local subdomains

Whenever a formal argument refers to an indexed identifier defined over
local sets, the domain of the actual argument can be further restricted
to a subdomain as in the example above. In any case, the (sub)domain of
the actual argument determines the contents of the local set(s) used in
the formal arguments. Note that consistency in the specified domains of
the actual arguments is required when a local set is used in the index
domain of several formal arguments.

.. _arg-tag:

.. rubric:: Tagging arguments

In order to improve the understandability of calls to procedures and
functions the actual arguments in a reference may be tagged with the
formal argument names used in the declaration. In a procedure reference,
it is mandatory to tag all *optional* arguments which do not occur in
their natural order.

.. rubric:: Permuting tagged arguments

Tagged arguments may be inserted at any position in the argument list,
because AIMMS can determine their actual position based on the tag. The
non-tagged arguments must keep their relative position, and will be
intertwined with the (permuted) tagged arguments to form the complete
argument list.

.. rubric:: Example

The following permuted call to the procedure ``ComputeShortestDistance``
illustrates the use of tags.

.. code-block:: aimms

	for ( i ) do
	    ComputeShortestDistance( Distance       : ShortestDistanceMatrix(i,.),
	                             DistanceMatrix : DistanceMatrix,
	                             City           : i );
	endfor;

.. rubric:: Using the return value
   :name: proc.ret-val.use

As indicated in :ref:`sec:intern.proc` procedures in AIMMS can return
with an integer return value. Its use is limited to two situations.

-  You can assign the return value of a procedure to a scalar parameter
   in the calling procedure. However, a procedure call can never be part
   of a numerical expression.

-  You can use the return value in a logical condition in, for instance,
   an ``IF`` statement to terminate the execution when a procedure
   returns with an error condition.

You can use a procedure just as a single statement and ignore the return
value, or use the return value as described above. In the latter case,
AIMMS will first execute the procedure, and subsequently use the return
value as indicated.

.. rubric:: Example

Assume the existence of a procedure ``AskForUserInputs(Inputs,Outputs)``
which presents a dialog box to the user, passes the results to the
``Outputs`` argument, and returns with a nonzero value when the user has
pressed the OK button in the dialog box. Then the following ``IF``
statement illustrates a valid use of the return value.

.. code-block:: aimms

	if ( AskForUserInputs( Inputs, Outputs ) )
	then
	   ... /* Take appropriate action to process user inputs */
	else
	   ... /* Take actions to process invalid user input */
	endif ;

.. _sec:intern.ref.apply:

The ``APPLY`` Operator
----------------------

.. rubric:: Data-driven procedures
   :name: apply

In many real-life applications the exact nature of a specific type of
computation may heavily depend on particular characteristics of its
input data. To accommodate such data-driven computations, AIMMS offers
the ``APPLY`` operator which can be used to dynamically select a
procedure or function of a given prototype to perform a particular
computation. The following two examples give you some feeling of the
possible uses.

.. rubric:: Example: processing events

In event-based applications many different types of events may exist,
each of which may require an event-type specific sequence of actions to
process it. For instance, a ship arrival event should be treated
differently from an event representing a pipeline batch, or an event
representing a batch feeding a crude distiller unit. Ideally, such
event-specific actions should be modeled as a separate procedure for
each event type.

.. rubric:: Example: product blending

A common action in the oil-processing industry is the blending of crudes
and intermediate products. During this process certain material
properties are monitored, and their computation for a blend require a
property-specific *blending rule*. For instance, the sulphur content of
a mixture may blend linearly in weight, while for density the reciprocal
density values blend linear in weight. Ideally, each blending rule
should be implemented as a separate procedure or function.

.. rubric:: The ``APPLY`` operator

With the ``APPLY`` operator you can dynamically select a procedure or
function to be called. The first argument of the ``APPLY`` operator must
be the name of the procedure or function that you want to call. If the
called procedure or function has arguments itself, these must be added
as the second and further arguments to the ``APPLY`` operator. In case
of an indexed-valued function, you can add indexing to the ``APPLY``
operator as if it were a function call.

.. rubric:: Requirements

In order to allow AIMMS to perform the necessary dynamic type checking
for the ``APPLY`` operator, certain requirements must be met:

-  the first argument of the ``APPLY`` operator must be a reference to a
   string parameter or to an element parameter into the set
   :any:`AllIdentifiers`,

-  this element parameter must have a ``Default`` value, which is the
   name of an existing procedure or function in your model, and

-  all other values that this string or element parameter assumes must
   be existing procedures or functions with the same prototype as its
   ``Default`` value.

.. rubric:: Example: processing events elaborated

Consider a set of ``Events`` with an index ``e`` and an element
parameter named ``CurrentEvent``. Assume that each event ``e`` has been
assigned an event type from a set ``EventTypes``, and that an event
handler is defined for each event type. It is further assumed that the
event handler of a particular event type takes the appropriate actions
for that type. The following declarations illustrates this set up.

.. code-block:: aimms

	ElementParameter EventType {
	    IndexDomain    : e;
	    Range          : EventTypes;
	}
	ElementParameter EventHandler {
	    IndexDomain    : et in EventTypes;
	    Range          : AllIdentifiers;
	    Default        : NoEventHandlerSelected;
	    InitialData    : {
	          DATA { ShipArrivalEvent    : DischargeShip,
	                 PipelineEvent       : PumpoverPipelineBatch,
	                 CrudeDistillerEvent : CrudeDistillerBatch }
	    }
	}

The ``Default`` value of the parameter ``EventHandler(et)``, as well as
all of the values assigned in the ``InitialData`` attribute, must be
valid procedure names in the model, each having the same prototype. In
this example, it is assumed that the procedures
``NoEventHandlerSelected``, ``DischargeShip``,
``PumpoverPipelineBatch``, and ``CrudeDistillerBatch`` all have two
arguments, the first being an element of a set ``Events``, and the
second being the time at which the event has to commence. Then the
following call to the ``APPLY`` statement implements the call to an
event type specific event handler for a particular event
``CurrentEvent`` at time ``NewEventTime``.

.. code-block:: aimms

	Apply( EventHandler(EventType(CurrentEvent)), CurrentEvent, NewEventTime );

When no event handler for a particular event type has been provided, the
default procedure ``NoEventHandlerSelected`` is run which can abort with
an appropriate error message.

.. rubric:: Use in constraints

When applied to functions, you can also use the ``APPLY`` operator
inside constraints. This allows you, for instance, to provide a generic
constraint where the individual terms depend on the value of set
elements in the domain of the constraint. Note, that such use of the
``APPLY`` operator will only work in conjunction with external
functions, which allow the use of variable arguments (see
:ref:`sec:extern.constraints`).

.. rubric:: Example: product blending

Consider a set of ``Products`` with index ``p``, and a set of monitored
``Properties`` with index ``q``. With each property ``q`` a blend rule
function can be associated such that the resulting values blend linear
in weight. These property-dependent functions can be expressed by the
element parameter ``BlendRule(q)`` given by

.. code-block:: aimms

	ElementParameter BlendRule {
	    IndexDomain    : q;
	    Range          : AllIdentifiers;
	    Default        : BlendLinear;
	    InitialData    : {
	          DATA { Sulphur    : BlendLinear,
	                 Density    : BlendReciprocal,
	                 Viscosity  : BlendViscosity   }
	    }
	}

Thus, the computation of the property values of a product blend can be
expressed by the following single constraint, which takes into account
the differing blend rules for all properties.

.. code-block:: aimms

	Constraint ComputeBlendProperty {
	    IndexDomain    : q;
	    Definition     : {
	        Sum[p, ProductAmount(p)  * Apply(BlendRule(q), ProductProperty(p,q))] =
	        Sum[p, ProductAmount(p)] * Apply(BlendRule(q), BlendProperty(q))
	    }
	}

Depending on the precise computation in the blend rules functions for
every property ``q``, the ``APPLY`` operator may result in linear or
nonlinear terms being added to the constraint.