.. _sec:expr.num:

Numerical Expressions
=====================

.. rubric:: Constant numerical expressions

Like any expression in AIMMS, a numerical expression can either be a
*constant* or a *symbolic* expression. Constant expressions are those
that contain references to explicit set elements and values, but do not
contain references to other identifiers. Constant expressions are mostly
intended for the initialization of sets, parameters and variables. Such
an initialization must conform to one of the following formats:

-  a *scalar* value,

-  a *list* expression,

-  a *table* expression, or

-  a *composite table*.

Table expressions and composite tables are mostly used for data
initialization from *external* files. They are discussed in
:ref:`chap:text.data.file`.

.. rubric:: Symbolic numerical expressions

Symbolic expressions are those expressions that contain references to
other AIMMS identifiers. They can be used in the ``Definition``
attributes of sets, parameters and variables, or as the right-hand side
of assignment statements. AIMMS provides a powerful notation for
expressions, and complicated numerical manipulations can be expressed in
a clear and concise manner.

.. _numerical-expression:

.. rubric:: Syntax

*numerical-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 341.36503 347.20532"
	   height="347.20532"
	   width="341.36502"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,2280.2671)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><g
	         transform="scale(1.04294)"
	         id="g14"><path
	           id="path16"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><path
	         id="path18"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 340,14600 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g20"><text
	           id="text24"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,40.4,1456)"><tspan
	             id="tspan22"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path26"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 540,14600 50,-20 v 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 660,14600 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,71,1456)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1900.24,14600 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2020.24,14600 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,208.424,1456)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2220.24,14600 50,-20 v 40" /><g
	         transform="scale(1.04294)"
	         id="g48"><path
	           id="path50"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04417)"
	         id="g52"><path
	           id="path54"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 960.877,16280.8 -47.885,19.2 v -38.3" /></g><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,105.332,1696)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#constant">constant</a></tspan></text>
	</g><g
	         transform="scale(1.04417)"
	         id="g62"><path
	           id="path64"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1491.06,16280.8 47.88,-19.1 v 38.3" /></g><g
	         transform="scale(1.04294)"
	         id="g66"><path
	           id="path68"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><g
	         transform="scale(1.00736)"
	         id="g70"><path
	           id="path72"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 969.542,16280.1 -49.635,19.9 v -39.7" /></g><g
	         transform="scale(10)"
	         id="g74"><text
	           id="text78"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,102.668,1636)"><tspan
	             id="tspan76"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#reference">reference</a></tspan></text>
	</g><g
	         transform="scale(1.00736)"
	         id="g80"><path
	           id="path82"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1571.99,16280.1 49.63,-19.8 v 39.7" /></g><g
	         transform="scale(1.04294)"
	         id="g84"><path
	           id="path86"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04294)"
	         id="g88"><path
	           id="path90"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><g
	         transform="scale(1.02577)"
	         id="g92"><path
	           id="path94"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 796.146,16280.5 -48.744,19.5 v -39" /></g><g
	         transform="scale(10)"
	         id="g96"><text
	           id="text100"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,86.666,1666)"><tspan
	             id="tspan98"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#enumerated-list">enumerated-list</a></tspan></text>
	</g><g
	         transform="scale(1.02577)"
	         id="g102"><path
	           id="path104"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 1699.78,16280.5 48.75,-19.5 v 39" /></g><g
	         transform="scale(1.04294)"
	         id="g106"><path
	           id="path108"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04294)"
	         id="g110"><path
	           id="path112"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><path
	         id="path114"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 696.602,15800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g116"><text
	           id="text120"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,74.6602,1576)"><tspan
	             id="tspan118"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#operator-expression">operator-expression</a></tspan></text>
	</g><path
	         id="path122"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1863.64,15800 50,-20 v 40" /><g
	         transform="scale(1.04294)"
	         id="g124"><path
	           id="path126"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.17,-47.9 h 38.35" /></g><g
	         transform="scale(1.04294)"
	         id="g128"><path
	           id="path130"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><path
	         id="path132"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 910.02,16100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g134"><text
	           id="text138"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,96.002,1606)"><tspan
	             id="tspan136"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#function-call">function-call</a></tspan></text>
	</g><path
	         id="path140"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1650.22,16100 50,-20 v 40" /><g
	         transform="scale(1.04294)"
	         id="g142"><path
	           id="path144"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04294)"
	         id="g146"><path
	           id="path148"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><path
	         id="path150"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 709.98,15500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g152"><text
	           id="text156"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,75.998,1546)"><tspan
	             id="tspan154"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#iterative-expression">iterative-expression</a></tspan></text>
	</g><path
	         id="path158"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1850.26,15500 50,-20 v 40" /><g
	         transform="scale(1.04294)"
	         id="g160"><path
	           id="path162"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04294)"
	         id="g164"><path
	           id="path166"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><path
	         id="path168"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 750,14900 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g170"><text
	           id="text174"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,80,1486)"><tspan
	             id="tspan172"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/logical-expressions.html#logical-expression">logical-expression</a></tspan></text>
	</g><path
	         id="path176"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1810.24,14900 50,-20 v 40" /><g
	         transform="scale(1.04294)"
	         id="g178"><path
	           id="path180"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04294)"
	         id="g182"><path
	           id="path184"
	           style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 115.059,16300 -19.1766,-47.9 h 38.3526" /></g><path
	         id="path186"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 633.238,15200 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g188"><text
	           id="text192"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,68.3238,1516)"><tspan
	             id="tspan190"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#conditional-expression">conditional-expression</a></tspan></text>
	</g><path
	         id="path194"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1927,15200 50,-20 v 40" /><g
	         transform="scale(1.04294)"
	         id="g196"><path
	           id="path198"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2339.76,16300 -19.18,-47.9 h 38.35" /></g><g
	         transform="scale(1.04417)"
	         id="g200"><path
	           id="path202"
	           style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           d="m 2451.93,16280.8 -47.88,19.2 v -38.3" /></g><g
	         transform="scale(1.04908)"
	         id="g204"><path
	           id="path206"
	           style="fill:none;stroke:#000000;stroke-width:3.81287003;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	           d="m 0,16204.7 h 114.386 m 0,0 v -2192.4 c 0,-52.7 42.679,-95.3 95.322,-95.3 v 0 h 114.386 v 0 c 0,52.6 42.678,95.3 95.321,95.3 v 0 c 52.643,0 95.322,-42.7 95.322,-95.3 v 0 0 c 0,-52.7 -42.679,-95.4 -95.322,-95.4 v 0 c -52.643,0 -95.321,42.7 -95.321,95.4 v 0 m 190.643,0 h 114.386 v 95.3 H 1811.31 v -95.3 -95.4 H 629.123 v 95.4 m 1182.217,0 h 114.38 v 0 c 0,52.6 42.68,95.3 95.33,95.3 v 0 c 52.64,0 95.32,-42.7 95.32,-95.3 v 0 0 c 0,-52.7 -42.68,-95.4 -95.32,-95.4 v 0 c -52.65,0 -95.33,42.7 -95.33,95.4 v 0 m 190.65,0 h 114.38 v 0 c 52.65,0 95.33,42.6 95.33,95.3 v 2192.4 m -2211.694,0 h 95.322 632.287 114.386 v 95.3 h 527.699 v -95.3 -95.3 H 956.381 v 95.3 m 527.699,0 h 114.39 727.61 m -2211.694,0 v -476.6 c 0,-52.7 42.679,-95.4 95.322,-95.4 h 606.893 114.386 v 95.4 h 578.473 v -95.4 -95.3 H 930.987 v 95.3 m 578.483,0 h 114.39 606.89 c 52.65,0 95.33,42.7 95.33,95.4 v 476.6 m -2211.694,0 V 16014 c 0,-52.6 42.679,-95.3 95.322,-95.3 h 454.36 114.386 v 95.3 h 883.526 v -95.3 -95.3 H 778.454 v 95.3 m 883.556,0 h 114.39 454.35 c 52.65,0 95.33,42.7 95.33,95.3 v 190.7 m -2211.694,0 v -1048.6 c 0,-52.6 42.679,-95.3 95.322,-95.3 h 339.918 114.386 v 95.3 H 1776.43 v -95.3 -95.3 H 664.012 v 95.3 m 1112.438,0 h 114.39 339.92 c 52.64,0 95.32,42.7 95.32,95.3 v 1048.6 m -2211.694,0 v -762.6 c 0,-52.6 42.679,-95.3 95.322,-95.3 H 753.06 867.446 v 95.3 H 1573 v -95.3 -95.3 H 867.446 v 95.3 m 705.574,0 h 114.38 543.35 c 52.65,0 95.33,42.7 95.33,95.3 v 762.6 m -2211.694,0 v -1334.5 c 0,-52.7 42.679,-95.3 95.322,-95.3 h 352.671 114.386 v 95.3 H 1763.67 v -95.3 -95.4 H 676.765 v 95.4 m 1086.935,0 h 114.39 352.66 c 52.65,0 95.33,42.6 95.33,95.3 v 1334.5 m -2211.694,0 v -1906.5 c 0,-52.6 42.679,-95.3 95.322,-95.3 h 390.818 114.386 v 95.3 H 1725.52 v -95.3 -95.3 H 714.912 v 95.3 m 1010.638,0 h 114.38 390.82 c 52.65,0 95.33,42.7 95.33,95.3 v 1906.5 m -2211.694,0 v -1620.5 c 0,-52.6 42.679,-95.3 95.322,-95.3 h 279.519 114.386 v 95.3 H 1836.81 v -95.3 -95.3 H 603.613 v 95.3 m 1233.237,0 h 114.38 279.52 c 52.65,0 95.33,42.7 95.33,95.3 v 1620.5 h 114.38" /></g></g></g></svg></div>

