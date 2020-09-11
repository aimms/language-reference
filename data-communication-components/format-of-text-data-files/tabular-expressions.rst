.. _sec:text.table:

Tabular Expressions
===================

.. rubric:: Tables for initialization

For multidimensional quantities the table format often provides the most
natural structure for data entry because elements are repeated less
often. Tables can be used in text data files and in the ``InitialData``
attribute inside the declaration of an identifier.

.. rubric:: Two-dimensional views

A table is a two-dimensional view of a multidimensional quantity. The
index tuple of the quantity is split into two parts: row identifiers and
column identifiers. Indices may not be permuted.

.. rubric:: Example

The following example illustrates a simple example of the table format.

.. code-block:: aimms

	Distance(i,j) := DATA TABLE
	                Rotterdam    Antwerp    Berlin    Paris
	!               ---------    -------    ------    -----
	    Amsterdam       85          170       660      510
	    Rotterdam                   100       700      440
	    Antwerp                               725      340
	    Berlin                                        1050
	;

The first line of a table (after the keyword ``DATA TABLE``) contains
the column identifiers. Each subsequent line contains a row identifier
followed by the table entries.

.. rubric:: Multidimensional entries

Row and column identifiers may be set elements, tuples of elements, or
tuples containing element ranges. As a result, multidimensional
identifiers can still be captured within the two-dimensional framework
of a table.

.. rubric:: Proper spacing

Column identifiers must be separated by at least one space. AIMMS keeps
track of the column width by maintaining the first and last position
used by each column identifier. Any entry must intersect only one column
and is understood to be part of that column. AIMMS will reject any entry
that intersects two columns, or falls between them.

.. rubric:: Continuation of tables with ``+``

Even though the table format is a convenient way to enter data, the
number of columns is always restricted by the width of a line. However,
by placing a ``+`` on a new line you can continue a table by repeating
the table format. Row identifiers and column identifiers can be repeated
in each block separated by the ``+`` sign, but must be unique within a
block.

.. rubric:: Example

The following table illustrates a valid example of table continuation,
equivalent with the previous example.

.. code-block:: aimms

	Distance(i,j) := DATA TABLE
	                Rotterdam    Antwerp   
	!               ---------    -------   
	    Amsterdam       85          170    
	    Rotterdam                   100    
	+
	                Berlin    Paris
	!               ------    -----
	    Amsterdam     660      510 
	    Rotterdam     700      440 
	    Antwerp       725      340 
	    Berlin                1050
	;

.. rubric:: Data and membership tables

Tables can be used for the initialization of both parameters and sets.
When used for parameter initialization, table entries are either blank
or contain explicit numbers, quoted or unquoted set elements and quoted
strings. Entries in tables used for set initialization are either blank
or contain a ``*`` denoting membership.

.. rubric:: Syntax

The detailed syntax of a table constant is given by the following
diagram, where the symbol ":math:`\backslash`\ n" stands for the newline
character.

.. _table:

*table:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 516.6827 87.199997"
	   height="87.199997"
	   width="516.68268"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,206.93333)"
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
	           transform="matrix(1,0,0,-1,17,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">DATA TABLE</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 940,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1180,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,123,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">\n</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1424,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1544,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,159.4,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/format-of-text-data-files/tabular-expressions.html#table-header">table-header</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2317.68,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2437.68,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,248.768,96)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">\n</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2681.68,1000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2921.68,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,297.168,96)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/format-of-text-data-files/tabular-expressions.html#table-row">table-row</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3515.12,1000 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2801.68,1000 20,50 h -40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3096.4,1300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g68"><text
	           id="text72"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,314.64,126)"><tspan
	             id="tspan70"
	             y="0"
	             x="0">\n</tspan></text>
	</g><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3340.4,1300 50,-20 v 40" /><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3635.12,1000 20,50 h -40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1060,1000 20,50 h -40" /><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2307.56,1450 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g82"><text
	           id="text86"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,237.156,141)"><tspan
	             id="tspan84"
	             y="0"
	             x="0">+</tspan></text>
	</g><path
	         id="path88"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2507.56,1450 50,-20 v 40" /><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3755.12,1000 20,50 h -40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3875.12,1000 -50,20 v -40" /><path
	         id="path94"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 v 0 c 0,55.23 44.773,100 100,100 h 620 c 55.227,0 100,-44.77 100,-100 v 0 0 C 940,944.773 895.227,900 840,900 H 220 c -55.227,0 -100,44.773 -100,100 v 0 m 820,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.773 -100,100 v 0 m 244,0 h 120 v 100 h 773.66 V 1000 900 H 1544 v 100 m 773.68,0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.773 -100,100 v 0 m 244,0 h 120 m 0,0 v 0 h 120 v 100 H 3515.1 V 1000 900 h -593.42 v 100 m 593.44,0 h 120 m -833.44,0 v 200 c 0,55.23 44.77,100 100,100 h 74.72 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 74.72 c 55.22,0 100,-44.77 100,-100 v -200 h 120 M 1060,1000 v 350 c 0,55.23 44.77,100 100,100 h 1027.56 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 1027.56 c 55.22,0 100,-44.77 100,-100 v -350 h 120" /></g></g></svg></div>

.. _table-header:

*table-header:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 174.26133 53.866665"
	   height="53.866665"
	   width="174.26132"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,173.6)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 240,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,29,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#element-tuple">element-tuple</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1066.96,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,1000 20,50 h -40" /><path
	         id="path26"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1186.96,1000 20,50 h -40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1306.96,1000 -50,20 v -40" /><path
	         id="path30"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 m 0,0 v 0 h 120 v 100 h 826.94 V 1000 900 H 240 v 100 m 826.96,0 h 120 M 120,1000 v 200 c 0,55.23 44.773,100 100,100 h 373.48 120 373.48 c 55.23,0 100,-44.77 100,-100 v -200 h 120" /></g></g></svg></div>

.. _table-row:

*table-row:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 296.07466 120.53333"
	   height="120.53333"
	   width="296.07465"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,440.26666)"
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
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#element-tuple">element-tuple</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 946.961,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1306.96,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,135.696,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#constant">constant</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1860.56,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1186.96,3000 -20,-50 h 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1483.76,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,154.776,266)"><tspan
	             id="tspan40"
	             y="0"
	             x="0">*</tspan></text>
	</g><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1683.76,2700 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1980.56,3000 -20,-50 h 40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1186.96,3000 -20,-50 h 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1980.56,3000 -20,-50 h 40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1066.96,3000 20,50 h -40" /><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2100.56,3000 20,50 h -40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2220.56,3000 -50,20 v -40" /><path
	         id="path58"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 v 100 H 946.938 V 3000 2900 H 120 v 100 m 826.961,0 h 119.999 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 553.59 v -100 -100 h -553.59 v 100 m 553.6,0 h 120 m -793.6,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 76.8 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120 76.8 c 55.23,0 100,44.77 100,100 v 200 m -793.6,0 v -500 c 0,-55.23 44.77,-100 100,-100 h 236.8 120 236.8 c 55.23,0 100,44.77 100,100 v 500 h 120 m -1033.6,0 v 200 c 0,55.23 44.77,100 100,100 h 356.8 120 356.8 c 55.23,0 100,-44.77 100,-100 v -200 h 120" /></g></g></svg></div>