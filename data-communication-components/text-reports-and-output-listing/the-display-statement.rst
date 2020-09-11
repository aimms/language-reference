.. _sec:report.display:

The ``DISPLAY`` Statement
=========================

.. _display:

.. rubric:: Output in AIMMS format

You can use the ``DISPLAY`` statement to print the data associated with
sets, parameters and variables to a file or window in AIMMS format. As
this format is also very easy to read, the ``DISPLAY`` statement is an
excellent alternative for printing indexed identifiers.

.. _display-statement:

.. rubric:: Syntax

*display-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 560.59731 213.86666"
	   height="213.86667"
	   width="560.59729"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,1120.2666)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 90,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,14,796)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">DISPLAY</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 694,8000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 874,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,93.8,796)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">{</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1074,8000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 784,8000 -20,-50 h 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1164,8000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1344,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,139.4,796)"><tspan
	             id="tspan42"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/assignment-statements.html#data-selection">data-selection</a></tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2191,8000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2371,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,242.1,796)"><tspan
	             id="tspan52"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-display-statement.html#display-format">display-format</a></tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3224.48,8000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2281,8000 -20,-50 h 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3314.48,8000 -20,-50 h 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1254,8000 20,50 h -40" /><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2229.24,8300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g66"><text
	           id="text70"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,229.324,826)"><tspan
	             id="tspan68"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2429.24,8300 50,-20 v 40" /><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3404.48,8000 20,50 h -40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3584.48,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g78"><text
	           id="text82"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,364.848,796)"><tspan
	             id="tspan80"
	             y="0"
	             x="0">}</tspan></text>
	</g><path
	         id="path84"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3784.48,8000 50,-20 v 40" /><path
	         id="path86"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3494.48,8000 -20,-50 h 40" /><path
	         id="path88"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3874.48,8000 -20,-50 h 40" /><path
	         id="path90"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 3964.48,8000 h 240" /><path
	         id="path92"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 1300,7100 h 240" /><path
	         id="path94"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1720,7100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g96"><text
	           id="text100"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,177,706)"><tspan
	             id="tspan98"
	             y="0"
	             x="0">WHERE</tspan></text>
	</g><path
	         id="path102"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2180,7100 50,-20 v 40" /><path
	         id="path104"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2360,7100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g106"><text
	           id="text110"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,241,706)"><tspan
	             id="tspan108"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-display-statement.html#display-format">display-format</a></tspan></text>
	</g><path
	         id="path112"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3213.48,7100 50,-20 v 40" /><path
	         id="path114"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2270,7100 20,50 h -40" /><path
	         id="path116"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2686.74,7400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g118"><text
	           id="text122"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,275.074,736)"><tspan
	             id="tspan120"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path124"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2886.74,7400 50,-20 v 40" /><path
	         id="path126"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3303.48,7100 20,50 h -40" /><path
	         id="path128"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1630,7100 -20,-50 h 40" /><path
	         id="path130"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3393.48,7100 -20,-50 h 40" /><path
	         id="path132"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3483.48,7100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g134"><text
	           id="text138"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,354.748,706)"><tspan
	             id="tspan136"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path140"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3683.48,7100 50,-20 v 40" /><path
	         id="path142"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3773.48,7100 -50,20 v -40" /><path
	         id="path144"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,8000 h 90 v 0 c 0,55.23 44.773,100 100,100 h 404 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 190 c -55.227,0 -100,44.77 -100,100 v 0 m 604,0 h 90 m 0,0 v 0 h 90 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 90 m -380,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 45 90 45 c 55.23,0 100,44.77 100,100 v 200 h 90 m 0,0 v 0 h 90 v 100 h 846.98 V 8000 7900 H 1344 v 100 m 847,0 h 90 m 0,0 v 0 h 90 v 100 h 853.46 V 8000 7900 H 2371 v 100 m 853.48,0 h 90 M 2281,8000 v -200 c 0,-55.23 44.77,-100 100,-100 h 371.74 90 371.74 c 55.23,0 100,44.77 100,100 v 200 h 90 M 1254,8000 v 200 c 0,55.23 44.77,100 100,100 h 785.24 90 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 90 785.24 c 55.23,0 100,-44.77 100,-100 v -200 h 90 m 0,0 v 0 h 90 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 90 m -380,0 v -200 c 0,-55.23 44.78,-100 100,-100 h 45 90 45 c 55.23,0 100,44.77 100,100 v 200 h 90 M 1540,7100 h 90 m 0,0 v 0 h 90 v 0 c 0,55.23 44.77,100 100,100 h 260 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -260 c -55.23,0 -100,44.77 -100,100 v 0 m 460,0 h 90 m 0,0 v 0 h 90 v 100 h 853.46 V 7100 7000 H 2360 v 100 m 853.48,0 h 90 M 2270,7100 v 200 c 0,55.23 44.77,100 100,100 h 226.74 90 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90 226.74 c 55.23,0 100,-44.77 100,-100 v -200 h 90 M 1630,7100 v -200 c 0,-55.23 44.77,-100 100,-100 h 736.74 90 736.74 c 55.22,0 100,44.77 100,100 v 200 h 90 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 90" /></g></g></svg></div>