.. _sec:expr.num.arith-ext:

Real Values and Arithmetic Extensions
-------------------------------------

.. _na:

.. _undf:

.. _inf:

.. _zero:

.. rubric:: Extension of the real line

Traditional arithmetic is defined on the real line,
:math:`\mathbb{R}=(-\infty,\infty)`, which does not contain either
:math:`+\infty` or :math:`-\infty`. AIMMS' arithmetic is defined on the
set :math:`\mathbb{R}\cup\{{}`\ ``-INF``, ``INF``, ``NA``, ``UNDF``,
``ZERO``\ :math:`{}\}` and summarized in :numref:`table:expr.arith-ext`.
The symbols ``INF`` and ``-INF`` are mostly used to model unbounded
variables. The symbols ``NA`` and ``UNDF`` stand for *not available* and
*undefined* data values respectively. The symbol ``ZERO`` denotes the
numerical value zero, but has the logical value true (not zero).

.. _table:expr.arith-ext:

.. table:: Extended values of the AIMMS language

   +----------+----------------------------------------------------------------------------+---------------+------------------------+
   | Symbol   | Description                                                                | Logical value | **\``MapVal`\`** value |
   +==========+============================================================================+===============+========================+
   | *number* | any valid real number                                                      |               | 0                      |
   +----------+----------------------------------------------------------------------------+---------------+------------------------+
   | ``UNDF`` | undefined (result of an arithmetic error)                                  | 1             | 4                      |
   +----------+----------------------------------------------------------------------------+---------------+------------------------+
   | ``NA``   | not available                                                              | 1             | 5                      |
   +----------+----------------------------------------------------------------------------+---------------+------------------------+
   | ``INF``  | :math:`+\infty`                                                            | 1             | 6                      |
   +----------+----------------------------------------------------------------------------+---------------+------------------------+
   | ``-INF`` | :math:`-\infty`                                                            | 1             | 7                      |
   +----------+----------------------------------------------------------------------------+---------------+------------------------+
   | ``ZERO`` | numerically indistinguishable from zero, but has the logical value of one. | 1             | 8                      |
   +----------+----------------------------------------------------------------------------+---------------+------------------------+

.. rubric:: Numerical behavior

AIMMS treats these special symbols as ordinary real numbers, and the
results of the available arithmetic operations and functions on these
symbols are defined. The values ``INF``, ``-INF`` and ``ZERO`` are
accessible by the user and are dealt with as expected:
:math:`1+{\texttt{INF}}` evaluates to ``INF``, :math:`1/{\texttt{INF}}`
to 0, :math:`1+{\texttt{ZERO}}` to 1, etc. However, the values of
``INF`` and ``-INF`` are undetermined and therefore, it makes no sense
to consider :math:`{\texttt{INF}}/{\texttt{INF}}`,
:math:`{\texttt{-INF}}+{\texttt{INF}}`, etc. These expressions are
therefore evaluated to ``UNDF``. A runtime error will occur if the value
``UNDF`` is assigned to an identifier.

.. rubric:: The symbol ``ZERO``

The symbol ``ZERO`` behaves like zero numerically, but its logical value
is one. Using this symbol, you can make a distinction between the
default value of 0 and an assigned ``ZERO``. As an illustration,
consider a distance matrix with distances between selected factory-depot
combinations. A missing distance value evaluates to 0, and could mean
that the particular factory-depot combination should not be considered.
A ``ZERO`` value in that case could be used to indicate that the
combination should be considered even though the corresponding distance
is zero because the depot and factory happen to be one facility.

.. rubric:: Expressions with 0 and ``ZERO``

Whenever the values 0 and ``ZERO`` appear in the same expression with
equal priority, the value of ``ZERO`` prevails. For example, the
expressions :math:`0+{\texttt{ZERO}}` or ``max``\ (0,\ ``ZERO``) will
both result in a numerical value of ``ZERO``. In this way, the logically
distinctive effect of ``ZERO`` is retained as long as possible. You
should note, however, that AIMMS will evaluate the multiplication of 0
with *any* special number to 0.

.. rubric:: The symbol ``NA``

The symbol ``NA`` can be used for missing data. The interpretation is
"this number is not yet known". Any operation that uses ``NA`` and does
not use the symbol ``UNDF`` will also produce the result ``NA``. AIMMS
can reason with this value as it propagates the value ``NA`` through its
computations and assignments. The only exception is the condition in
control flow statements where it must be known whether the result of
that condition is equal to ``0.0`` or not, see also
:ref:`sec:exec.flow`.

.. rubric:: The symbol ``UNDF``

The symbol ``UNDF`` cannot be input directly by a user, but is, besides
an error message, the result of an undefined or illegal arithmetic
operation. For example, ``1/ZERO``, ``0/0``, ``(-2)^0.1`` all result in
``UNDF``. Any operation containing the ``UNDF`` symbol evaluates to
``UNDF``.

.. _sec:expr.num.list:

List Expressions
----------------

.. rubric:: Element-value pairs

A *list* is a collection of *element-value pairs*. In a list a single
element or range of elements is combined with a numerical, element-, or
string-valued expression, separated by a *colon*. List expressions are
the numerical extension of enumerated set expressions. The elements to
which a value is assigned inside a list, are specified in exactly the
same manner as in an enumerated set expression as explained in
:ref:`sec:set-expr.set.enum`.

.. _enumerated-list:

.. rubric:: Syntax

*enumerated-list:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 508.68801 93.866661"
	   height="93.866661"
	   width="508.68799"
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
	         d="m 240,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,29,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">DATA</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 628,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,2000 -20,-50 h 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 748,2000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 868,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,93.2,196)"><tspan
	             id="tspan32"
	             y="0"
	             x="0">{</tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1068,2000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1308,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,135.8,196)"><tspan
	             id="tspan42"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#element-tuple">element-tuple</a></tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2134.96,2000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2254.96,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,231.896,196)"><tspan
	             id="tspan52"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2454.96,2000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2574.96,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,262.496,196)"><tspan
	             id="tspan62"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3255.16,2000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1188,2000 20,50 h -40" /><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2181.58,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g72"><text
	           id="text76"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,224.558,226)"><tspan
	             id="tspan74"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2381.58,2300 50,-20 v 40" /><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3375.16,2000 20,50 h -40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3495.16,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,355.916,196)"><tspan
	             id="tspan86"
	             y="0"
	             x="0">}</tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3695.16,2000 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3815.16,2000 -50,20 v -40" /><path
	         id="path94"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.773,100 100,100 h 188 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 340 c -55.227,0 -100,44.77 -100,100 v 0 m 388,0 h 120 m -628,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 154 120 154 c 55.227,0 100,44.77 100,100 v 200 h 120 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 120 m 0,0 v 0 h 120 v 100 h 826.94 V 2000 1900 H 1308 v 100 m 826.96,0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 680.19 v -100 -100 h -680.19 v 100 m 680.2,0 h 120 M 1188,2000 v 200 c 0,55.23 44.77,100 100,100 h 773.58 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120 773.58 c 55.23,0 100,-44.77 100,-100 v -200 h 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. _data:

.. rubric:: Constant versus symbolic

By preceding the list expression with the keyword ``DATA``, it becomes a
*constant* list expression, in a similar fashion as with constant set
expressions (see :ref:`sec:set-expr.set.enum`). In a constant list
expression, set elements need not be quoted and the assigned values must
be constants. All other list expressions are symbolic, in which both the
elements and the assigned values are the result of expression
evaluation.

.. rubric:: Example

The following assignments illustrate the use of list expressions.

-  The following constant list expression assigns distances to tuples of
   cities.

   .. code-block:: aimms
   
   	Distance(i,j) := DATA {
   	    (Amsterdam, Rotterdam  ) : 85 [km] ,
   	    (Amsterdam, 'The Hague') : 65 [km] ,
   	    (Rotterdam, 'The Hague') : 25 [km]
   	} ;

-  The following symbolic list expression assigns a certain status to
   every node in a number of dynamically computed ranges.

   .. code-block:: aimms
   
   	NodeUsage(i) := {
   	    FirstNode            .. FirstNode + Batch - 1   : 'InUse'   ,
   	    FirstNode + Batch    .. FirstNode + 2*Batch - 1 : 'StandBy' ,
   	    FirstNode + 2*Batch  .. LastNode                : 'Reserve'
   	} ;

.. _sec:expr.num.ref:

References
----------

.. rubric:: References

Sets, parameters and variables can be referred to by name resulting in a
set-, set element-, string-valued, or numerical quantity. A reference
can be scalar or multidimensional, and index positions may contain
either indices or element expressions. By specifying a case reference in
front, a reference can refer to data from cases that are not in memory.

.. _reference:

.. rubric:: Syntax

*reference:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 615.66402 93.866661"
	   height="93.866661"
	   width="615.664"
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
	         d="m 180,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,23,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#case-reference">case-reference</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1080.28,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1170.28,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,123.428,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">.</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1370.28,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 90,2000 -20,-50 h 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1460.28,2000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1550.28,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,160.028,196)"><tspan
	             id="tspan42"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#identifier-part">identifier-part</a></tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2350.48,2000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2530.48,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,259.448,196)"><tspan
	             id="tspan52"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2730.48,2000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2910.48,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,296.048,196)"><tspan
	             id="tspan62"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4057.48,2000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2820.48,2000 20,50 h -40" /><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3383.98,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g72"><text
	           id="text76"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,344.798,226)"><tspan
	             id="tspan74"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3583.98,2300 50,-20 v 40" /><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4147.48,2000 20,50 h -40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4237.48,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,430.148,196)"><tspan
	             id="tspan86"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4437.48,2000 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2440.48,2000 -20,-50 h 40" /><path
	         id="path94"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4527.48,2000 -20,-50 h 40" /><path
	         id="path96"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4617.48,2000 -50,20 v -40" /><path
	         id="path98"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 90 m 0,0 v 0 h 90 v 100 h 900.26 V 2000 1900 H 180 v 100 m 900.28,0 h 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 M 90,2000 v -200 c 0,-55.23 44.773,-100 100,-100 h 540.141 90 540.139 c 55.23,0 100,44.77 100,100 v 200 h 90 v 100 h 800.17 v -100 -100 h -800.17 v 100 m 800.2,0 h 90 m 0,0 v 0 h 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 m 0,0 v 0 h 90 v 100 H 4057.45 V 2000 1900 H 2910.48 v 100 m 1147,0 h 90 m -1327,0 v 200 c 0,55.23 44.77,100 100,100 h 373.5 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 373.5 c 55.23,0 100,-44.77 100,-100 v -200 h 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 m -2087,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 898.5 90 898.5 c 55.23,0 100,44.77 100,100 v 200 h 90" /></g></g></svg></div>

.. _identifier-part:

*identifier-part:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 485.92 80.533332"
	   height="80.533333"
	   width="485.91998"
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
	         d="m 360,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,41,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#module-prefix">module-prefix</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1186.84,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1306.84,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,135.684,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">::</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1550.84,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 240,2000 20,50 h -40" /><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1670.84,2000 20,50 h -40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,2000 -20,-50 h 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1790.84,2000 -20,-50 h 40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1910.84,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g44"><text
	           id="text48"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,196.084,196)"><tspan
	             id="tspan46"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path50"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2464.32,2000 50,-20 v 40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2704.32,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g54"><text
	           id="text58"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,276.832,196)"><tspan
	             id="tspan56"
	             y="0"
	             x="0">.</tspan></text>
	</g><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2904.32,2000 50,-20 v 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3024.32,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,307.432,196)"><tspan
	             id="tspan66"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#suffix">suffix</a></tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3404.4,2000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2584.32,2000 -20,-50 h 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3524.4,2000 -20,-50 h 40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3644.4,2000 -50,20 v -40" /><path
	         id="path78"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 826.82 V 2000 1900 H 360 v 100 m 826.84,0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 M 240,2000 v 200 c 0,55.23 44.773,100 100,100 h 555.422 119.998 555.42 c 55.23,0 100,-44.77 100,-100 v -200 h 120 M 120,2000 v -200 c 0,-55.23 44.773,-100 100,-100 h 675.422 119.998 675.42 c 55.23,0 100,44.77 100,100 v 200 h 120 v 100 h 553.46 v -100 -100 h -553.46 v 100 m 553.48,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 380.07 v -100 -100 h -380.07 v 100 m 380.08,0 h 120 m -940.08,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 310.04 120 310.04 c 55.23,0 100,44.77 100,100 v 200 h 120" /></g></g></svg></div>

.. rubric:: Scalar versus indexed

A *scalar* set, parameter or variable has no indexing (dimension) and is
referenced simply by using its identifier. Indexed sets, parameters and
variables have dimensions equal to the number of indices.

.. rubric:: Example

The right-hand sides of the following assignments are examples of
references to scalar and indexed identifiers.

.. code-block:: aimms

	MainCity                := 'Amsterdam' ;

	DistanceFromMainCity(i) := Distance( MainCity, i );

	SecondNextCity(i)       := NextCity( NextCity(i) );

	NextPeriodStock(t)      := Stock( t + 1 );

.. rubric:: Undefined references

The last two references, which make use of lag and lead operators and
element parameters, may sometimes be undefined. When used in an
expression such undefined references evaluate to the empty set, zero,
the empty element, or the empty string, depending on the value type of
the identifier. When an undefined lag or lead operator or element
parameter occurs on the left-hand side of an assignment, the assignment
is skipped. For more details, refer to :ref:`sec:exec.assign`.

.. _module-prefix:

.. rubric:: Referring to module identifiers

When your model contains one or more ``Modules``, your model will be
supplied multiple additional namespaces besides the global namespace,
one for each module. Identifiers declared within a module are, by
default, not contained in the global namespace. To refer to such
identifiers outside the module, you have to prefix the identifier name
with a module-specific prefix and the ``::`` namespace resolution
operator. ``Modules`` and the namespace resolution operator are
discussed in full detail in :ref:`sec:module.module`.

.. rubric:: Referring to other cases
   :name: case.reference

.. _case-reference:

When a reference is preceded by a *case reference*, AIMMS will not
retrieve the requested identifier data from the case in memory, but from
the case file associated with the case reference. Case references are
elements of the (predefined) set :any:`AllCases`, which contains all the
cases available in the data manager of AIMMS. The AIMMS `User's Guide <https://documentation.aimms.com/_downloads/AIMMS_user.pdf>`__
describes all the mechanisms that are available and functions that you
can use to let an end-user of your application select one or more cases
from the set of all available cases. Case referencing is useful when you
want to perform advanced case comparison over multiple cases.

