.. _sec:text.composite:

Composite Tables
================

.. _composite:

.. rubric:: Multiple identifiers

A composite table is a bulk form of initialization, and is similar in
structure to a table in a database. Using a composite table you can
initialize simple sets, relations, parameters, and variables in a single
statement. Composite tables always form a single block, and can only be
used in text data files.

.. rubric:: Format

The first line of a composite table contains column identifiers that
define the index columns and the quantity columns. The subsequent lines
contain data entries. Like in a tabular expression, entries in a
composite table may be either blank or contain explicit numbers, quoted
or unquoted set elements and quoted strings, depending on the type of
the identifier associated with a column. Blank entries in the quantity
columns are treated as "no assignment.", while blank entries in the
index columns are not allowed. All data entries must lie directly below
their corresponding column identifier as in regular tables.

.. rubric:: Indices must come first

The full index space is declared in the first group of column
identifiers, and is comparable to the *primary key* in a database table.
The remaining column identifiers declare various quantities that must
share the identical index space. Note that, unlike in tabular
expressions, index columns in a data entry row of a composite table
cannot refer to tuples or ranges of elements, but only to single set
elements.

.. rubric:: Example

The following statement illustrates a valid example of a composite
table. It initializes the relation ``Routes``, as well as the parameters
``Distance`` and ``TransportCost``, all of which are defined over the
index space (``i``, ``j``).

.. code-block:: aimms

	COMPOSITE TABLE
	    i           j            Routes    Distance    TransportCost
	!   ---------   ---------    ------    --------    -------------
	    Amsterdam   Rotterdam      *            85        1.00
	    Amsterdam   Antwerp        *           170        2.50
	    Amsterdam   Berlin                     660       10.00
	    Amsterdam   Paris          *           510        8.25
	    Rotterdam   Antwerp        *           100        1.20
	    Rotterdam   Berlin         *           700       10.00
	    Rotterdam   Paris                      440        7.50
	    Antwerp     Berlin         *           725       11.00 
	    Antwerp     Paris          *           340        5.00
	    Berlin      Paris                     1050       17.50
	;

.. rubric:: Syntax

The detailed syntax of the composite table is given by the following
diagram, where the symbol ``\n`` stands for the newline character.

.. _composite-table:

*composite-table:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 507.21599 120.53333"
	   height="120.53333"
	   width="507.21597"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,746.93331)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 90,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,14,546)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">COMPOSITE</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 838,5500 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 928,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,97.8,546)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">TABLE</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1388,5500 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1478,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,152.8,546)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">\n</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1722,5500 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1812,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,186.2,546)"><tspan
	             id="tspan48"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/format-of-text-data-files/composite-tables.html#composite-header">composite-header</a></tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2872.36,5500 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2962.36,5500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,301.236,546)"><tspan
	             id="tspan58"
	             y="0"
	             x="0">\n</tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3206.36,5500 50,-20 v 40" /><path
	         id="path64"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 3296.36,5500 h 240" /><path
	         id="path66"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 1700,4800 h 240" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2120,4800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g70"><text
	           id="text74"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,217,476)"><tspan
	             id="tspan72"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/format-of-text-data-files/composite-tables.html#composite-row">composite-row</a></tspan></text>
	</g><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3000.12,4800 50,-20 v 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3090.12,4800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g80"><text
	           id="text84"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,314.012,476)"><tspan
	             id="tspan82"
	             y="0"
	             x="0">\n</tspan></text>
	</g><path
	         id="path86"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3334.12,4800 50,-20 v 40" /><path
	         id="path88"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2030,4800 20,50 h -40" /><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3424.12,4800 20,50 h -40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3514.12,4800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g94"><text
	           id="text98"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,357.812,476)"><tspan
	             id="tspan96"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path100"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3714.12,4800 50,-20 v 40" /><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3804.12,4800 -50,20 v -40" /><path
	         id="path104"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5500 h 90 v 0 c 0,55.23 44.773,100 100,100 h 548 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 190 c -55.227,0 -100,44.77 -100,100 v 0 m 748,0 h 90 v 0 c 0,55.23 44.773,100 100,100 h 260 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -260 c -55.227,0 -100,44.77 -100,100 v 0 m 460,0 h 90 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 90 v 100 H 2872.34 V 5500 5400 H 1812 v 100 m 1060.36,0 h 90 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 90 M 1940,4800 h 90 m 0,0 v 0 h 90 v 100 h 880.1 V 4800 4700 H 2120 v 100 m 880.12,0 h 90 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 90 M 2030,4800 v 200 c 0,55.23 44.77,100 100,100 h 552.06 90 552.06 c 55.23,0 100,-44.77 100,-100 v -200 h 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90" /></g></g></svg></div>

.. _composite-header:

*composite-header:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 244.49067 53.866665"
	   height="53.866665"
	   width="244.49066"
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
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-declaration/index-declaration-and-attributes.html#index">index</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 626.801,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,1000 20,50 h -40" /><path
	         id="path26"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 746.801,1000 20,50 h -40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 986.801,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,103.68,96)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#reference">reference</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1593.68,1000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 866.801,1000 20,50 h -40" /><path
	         id="path40"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1713.68,1000 20,50 h -40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1833.68,1000 -50,20 v -40" /><path
	         id="path44"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 m 0,0 v 0 h 120 v 100 H 626.793 V 1000 900 H 240 v 100 m 386.801,0 h 120 M 120,1000 v 200 c 0,55.23 44.773,100 100,100 h 153.398 120 153.403 c 55.226,0 100,-44.77 100,-100 v -200 h 120 m 0,0 v 0 h 120 v 100 H 1593.67 V 1000 900 H 986.801 v 100 m 606.879,0 h 120 m -846.879,0 v 200 c 0,55.23 44.773,100 100,100 h 263.439 120 263.44 c 55.23,0 100,-44.77 100,-100 v -200 h 120" /></g></g></svg></div>

.. _composite-row:

*composite-row:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 256.05866 53.866665"
	   height="53.866665"
	   width="256.05865"
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
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#element">element</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 766.84,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,1000 20,50 h -40" /><path
	         id="path26"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 886.84,1000 20,50 h -40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1126.84,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,117.684,96)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#constant">constant</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1680.44,1000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1006.84,1000 20,50 h -40" /><path
	         id="path40"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1800.44,1000 20,50 h -40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1920.44,1000 -50,20 v -40" /><path
	         id="path44"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 m 0,0 v 0 h 120 v 100 H 766.828 V 1000 900 H 240 v 100 m 526.84,0 h 120 M 120,1000 v 200 c 0,55.23 44.773,100 100,100 h 223.422 120 223.418 c 55.226,0 100,-44.77 100,-100 v -200 h 120 m 0,0 v 0 h 120 v 100 h 553.59 V 1000 900 h -553.59 v 100 m 553.6,0 h 120 m -793.6,0 v 200 c 0,55.23 44.77,100 100,100 h 236.8 120 236.8 c 55.23,0 100,-44.77 100,-100 v -200 h 120" /></g></g></svg></div>