.. _display-format:

*display-format:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 300.13334 27.199999"
	   height="27.199999"
	   width="300.13333"
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
	         d="m 100,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,15,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-display-statement.html#format-specifier">format-specifier</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1026.8,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1126.8,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,117.68,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">:=</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1370.8,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1470.8,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,152.08,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2151,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2251,1000 -50,20 v -40" /><path
	         id="path46"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 100 v 100 h 926.77 V 1000 900 H 100 v 100 m 926.8,0 h 100 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.773 -100,100 v 0 m 244,0 h 100 v 100 h 680.19 V 1000 900 H 1470.8 v 100 m 680.2,0 h 100" /></g></g></svg></div>

.. rubric:: Display format

All data selections of a ``DISPLAY`` statement are printed by AIMMS in
the form of a data assignment.

-  Sets are printed in the form of a set assignment with an *enumerated
   set* on the right-hand side.

-  (Slices of) parameters and variables are printed in the form of data
   assignments, which can be either a table format, a list format, or a
   composite table.

For indexed parameters and variables AIMMS uses a default display format
which is dependent on the dimension.

.. _format-specifier:

.. rubric:: Overriding the display format

You can override the default AIMMS format by specifying a *display
format*, consisting of one or more format specifications, in the
``WHERE`` clause. AIMMS supports the following format specifiers:

-  ``DECIMALS``: the number of decimals to be printed for each entry,

-  ``ROWDIM``: the dimension of the row space,

-  ``COLDIM``: the dimension of the column space, and

-  ``COLSPERLINE``: the desired numbers of columns per line.

When a format specifier is not specified, AIMMS will use the system
default.

.. rubric:: Number of decimals

All format specifications in a ``WHERE`` clause are applied to the
entire collection of data selections printed in the ``DISPLAY``
statement. By specifying a ``DECIMAL`` format specifier for a particular
data selection in the ``DISPLAY`` statement, you can also override the
number of decimals printed for each data selection individually. You
cannot specify other format specifiers for individual data selections.

.. rubric:: Obtaining lists and tables

If you have set the dimension of either the row or column space to zero,
AIMMS will print the identifier in list format. If both the dimension of
the row and column space are greater than zero, AIMMS will print the
identifier as a table. AIMMS will honor your request to print the
desired number of columns per line if the resulting width does not
exceed the default page width. In the latter case, AIMMS will reduce the
number of columns until they fit within the requested page width. The
default page width can be set as an option within your project.

.. rubric:: Outer indices for slicing

If the sum of the dimensions of the row and column space is less than
the dimension of the parameter or variable to be displayed, AIMMS will
display the identifiers as slices of the requested format, where the
slices are taken by fixing the first indices in the domain.

.. rubric:: Composite tables