.. rubric:: Example

The following computes the differences of the values of the variable
``Transport`` in the current case compared to its values in all cases in
the set :any:`CurrentCaseSelection`.

.. code-block:: aimms

	for ( c in CurrentCaseSelection ) do
	    Difference(c,i,j) := c.Transport(i,j) - Transport(i,j) ;
	endfor;

During execution, AIMMS will (temporarily) retrieve the values of
``Transport`` from all requested cases to compute the difference with
the data of the current case.

.. _sec:expr.num.functions:

Arithmetic Functions
--------------------

.. rubric:: Standard functions

AIMMS provides the commonly used standard arithmetic functions such as
the trigonometric functions, logarithms, and exponentiations.
:numref:`table:expr.num-func` lists the available arithmetic functions
with their arguments and result, where :math:`x` is an extended range
arithmetic expressions, :math:`m`, :math:`n` are integer expressions,
:math:`i` is an index, :math:`l` is a set element, :math:`I` is a set
identifier, and :math:`e` is a scalar reference.

.. _table:expr.num-func:

.. table:: Intrinsic numerical functions of AIMMS

   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | Function                                 | Meaning                                                                                                      |
   +==========================================+==============================================================================================================+
   | :any:`Abs`:math:`(x)`                    | absolute value :math:`|x|`                                                                                   |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Exp`:math:`(x)`                    | :math:`e^x`                                                                                                  |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Log`:math:`(x)`                    | :math:`\log_e(x)` for :math:`x>0`,\ ``UNDF`` otherwise                                                       |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Log10`:math:`(x)`                  | :math:`\log_{10}(x)` for :math:`x>0`, ``UNDF`` otherwise                                                     |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Max`:math:`(x_1,\dots,x_n)`        | :math:`\max(x_1,\dots,x_n)\quad (n>1)`                                                                       |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Min`:math:`(x_1,\dots,x_n)`        | :math:`\min(x_1,\dots,x_n)\quad (n>1)`                                                                       |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Mod`:math:`(x_1,x_2)`              | :math:`x_1 \bmod {x_2} \in [0,x_2)` for :math:`x_2 > 0` or :math:`\in(x_2,0]` for :math:`x_2<0`              |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Div`:math:`(x_1,x_2)`              | :math:`x_1\;\mathrm{div}\;{x_2}`                                                                             |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Sign`:math:`(x)`                   | :math:`\mathrm{sign}(x)=+1` if :math:`x>0`, :math:`-1` if :math:`x<0` and :math:`0` if :math:`x=0`           |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Sqr`:math:`(x)`                    | :math:`x^2`                                                                                                  |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Sqrt`:math:`(x)`                   | :math:`\sqrt x` for :math:`x\geq0`, ``UNDF`` otherwise                                                       |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Power`:math:`(x_1,x_2)`            | :math:`x_1^{x_2}`, alternative for ``x`` (see :ref:`sec:expr.operators`)                                     |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ErrorF`:math:`(x)`                 | :math:`{\frac{1}{\sqrt{2\pi}}}\int_{-\infty}^x e^{-{\frac{t^2}{2}}}\, dt`                                    |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Cos`:math:`(x)`                    | :math:`\cos(x)`; :math:`x` in radians                                                                        |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Sin`:math:`(x)`                    | :math:`\sin(x)`; :math:`x` in radians                                                                        |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Tan`:math:`(x)`                    | :math:`\tan(x)`; :math:`x` in radians                                                                        |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ArcCos`:math:`(x)`                 | :math:`\mathrm{arccos}(x)`; result in radians                                                                |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ArcSin`:math:`(x)`                 | :math:`\mathrm{arcsin}(x)`; result in radians                                                                |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ArcTan`:math:`(x)`                 | :math:`\mathrm{arctan}(x)`; result in radians                                                                |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Degrees`:math:`(x)`                | converts :math:`x` from radians to degrees                                                                   |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Radians`:math:`(x)`                | converts :math:`x` from degrees to radians                                                                   |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Cosh`:math:`(x)`                   | :math:`\cosh(x)`                                                                                             |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Sinh`:math:`(x)`                   | :math:`\sinh(x)`                                                                                             |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Tanh`:math:`(x)`                   | :math:`\tanh(x)`                                                                                             |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ArcCosh`:math:`(x)`                | :math:`\mathrm{arccosh}(x)`                                                                                  |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ArcSinh`:math:`(x)`                | :math:`\mathrm{arcsinh}(x)`                                                                                  |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`ArcTanh`:math:`(x)`                | :math:`\mathrm{arctanh}(x)`                                                                                  |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Card`:math:`(I[,\mathit{suffix}])` | cardinality of (suffix of) set, parameter or variable :math:`I`                                              |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Ord`:math:`(i)`                    | ordinal number of index :math:`i` in set :math:`I` (see also :numref:`table:set-expr.set-func`)              |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Ord`:math:`(l[,I])`                | ordinal number of element :math:`l` in set :math:`I`                                                         |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Ceil`:math:`(x)`                   | :math:`\lceil x \rceil = \text{smallest integer} \geq x`                                                     |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Floor`:math:`(x)`                  | :math:`\lfloor x \rfloor = \text{largest integer} \leq x`                                                    |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Precision`:math:`(x,n)`            | :math:`x` rounded to :math:`n` significant digits                                                            |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Round`:math:`(x)`                  | :math:`x` rounded to nearest integer                                                                         |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Round`:math:`(x,n)`                | :math:`x` rounded to :math:`n` decimal places left (:math:`n<0`) or right (:math:`n>0`) of the decimal point |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`Trunc`:math:`(x)`                  | truncated value of :math:`x`: :any:`Sign`:math:`(x)*`:any:`Floor`:math:`(`:any:`Abs`:math:`(x))`             |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :math:`\mathtt{NonDefault}(e)`           | :math:`1` if :math:`e` is not at its default value, :math:`0` otherwise                                      |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :any:`MapVal`:math:`(x)`                 | :any:`MapVal` value of :math:`x` according to :numref:`table:expr.arith-ext`                                 |
   +------------------------------------------+--------------------------------------------------------------------------------------------------------------+

.. rubric:: Functions and extended arithmetic

Special caution is required when one or more of the arguments in the
functions are special symbols of AIMMS' extended range arithmetic. If
the value of any of the arguments is ``UNDF`` or ``NA``, then the result
will also be ``UNDF`` or ``NA``. If the value of any of the arguments is
``ZERO`` and the numerical value of the result is zero, the function
will return ``ZERO``.

.. _sec:expr.operators:

Numerical Operators
-------------------

Using unary or binary numerical operators you can construct numerical
expressions that consist of multiple terms and/or factors. The syntax
follows.

.. _operator-expression:

.. rubric:: Syntax

*operator-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 399.2 67.199997"
	   height="67.199997"
	   width="399.19998"
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
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 240,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,29,296)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 920.199,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1040.2,3000 -50.001,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,109.02,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#binary-operator">binary-operator</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1953.8,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2073.8,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,212.38,296)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2754,3000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,3000 -20,-50 h 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 653.418,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,70.3418,266)"><tspan
	             id="tspan50"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#unary-operator">unary-operator</a></tspan></text>
	</g><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1540.38,2700 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1660.38,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g58"><text
	           id="text62"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,171.038,266)"><tspan
	             id="tspan60"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2340.58,2700 50,-20 v 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2874,3000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2994,3000 -50,20 v -40" /><path
	         id="path70"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 m 0,0 v 0 h 120 v 100 H 920.188 V 3000 2900 H 240 v 100 m 680.199,0 H 1040.2 v 100 h 913.57 V 3000 2900 H 1040.2 v 100 m 913.6,0 h 120 v 100 h 680.19 V 3000 2900 H 2073.8 v 100 m 680.2,0 h 120 m -2754,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 313.418 120 v 100 H 1540.36 V 2700 2600 H 653.418 v 100 m 886.962,0 h 120 v 100 h 680.19 v -100 -100 h -680.19 v 100 m 680.2,0 h 120 313.42 c 55.23,0 100,44.77 100,100 v 200 h 120" /></g></g></svg></div>

.. _binary-operator:

.. _unary-operator:

.. rubric:: Standard numerical operators

The order of precedence of the standard numerical operators in AIMMS is
given in :numref:`table:expr.num-oper`. Parentheses may be used to
override the precedence order. Expression evaluation is from left to
right.

.. _table:expr.num-oper:

.. table:: Numerical operators

   +----------+----------------+------------+
   | Operator | Meaning        | Precedence |
   +==========+================+============+
   | *Unary*                                |
   +----------+----------------+------------+
   | ``+``    | positive       | n/a        |
   +----------+----------------+------------+
   | ``-``    | negative       | n/a        |
   +----------+----------------+------------+
   | *Binary*                               |
   +----------+----------------+------------+
   | ``^``    | exponentiation | 3 (high)   |
   +----------+----------------+------------+
   | ``*``    | multiplication | 2          |
   +----------+----------------+------------+
   | ``/``    | division       | 2          |
   +----------+----------------+------------+
   | ``+``    | addition       | 1          |
   +----------+----------------+------------+
   | ``-``    | subtraction    | 1 (low)    |
   +----------+----------------+------------+

.. rubric:: Example

The expression

.. code-block:: aimms

	p1 + p2 * p3 / p4^p5

is parsed by AIMMS as if it had been written

.. code-block:: aimms

	p1 + [(p2 * p3) / (p4^p5)]

In general, it is better to use parentheses than to rely on the
precedence and associativity of the operators. Not only because it
prevents you from making unwanted mistakes, but also because it makes
your intentions clearer.

.. rubric:: Exponential operator

Special restrictions apply to the exponential operator ``^``. AIMMS
accepts the following combinations of left-hand side operand (called the
*base*), and right-hand side operand (called the *exponent*):

-  a positive base with a real exponent,

-  a negative base with an integer exponent,

-  a zero base with a positive exponent, and

-  a zero base with a zero exponent results in one (as controlled by the
   option ``power_0_0``).

.. _sec:expr.num.iter:

Numerical Iterative Operators
-----------------------------

.. _Sum:

.. _Prod:

.. _Count:

.. rubric:: Arithmetic iterative operators

Iterative operators are used to express repeated arithmetic operations,
such as summation, in a concise manner. The arithmetic iterative
operators supported by AIMMS are listed in
:numref:`table:expr.num-iter`. The second column in this table refers to
the required number of expression arguments following the binding domain
argument, while the last column refers to the result of the operator in
case of an empty domain.

.. _table:expr.num-iter:

.. table:: Arithmetic iterative operators

   ========== ======= ========================================== ========
   Name       # Expr. Computes over all elements in the domain   Default
   ========== ======= ========================================== ========
   ``Sum``    1       the sum of the expression                  0
   ``Prod``   1       the product of the expression              1
   ``Count``  0       the total number of elements in the domain 0
   :any:`Min` 1       the minimum value of the expression        ``INF``
   :any:`Max` 1       the maximum value of the expression        ``-INF``
   ========== ======= ========================================== ========

.. rubric:: Compared expressions

The :any:`Min` and :any:`Max` operators return the minimum or maximum value of
an expression. The allowed expressions are:

-  numerical expressions, in which case AIMMS returns the lowest or
   highest numerical values,

-  string expressions, in which case AIMMS returns the strings which are
   first or last with respect to the normal alphabetic ordering, and

-  element expressions, in which case AIMMS returns the elements with
   the lowest or highest ordinal numbers (see also
   :ref:`sec:set-expr.elem.functions`).

.. rubric:: Example

The following assignments are valid examples of the use of the
arithmetic iterative operators.

.. code-block:: aimms

	NumberOfRoutes      := Count( (i,j) | Distance(i,j) ) ;
	NettoTransport(i)   := Sum( j, Transport(i,j) - Transport(j,i) ) ;
	MaximumTransport(i) := Max( j, Transport(i,j) ) ;

.. _sec:expr.stat:

Statistical Functions and Operators
-----------------------------------

.. rubric:: Distributions

AIMMS provides the most commonly used distributions. They are listed in
:numref:`table:expr.distrib`, together with the required type of
arguments and a description of the result. You can find a more detailed
description of these distributions in :ref:`app:distribution.discrete`
and :ref:`app:distribution.cont`. When called as functions inside your
model, they behave as random number generators.

.. _table:expr.distrib:

.. table:: Distributions available in AIMMS

   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Distribution                                  | Meaning                                                                                                                                           |
   +===============================================+===================================================================================================================================================+
   | :any:`Binomial`:math:`(p,n)`                  | Binomial distribution with probability :math:`p` and number of trials :math:`n`                                                                   |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`NegativeBinomial`:math:`(p,r)`          | Negative Binomial distribution with probability :math:`p` and number of successes :math:`r`                                                       |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Poisson`:math:`(\lambda)`               | Poisson distribution with rate :math:`\lambda`                                                                                                    |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Geometric`:math:`(p)`                   | Geometric distribution with probability :math:`p`                                                                                                 |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`HyperGeometric`:math:`(p,n,N)`          | Hypergeometric distribution with initial probability of success :math:`p`, number of trials :math:`n` and population size :math:`N`               |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Uniform`:math:`({min,max})`             | Uniform distribution with lower bound min and upper bound max                                                                                     |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Triangular`:math:`(\beta,{min},{max})`  | Triangular distribution with shape :math:`\beta`, lower bound min, and upper bound max, where :math:`\beta=(x_{\text{peak}}-{min})/({max}-{min})` |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Beta`:math:`(\alpha,\beta,{min},{max})` | Beta distribution with shapes :math:`\alpha`, :math:`\beta`, lower bound min, and upper bound max                                                 |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`LogNormal`:math:`(\beta,{min},s)`       | Lognormal distribution with shape :math:`\beta`, lower bound min, and scale :math:`s`                                                             |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Exponential`:math:`({min},s)`           | Exponential distribution with lower bound min and scale :math:`s`                                                                                 |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Gamma`:math:`(\beta,{min},s)`           | Gamma distribution with shape :math:`\beta`, lower bound min, and scale :math:`s`                                                                 |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Weibull`:math:`(\beta,{min},s)`         | Weibull distribution with shape :math:`\beta`, lower bound min, and scale :math:`s`                                                               |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Pareto`:math:`(\beta,l,s)`              | Pareto distribution with shape :math:`\beta`, location :math:`l`, and scale :math:`s` (:math:`\text{lower bound} = l + s`)                        |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Normal`:math:`(\mu,\sigma)`             | Normal distribution with mean :math:`\mu` and standard deviation :math:`\sigma`                                                                   |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Logistic`:math:`(\mu,s)`                | Logistic distribution with mean :math:`\mu` and scale :math:`s`                                                                                   |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`ExtremeValue`:math:`(l,s)`              | Extreme Value distribution with location :math:`l` and scale :math:`s`                                                                            |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rubric:: Setting the seed

You can set the seed of the random number generators for all
distributions using the execution option ``seed``. By setting the seed
explicitly you can guarantee that your model results are reproducible.

.. _cumulativedistribution:

.. _inversecumulativedistribution:

.. rubric:: Cumulative distributions and their derivatives

Each distribution in :numref:`table:expr.distrib` can be used as an
argument for four operators: :any:`DistributionCumulative` and
:any:`DistributionInverseCumulative`, and their derivatives
:any:`DistributionDensity` and :any:`DistributionInverseDensity`. In the
explanation below it is assumed that :math:`\alpha \in [0,1]`,
:math:`x \in (-\infty,\infty)`, and :math:`X` a random variable
distributed according to the given distribution *distr*.

-  :any:`DistributionCumulative`\ (*distr*,\ :math:`x`) computes the
   probability :math:`P(X\leq x)`.

-  :any:`DistributionInverseCumulative`\ (*distr*,\ :math:`\alpha`)
   computes the smallest :math:`x` such that the probability
   :math:`P(X\leq x) \geq \alpha`, except for :math:`\alpha = 0` which
   returns the lowest possible value for :math:`X`.

-  :any:`DistributionDensity`\ (*distr*,\ :math:`x`) computes for
   continuous distributions the probability density
   :math:`\lim_{\alpha \downarrow 0}P(x
   \leq X\leq x+\alpha)/\alpha`. For discrete distributions, the
   operator is only defined for integer values of :math:`x` and returns
   :math:`P(X = x)`.