When all arguments of the ``DISPLAY`` statement have the same domain and
you enclose them by braces, AIMMS will print their values as a single
composite table. In this case, you can only specify the precision with
which each column must be printed. AIMMS will ignore any of the other
display options in combination with the composite table format.

.. rubric:: Example

The following statements illustrate the use of the ``DISPLAY`` statement
and its various display options.

-  The following statement will display the data of the variable
   ``Transport`` with 2 decimals and in the default format.

   .. code-block:: aimms
   
   	display Transport where decimals := 2;

   The execution of this statement results in the following output being
   generated.

   .. code-block:: aimms
   
   	    Transport :=
   	    data table
   	             Amsterdam   Rotterdam  'Den Haag'
   	         !  ----------  ----------  ----------
   	 Amsterdam        2.50        2.50        5.00
   	 Rotterdam        2.50        5.00        5.00
   	'Den Haag'                    2.50        5.00
   	    ;

-  The following statement displays the subselection of the slice of the
   variable ``Transport`` consisting of all transports departing from
   the set ``LargeSupplyCities``.

   .. code-block:: aimms
   
   	display Transport(i in LargeSupplyCities,j) where decimals := 2;

   This statement will result in the following table, assuming that
   ``LargeSupplyCities`` contains only ``Amsterdam`` and ``Rotterdam``.

   .. code-block:: aimms
   
   	   Transport :=
   	   data table
   	            Amsterdam   Rotterdam  'Den Haag'
   	        !  ----------  ----------  ----------
   	Amsterdam        2.50        2.50        5.00
   	Rotterdam        2.50        5.00        5.00
   	   ;

-  The following ``DISPLAY`` statement displays ``Transport`` with no
   rows, two columns (i.e. in list format), and two entries per line.

   .. code-block:: aimms
   
   	display Transport where decimals:=2, rowdim:=0, coldim:=2, colsperline:=2;

   The resulting output looks as follows.

   .. code-block:: aimms
   
   	Transport := data
   	{ ( Amsterdam , Amsterdam  ) : 2.50,  ( Amsterdam , Rotterdam  ) : 2.50,
   	  ( Amsterdam , 'Den Haag' ) : 5.00,  ( Rotterdam , Amsterdam  ) : 2.50,
   	  ( Rotterdam , Rotterdam  ) : 5.00,  ( Rotterdam , 'Den Haag' ) : 5.00,
   	  ( 'Den Haag', Rotterdam  ) : 2.50,  ( 'Den Haag', 'Den Haag' ) : 5.00 } ;

-  In the following ``DISPLAY`` statement the row and column display
   dimensions do not add up to the dimension of ``Transport``.

   .. code-block:: aimms
   
   	display Transport where decimals:=2, rowdim:=0, coldim:=1, colsperline:=3;

   As a result AIMMS considers the indices corresponding to the
   dimension deficit as outer, and displays ``Transport`` by means of
   three one-dimensional displays, each of the requested dimension.

   .. code-block:: aimms
   
   	Transport('Amsterdam', j) := data
   	{ Amsterdam  : 2.50,  Rotterdam  : 2.50,  'Den Haag' : 5.00 } ;
   
   	Transport('Rotterdam', j) := data
   	{ Amsterdam  : 2.50,  Rotterdam  : 5.00,  'Den Haag' : 5.00 } ;
   
   	Transport('Den Haag', j) := data
   	{ Rotterdam  : 2.50,  'Den Haag' : 5.00 } ;

-  The following ``DISPLAY`` statement illustrates how a composite table
   can be obtained for identifiers defined over the same domain, with a
   different number of decimals for each identifier.

   .. code-block:: aimms
   
   	display { Supply decimals := 2, Demand decimals := 3 };

   Execution of this statement results in the creation of the following
   one-dimensional composite table.

   .. code-block:: aimms
   
   	Composite table:
   	    i             Supply   Demand
   	!   ----------    ------  -------
   	    Amsterdam      10.00    5.000
   	    Rotterdam      12.50   10.000
   	    'Den Haag'      7.50   15.000
   	    ;