-  :any:`DistributionInverseDensity`\ (*distr*,\ :math:`\alpha`) is the
   derivative of :any:`DistributionInverseCumulative`. For more details you
   are referred to :ref:`app:distribution.stat`.

.. rubric:: Use in constraints

For the continuous distributions in :numref:`table:expr.distrib`, AIMMS
can compute the derivatives of the cumulative and inverse cumulative
distribution functions. As a consequence, you may use these functions in
the constraints of a nonlinear model when the second argument is a
variable.

.. rubric:: Example

The following statements demonstrate how the distributions can be used
to perform statistical tasks.

#. Draw a random number from a distribution.

   .. code-block:: aimms
   
   	Draw := Normal(0,1);
   	Draw := Uniform(LowestValue, HighestValue);

#. Compute the probability of at most 10 successes out of 50 trials,
   with a 0.25 probability of success.

   .. code-block:: aimms
   
   	Probability := DistributionCumulative( Binomial(0.25,50), 10 );

#. Compute a two-sided 90% confidence interval of a Normal(0,1)
   distribution.

   .. code-block:: aimms
   
   	LeftBound  := DistributionInverseCumulative( Normal(0,1), 0.05);
   	RightBound := DistributionInverseCumulative( Normal(0,1), 0.95);

.. rubric:: Statistical operators

The distributions, listed in :numref:`table:expr.distrib`, make it
possible for you to execute a stochastic experiment based on your model
representation. In order to analyze the subsequent results, AIMMS
provides a number of statistical iterative operators which are listed in
:numref:`table:expr.stat-iter`. The second column in this table refers
to the required number of expression arguments following the binding
domain argument. For the most common sample operators, AIMMS provides
distribution operators to calculate the corresponding expected values,
assuming the sample is drawn from a given distribution. These
distribution operators are listed in :numref:`table:expr.distrib-oper`.
A more detailed description of these operators is provided in
:ref:`app:distribution`.

.. _table:expr.stat-iter:

.. table:: Statistical sample operators

   ======================= ======= ========================================
   Name                    # Expr. Computes over all elements in the domain
   ======================= ======= ========================================
   ``Mean``                1       the (arithmetic) mean
   ``GeometricMean``       1       the geometric mean
   ``HarmonicMean``        1       the harmonic mean
   ``RootMeanSquare``      1       the root mean square
   ``Median``              1       the median
   ``SampleDeviation``     1       the standard deviation of a sample
   ``PopulationDeviation`` 1       the standard deviation of a population
   ``Skewness``            1       the coefficient of skewness
   ``Kurtosis``            1       the coefficient of kurtosis
   ``Correlation``         2       the correlation coefficient
   ``RankCorrelation``     2       the rank correlation coefficient
   ======================= ======= ========================================

.. _table:expr.distrib-oper:

.. table:: Statistical distribution operators

   +------------------------------+--------------------------------------------+
   | Name                         | Computes for a given distribution          |
   +==============================+============================================+
   | :any:`DistributionMean`      | the (arithmetic) mean                      |
   +------------------------------+--------------------------------------------+
   | :any:`DistributionDeviation` | the (standard) deviation                   |
   +------------------------------+--------------------------------------------+
   | :any:`DistributionVariance`  | the variance (the square of the deviation) |
   +------------------------------+--------------------------------------------+
   | :any:`DistributionSkewness`  | the coefficient of skewness                |
   +------------------------------+--------------------------------------------+
   | :any:`DistributionKurtosis`  | the coefficient of kurtosis                |
   +------------------------------+--------------------------------------------+

.. rubric:: Example

Assume that ``p`` is an index into a set that has been used to index a
number of experiments resulting in observables ``x(p)`` and ``y(p)``.
Then the following assignments demonstrate the use of the statistical
operators in AIMMS.

.. code-block:: aimms

	MeanX         := Mean(p, x(p));
	MeanX         := Mean(p | x(p), x(p));
	DeviationX    := SampleDeviation(p, x(p));
	CorrelationXY := Correlation(p, x(p), y(p));

In case the :math:`x` values are drawn from a ``Binomial(0.6,8)``
distribution the expected value of ``MeanX`` is given by

.. code-block:: aimms

	ExpectedMeanX := DistributionMean(Binomial(0.6,8));

.. rubric:: Units of measurement

For all distributions, the units of measurement (see also
:ref:`chap:units`) of parameters and result should be consistent. The
unit relationships for each distribution are described in
:ref:`app:distribution` in full detail. In the presence of units of
measurement within your model, AIMMS will perform a unit consistency
check.

.. rubric:: Histogram support

For easy visualization of statistical data, AIMMS offers support for
creating histograms based on a large collection of observed values.
Through a number of predefined procedures and functions, AIMMS allows
you to flexibly create interval-based histogram data, which can easily
be displayed, for instance, using the standard (graphical) AIMMS bar
chart object. For further information about creating and displaying
histograms, as well as an illustrative example, you are referred to
:ref:`sec:gui.histogram` in the Appendix.

.. rubric:: Combinatoric functions

In addition to the distribution and statistical operators listed above,
AIMMS also offers support for the most common combinatoric calculations.
:numref:`table:expr.combinatoric` contains the list of combinatoric
functions that are available in AIMMS.

.. _permutation-LR:

.. _combination-LR:

.. _factorial-LR:

.. _table:expr.combinatoric:

.. table:: Combinatoric functions

   =============================== =============================
   Function                        Meaning
   =============================== =============================
   :any:`Factorial`:math:`(n)`     :math:`n!`
   :any:`Combination`:math:`(n,m)` :math:`\binom{n}{m}`
   :any:`Permutation`:math:`(n,m)` :math:`m!\cdot{\binom{n}{m}}`
   =============================== =============================

.. _sec:expr.financial:

Financial Functions
-------------------

.. rubric:: Financial functions
   :name: finance.func

AIMMS provides an extensive library of financial functions for a variety
of financial applications. The available functions can be classified as
follows.

-  Functions for the computation of the depreciation of assets using
   various methods such as fixed-declining balance method,
   double-declining balance method, etc.

-  Functions for computing various quantities regarding investments that
   consist of a series of constant or variable periodic cash flows. The
   computed quantities include present value, net present value, future
   value, internal rate of return, interest and principal payments, etc.

-  Functions for computing various security-related quantities of, for
   instance, discounted securities, securities that pay periodic
   interest and securities that pay interest at maturity. The computed
   quantities include yield, interest rate, redemption, price, accrued
   interest, etc.

.. rubric:: Consult the online function reference

The precise description of all financial functions available in AIMMS is
not included in this Language Reference. A complete list of
the available financial functions can be found in :ref:`chap:finance-intro` of the AIMMS `Function Reference <https://documentation.aimms.com/functionreference/>`__.
The `Function Reference <https://documentation.aimms.com/functionreference/>`__ provides
a description as well as the prototype of every financial function
present in AIMMS.

.. _sec:expr.cond:

Conditional Expressions
-----------------------

.. rubric:: Two conditional expressions

There are two ways to specify expressions that adopt different values
depending on one or more logical conditions. The ``ONLYIF`` operator is
the simpler and operates as it sounds. The ``IF-THEN-ELSE`` expression
is more powerful in its ability to distinguish several cases.

.. _conditional-expression:

.. rubric:: Syntax

*conditional-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 265.82401 67.199997"
	   height="67.199997"
	   width="265.82401"
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
	         d="m 120,3000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 340,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,39,266)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#if-then-else-expression">if-then-else-expression</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1653.68,2700 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1873.68,3000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 496.719,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,54.6719,296)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#onlyif-expression">onlyif-expression</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1496.96,3000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1993.68,3000 -50,20 v -40" /><path
	         id="path40"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 m 0,0 v -200 c 0,-55.23 44.773,-100 100,-100 v 0 h 120 v 100 H 1653.64 V 2700 2600 H 340 v 100 m 1313.68,0 h 120 v 0 c 55.23,0 100,44.77 100,100 v 200 M 120,3000 h 100 156.719 120 v 100 H 1496.93 V 3000 2900 H 496.719 v 100 m 1000.241,0 h 120 256.72 120" /></g></g></svg></div>

.. rubric:: The ``ONLYIF`` operator

The simplest way of specifying a conditional expression is to use the
``ONLYIF`` operator. Its syntax is given by

.. _onlyif-expression:

*onlyif-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 398.99202 67.199997"
	   height="67.199997"
	   width="398.992"
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
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,296)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 800.199,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1040.2,3000 -50.001,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,109.02,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">ONLYIF</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1572.2,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 920.199,3000 -20,-50 h 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1206.2,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,127.02,266)"><tspan
	             id="tspan40"
	             y="0"
	             x="0">$</tspan></text>
	</g><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1406.2,2700 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1692.2,3000 -20,-50 h 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1812.2,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,186.22,296)"><tspan
	             id="tspan52"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/logical-expressions.html#logical-expression">logical-expression</a></tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2872.44,3000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2992.44,3000 -50,20 v -40" /><path
	         id="path60"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 v 100 H 800.188 V 3000 2900 H 120 v 100 m 680.199,0 h 120 m 0,0 v 0 H 1040.2 v 0 c 0,55.23 44.77,100 100,100 h 332 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -332 c -55.23,0 -100,44.77 -100,100 v 0 m 532,0 h 120 m -772.001,0 v -200 c 0,-55.23 44.774,-100 100.001,-100 h 66 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 66 c 55.23,0 100,44.77 100,100 v 200 h 120 v 100 H 2872.41 V 3000 2900 H 1812.2 v 100 m 1060.24,0 h 120" /></g></g></svg></div>

The ``ONLYIF`` expression evaluates to the arithmetic expression in the
first argument if the logical condition of the second argument is true.
Otherwise, it is zero. The ``$`` symbol can be used as a synonym for
the ``ONLYIF`` operator.

.. rubric:: Example

A simple example of the use of the ``ONLYIF`` operator is given by the
assignment

.. code-block:: aimms

	AverageVelocity := (Distance / TravelTime) ONLYIF TravelTime ;

or equivalently, using the ``$`` operator,

.. code-block:: aimms

	AverageVelocity := (Distance / TravelTime) $ TravelTime ;

Both expressions evaluate to ``Distance / TravelTime`` if ``TravelTime``
assumes a nonzero value, or to zero otherwise. In
:ref:`sec:sparse.modifier.binary` you will see that this particular
expression can be written even more concisely using the sparsity
modifier ``$``.

.. rubric:: ``IF-THEN-ELSE`` expressions

A much more flexible way for specifying conditional expressions is given
by the ``IF-THEN-ELSE`` operator. The syntax of the ``IF-THEN-ELSE``
expression is given below.

.. _if-then-else-expression:

.. rubric:: Syntax

*if-then-else-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 505.09334 160.53333"
	   height="160.53333"
	   width="505.09332"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,786.93331)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,546)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">IF</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 364,5500 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 604,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,65.4,546)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/logical-expressions.html#logical-expression">logical-expression</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1664.24,5500 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1784.24,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,183.424,546)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">THEN</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2172.24,5500 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2292.24,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,234.224,546)"><tspan
	             id="tspan48"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2972.44,5500 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 484,5500 20,50 h -40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1522.22,5800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g58"><text
	           id="text62"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,157.222,576)"><tspan
	             id="tspan60"
	             y="0"
	             x="0">ELSEIF</tspan></text>
	</g><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2054.22,5800 50,-20 v 40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3092.44,5500 20,50 h -40" /><path
	         id="path68"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 3212.44,5500 h 240" /><path
	         id="path70"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 1300,5000 h 240" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1780,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g74"><text
	           id="text78"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,183,496)"><tspan
	             id="tspan76"
	             y="0"
	             x="0">ELSE</tspan></text>
	</g><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2168,5000 50,-20 v 40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2288,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,233.8,496)"><tspan
	             id="tspan86"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2968.2,5000 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1660,5000 -20,-50 h 40" /><path
	         id="path94"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3088.2,5000 -20,-50 h 40" /><path
	         id="path96"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3208.2,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g98"><text
	           id="text102"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,325.82,496)"><tspan
	             id="tspan100"
	             y="0"
	             x="0">ENDIF</tspan></text>
	</g><path
	         id="path104"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3668.2,5000 50,-20 v 40" /><path
	         id="path106"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3788.2,5000 -50,20 v -40" /><path
	         id="path108"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5500 h 120 v 0 c 0,55.23 44.773,100 100,100 h 44 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 h -44 c -55.227,0 -100,44.77 -100,100 v 0 m 244,0 h 120 m 0,0 v 0 h 120 v 100 H 1664.21 V 5500 5400 H 604 v 100 m 1060.24,0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 188 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 h -188 c -55.23,0 -100,44.77 -100,100 v 0 m 388,0 h 120 v 100 h 680.19 v -100 -100 h -680.19 v 100 m 680.2,0 h 120 M 484,5500 v 200 c 0,55.23 44.773,100 100,100 h 818.22 120 v 0 c 0,55.23 44.77,100 100,100 h 332 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -332 c -55.23,0 -100,44.77 -100,100 v 0 m 532,0 h 120 818.22 c 55.22,0 100,-44.77 100,-100 v -200 h 120 M 1540,5000 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 188 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -188 c -55.23,0 -100,44.77 -100,100 v 0 m 388,0 h 120 v 100 h 680.19 V 5000 4900 H 2288 v 100 m 680.2,0 h 120 m -1428.2,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 554.1 120 554.1 c 55.23,0 100,44.77 100,100 v 200 h 120 v 0 c 0,55.23 44.77,100 100,100 h 260 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -260 c -55.23,0 -100,44.77 -100,100 v 0 m 460,0 h 120" /></g></g></svg></div>

.. rubric:: Explanation

The ``IF-THEN-ELSE`` expression works like a *switch statement*-a series
of ``ELSEIF``\ s can be used to denote numerous special cases. The value
of the ``IF-THEN-ELSE`` expression is the first numerical expression for
which the corresponding logical condition is true. If none of the
conditions are true, then the value will be the numerical expression
after the ``ELSE`` keyword if present or zero otherwise.

.. rubric:: Example

A simple illustration of the use of the ``IF-THEN-ELSE`` construction is
given by the assignments

.. code-block:: aimms

	AverageVelocity := IF TravelTime THEN Distance / TravelTime ENDIF ;

which is equivalent to the ``ONLYIF`` expression above. A more elaborate
example is given by the assignment

.. code-block:: aimms

	WeightedDistance(i) :=
	    IF     Distance(i) <= 100 THEN Distance(i)
	    ELSEIF Distance(i) <= 200 THEN (100 + Distance(i)) / 2
	    ELSEIF Distance(i) <= 300 THEN (250 + Distance(i)) / 3
	    ELSE   550 / 3
	    ENDIF ;

The expression takes the value associated with the first logical
expression that is true.