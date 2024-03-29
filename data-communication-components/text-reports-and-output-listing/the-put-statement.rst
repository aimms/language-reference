.. _sec:report.put:

The ``PUT`` Statement
=====================

.. rubric:: Customized text reports

AIMMS provides two statements to create a customized text output report
in either a file or in a text window in the user interface. They are the
``PUT`` and the ``DISPLAY`` statements. The result of these statements
must always be directed to either a single file or a window.

.. rubric:: Basic steps

The following steps are required to create a customized text report:

-  direct the output to the appropriate ``File`` identifier, and

-  print one or more strings, set elements, numerical items, or tabular
   arrangements of data to it.

These basic operations are the subject of the subsequent subsections. At
the end of the section, an extended example will illustrate most of the
discussed features.

.. rubric:: Stream versus page mode

AIMMS can produce text reports in two modes. They are:

-  *stream mode*, in which all lines are printed consecutively, and

-  *page mode*, where the report is divided into pages of equal length,
   each consisting of a header, a footer and a data area.

Most aspects, such as opening files, output direction, and formatting,
are the same for both reporting modes. Only the structuring of pages is
an extra aspect of the page mode, and is discussed in
:ref:`sec:report.page-mode`.

.. _sec:report.put.file:

Opening Files and Output Redirection
------------------------------------

.. rubric:: Opening files

Disk files and windows are opened automatically as soon as output is
written to them. You can send output to a particular file by providing
the associated ``File`` identifier as the first argument of a ``PUT``
statement, which designates the file as the *current file*.

.. rubric:: ``PUT`` without file identifier

If you use the ``DISPLAY`` statement or any of the ``PUT`` operators
listed in :ref:`this table <table:report.put-keyword>` without a file identifier,
AIMMS will direct the output to the current file, i.e., the file last
opened through the ``PUT`` statement.

.. rubric:: Undirected output

When you have not yet selected a current file yet, AIMMS will send the
output of any ``PUT`` or ``DISPLAY`` statement to the standard listing
file associated with your model.

.. rubric:: Example

The following statements illustrates how to send output to a particular
file.

.. code-block:: aimms

	PUT ResultFile ;
	PUT "The model results are:" ;  
	DISPLAY Transport ;           
	PUTCLOSE;

The first ``PUT`` statement sets the current file equal to
``ResultFile``, causing the output of the subsequent ``PUT`` and
``DISPLAY`` statements to be directed to it. The final ``PUTCLOSE``
statement will close ``ResultFile``.

.. rubric:: File identifiers only

Unlike other statements like ``READ`` and ``WRITE`` which allow you to
represent files by strings or string parameters as well, the ``PUT``
statement requires that you use a ``File`` identifier to represent the
output file. The way in which output to a file is generated by the
``PUT`` statement is completely controlled by the suffices associated
with the corresponding ``File`` identifier (see also
:ref:`sec:report.page-mode`).

.. _currentfile-LR:

.. _currentfilename-LR:

.. rubric:: Accessing the current file

AIMMS has two pre-defined identifiers that provide access to the current
file. They are

-  the element parameter :any:`CurrentFile` (into the set
   :any:`AllIdentifiers`) containing the current ``File`` identifier, and

-  the string parameter :any:`CurrentFileName`, containing the file name or
   window title associated with the current file identifier.

The parameter :any:`CurrentFileName` is output only.

.. rubric:: Changing the current file

To select another current file, you can use either of two methods:

-  use the ``PUT`` statement to (re-)direct output to a different file,
   or

-  set the identifier :any:`CurrentFile` to the ``File`` identifier of your
   choice.

.. _putclose:

.. rubric:: Closing external files

Closing an external file can be done in two ways:

-  automatically, by quitting AIMMS at the end of a session, or

-  manually by calling "``PUTCLOSE`` *file-identifier*" during
   execution.

.. rubric:: Files left open

If you leave a file open during the execution of a procedure, AIMMS will
temporarily close it at the end of the current execution, and re-open it
in *append mode* at the beginning of a subsequent execution. This
enables you to inspect the ``PUT`` files in between runs.

.. _sec:report.put.format:

Formatting and Positioning ``PUT`` Items
----------------------------------------

.. _put:

Besides selecting the current file, the ``PUT`` statement can be used to
output one or more individual strings, numbers or set elements to an
external text file or window. Each item can be printed in either a
default or in a customized manner. The syntax of the ``PUT`` statement
follows.

.. _put-statement:

.. rubric:: Syntax

*put-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 494.28801 173.86666"
	   height="173.86667"
	   width="494.28799"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,853.59998)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,6000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,15,596)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-put-statement.html#PUT-operator">PUT-operator</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 926.84,6000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1126.84,6000 -20,-50 h 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1326.84,5400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,137.684,536)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2007.04,5400 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2207.04,5400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,225.704,536)"><tspan
	             id="tspan40"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-put-statement.html#format-field">format-field</a></tspan></text>
	</g><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2907.16,5400 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2107.04,5400 -20,-50 h 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3007.16,5400 -20,-50 h 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3207.16,6000 -20,-50 h 40" /><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1126.84,6000 -20,-50 h 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1526.78,5700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,157.678,566)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-put-statement.html#position-determination">position-determination</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2807.22,5700 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3207.16,6000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1793.6,6000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g68"><text
	           id="text72"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,184.36,596)"><tspan
	             id="tspan70"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/text-reports-and-output-listing/the-file-declaration.html#file-identifier">file-identifier</a></tspan></text>
	</g><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2540.4,6000 50,-20 v 40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1026.84,6000 20,50 h -40" /><path
	         id="path78"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2067,6300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g80"><text
	           id="text84"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,213.1,626)"><tspan
	             id="tspan82"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2267,6300 50,-20 v 40" /><path
	         id="path88"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3307.16,6000 20,50 h -40" /><path
	         id="path90"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3407.16,6000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g92"><text
	           id="text96"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,347.116,596)"><tspan
	             id="tspan94"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path98"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3607.16,6000 50,-20 v 40" /><path
	         id="path100"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3707.16,6000 -50,20 v -40" /><path
	         id="path102"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,6000 h 100 v 100 H 926.816 V 6000 5900 H 100 v 100 m 826.84,0 h 100 m 0,0 v 0 h 100 m 0,0 v -500 c 0,-55.23 44.77,-100 100,-100 v 0 h 100 v 100 h 680.19 v -100 -100 h -680.19 v 100 m 680.2,0 h 100 m 0,0 v 0 h 100 v 100 h 700.1 v -100 -100 h -700.1 v 100 m 700.12,0 h 100 m -900.12,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 300.06 100 300.06 c 55.23,0 100,44.77 100,100 v 200 h 100 v 0 c 55.23,0 100,44.77 100,100 v 500 m -2080.32,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 199.94 100 v 100 h 1280.4 v -100 -100 h -1280.4 v 100 m 1280.44,0 h 100 199.94 c 55.22,0 100,44.77 100,100 v 200 m -2080.32,0 h 100 466.76 100 v 100 h 746.77 V 6000 5900 H 1793.6 v 100 m 746.8,0 h 100 566.76 100 m -2280.32,0 v 200 c 0,55.23 44.77,100 100,100 H 1967 2067 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 840.16 c 55.23,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100" /></g></g></svg></div>

.. _puthd:

.. _putft:

.. _putpage:

.. _PUT-operator:

.. rubric:: ``PUT`` operators

All possible variants of the ``PUT`` operator are listed in
:ref:`this table <table:report.put-keyword>`. The ``PUT`` and ``PUTCLOSE``
operators can be used in both stream mode and page mode. The operators
``PUTHD``, ``PUTFT`` and ``PUTPAGE`` only make sense in page mode, and
are discussed in :ref:`sec:report.page-mode`.

.. _table:report.put-keyword:

.. table:: 

	+--------------+---------------------------------+-----------------+-----------------+
	| Statement    | Description                     | Stream mode     | Page mode       |
	+==============+=================================+=================+=================+
	| ``PUT``      | Direct output or write output   | :math:`\bullet` | :math:`\bullet` |
	+--------------+---------------------------------+-----------------+-----------------+
	| ``PUTCLOSE`` | ``PUT`` and close current file  | :math:`\bullet` | :math:`\bullet` |
	+--------------+---------------------------------+-----------------+-----------------+
	| ``PUTHD``    | Write in header area            |                 | :math:`\bullet` |
	+--------------+---------------------------------+-----------------+-----------------+
	| ``PUTFT``    | Write in footer area            |                 | :math:`\bullet` |
	+--------------+---------------------------------+-----------------+-----------------+
	| ``PUTPAGE``  | ``PUT`` and output current page |                 | :math:`\bullet` |
	+--------------+---------------------------------+-----------------+-----------------+
	
.. rubric:: Put items are always scalar

All ``PUT`` operators only accept scalar expressions. For each scalar
item to be printed you can optionally specify a format field, with
syntax:

.. _format-field:

.. rubric:: Syntax

*format-field:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 624.59731 147.19999"
	   height="147.2"
	   width="624.59729"
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
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,7000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,18.4,696)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 320,7000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 440,7000 -20,-50 h 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 620,6100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67,606)"><tspan
	             id="tspan30"
	             y="0"
	             x="0">&lt;&gt;</tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 864,6100 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1044,7000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 440,7000 -20,-50 h 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 642,6400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g42"><text
	           id="text46"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,70.6,636)"><tspan
	             id="tspan44"
	             y="0"
	             x="0">&gt;</tspan></text>
	</g><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 842,6400 50,-20 v 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1044,7000 -20,-50 h 40" /><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 440,7000 -20,-50 h 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 642,6700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,70.6,666)"><tspan
	             id="tspan58"
	             y="0"
	             x="0">&lt;</tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 842,6700 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1044,7000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1284,7000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g68"><text
	           id="text72"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,133.4,696)"><tspan
	             id="tspan70"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2524.24,7000 50,-20 v 40" /><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1164,7000 -20,-50 h 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2644.24,7000 -20,-50 h 40" /><path
	         id="path80"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2884.24,7000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g82"><text
	           id="text86"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,294.824,696)"><tspan
	             id="tspan84"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path88"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3084.24,7000 50,-20 v 40" /><path
	         id="path90"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3204.24,7000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g92"><text
	           id="text96"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,325.424,696)"><tspan
	             id="tspan94"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path98"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4444.48,7000 50,-20 v 40" /><path
	         id="path100"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2764.24,7000 -20,-50 h 40" /><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4564.48,7000 -20,-50 h 40" /><path
	         id="path104"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4684.48,7000 -50,20 v -40" /><path
	         id="path106"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,7000 h 120 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 120 m 0,0 v -800 c 0,-55.23 44.773,-100 100,-100 v 0 h 80 v 0 c 0,55.23 44.773,100 100,100 h 44 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 h -44 c -55.227,0 -100,44.77 -100,100 v 0 m 244,0 h 80 v 0 c 55.227,0 100,44.77 100,100 v 800 m -604,0 v -500 c 0,-55.23 44.773,-100 100,-100 h 22 80 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 80 22 c 55.227,0 100,44.77 100,100 v 500 m -604,0 v -200 c 0,-55.23 44.773,-100 100,-100 h 22 80 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 80 22 c 55.227,0 100,44.77 100,100 v 200 m -604,0 h 100 162 80 262 120 m 0,0 v 0 h 120 v 100 H 2524.21 V 7000 6900 H 1284 v 100 m 1240.24,0 h 120 M 1164,7000 v -200 c 0,-55.23 44.77,-100 100,-100 h 580.12 120 580.12 c 55.22,0 100,44.77 100,100 v 200 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 H 4444.45 V 7000 6900 H 3204.24 v 100 m 1240.24,0 h 120 m -1800.24,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 740.12 120 740.12 c 55.22,0 100,44.77 100,100 v 200 h 120" /></g></g></svg></div>

.. rubric:: Format fields

With the format field you specify

-  whether the item is to be centered, left aligned or right aligned,

-  the field width associated with an identifier, and

-  the precision.

Customized default values for the justification, field width and
precision can be specified through ``PUT``-related options, which can be
set via the Options menu. :ref:`The following table <table:report.put-arg>` shows a number
of examples of format fields, where :math:`m` and :math:`n` are
expressions evaluating to integers.

.. _table:report.put-arg:

.. table:: 

	+----------------------------------------------+---------------+--------------------------+-----------+
	| ``PUT`` **argument**                         | Justification | Field width (characters) | Precision |
	+==============================================+===============+==========================+===========+
	| *item*                                       | default       | default                  | default   |
	+----------------------------------------------+---------------+--------------------------+-----------+
	| *item*\ ``:``\ :math:`m`                     | default       | :math:`m`                | default   |
	+----------------------------------------------+---------------+--------------------------+-----------+
	| *item*\ ``:``\ :math:`m`\ ``:``\ :math:`n`   | default       | :math:`m`                | :math:`n` |
	+----------------------------------------------+---------------+--------------------------+-----------+
	| *item*\ ``:<``\ :math:`m`\ ``:``\ :math:`n`  | left          | :math:`m`                | :math:`n` |
	+----------------------------------------------+---------------+--------------------------+-----------+
	| *item*\ ``:>``\ :math:`m`\ ``:``\ :math:`n`  | right         | :math:`m`                | :math:`n` |
	+----------------------------------------------+---------------+--------------------------+-----------+
	| *item*\ ``:<>``\ :math:`m`\ ``:``\ :math:`n` | centered      | :math:`m`                | :math:`n` |
	+----------------------------------------------+---------------+--------------------------+-----------+
	
.. rubric:: Interpretation of precision

For numerical expressions the precision is the number of decimals to be
displayed. For strings and set elements the precision is the maximum
number of characters to be displayed. The numbers or characters are
placed into a field with the indicated width, and are positioned as
specified.

.. rubric:: Using the :any:`FormatString` function

The ``PUT`` syntax for formatting and displaying multiple items on a
single line is somewhat similar to the reporting syntax in programming
languages like ``FORTRAN`` or ``PASCAL``. If you are a ``C`` programmer,
you may prefer to construct and format a single line of text using the
:any:`FormatString` function (see also :ref:`sec:set-expr.string.format`).
In this case you only need the ``PUT`` statement to send the resulting
string to a text report or window.

.. rubric:: Position determination

For advanced reporting the ``PUT`` statement allows you to directly
position the cursor at a given row or column. The syntax is shown in the
following syntax diagram.

.. _position-determination:

*position-determination:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 285.36534 107.2"
	   height="107.2"
	   width="285.36533"
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
	         d="m 100,4000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 300,3700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,36.4,366)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">#</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 500,3700 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 600,3700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,65,366)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1840.24,3700 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2040.24,4000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 300,4000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g40"><text
	           id="text44"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,36.4,396)"><tspan
	             id="tspan42"
	             y="0"
	             x="0">@</tspan></text>
	</g><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 500,4000 50,-20 v 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 600,4000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,65,396)"><tspan
	             id="tspan52"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#numerical-expression">numerical-expression</a></tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1840.24,4000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,4000 -20,-50 h 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 970.121,3400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g62"><text
	           id="text66"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,103.412,336)"><tspan
	             id="tspan64"
	             y="0"
	             x="0">/</tspan></text>
	</g><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1170.12,3400 50,-20 v 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2040.24,4000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2140.24,4000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,4000 h 100 m 0,0 v -200 c 0,-55.23 44.773,-100 100,-100 v 0 h 100 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 100 v 100 H 1840.21 V 3700 3600 H 600 v 100 m 1240.24,0 h 100 v 0 c 55.22,0 100,44.77 100,100 v 200 M 100,4000 h 100 v 0 h 100 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 100 v 100 H 1840.21 V 4000 3900 H 600 v 100 m 1240.24,0 h 100 100 M 100,4000 v -500 c 0,-55.23 44.773,-100 100,-100 h 670.121 100 v 0 c 0,55.23 44.769,100 99.999,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -99.999,44.77 -99.999,100 v 0 m 199.999,0 h 100 670.12 c 55.23,0 100,44.77 100,100 v 500 h 100" /></g></g></svg></div>

.. rubric:: How to position

There are three special arguments for the ``PUT`` statement that can be
used to position printable items in a file:

-  the ``@`` operator-for horizontal positioning on a line,

-  the ``#`` operator-for vertical positioning, and

-  the newline operator ``/``.

These three operators are explained in :ref:`this table <table:report.put-pos>`,
where the symbols :math:`k` and :math:`l` are expressions evaluating to
integers.

.. _table:report.put-pos:

.. table:: Position determination

   +------------------+-----------------------------------------------------------------------+
   | Operator         | Meaning                                                               |
   +==================+=======================================================================+
   | ``@``\ :math:`k` | Start printing the next item at column :math:`k` of the current line. |
   +------------------+-----------------------------------------------------------------------+
   | ``#``\ :math:`l` | Goto line :math:`l` of current page (page mode only).                 |
   +------------------+-----------------------------------------------------------------------+
   | ``/``            | Goto new line.                                                        |
   +------------------+-----------------------------------------------------------------------+

.. rubric:: Page mode only

Using the vertical positioning operator ``#`` only makes sense when you
are printing in page mode. When printing in stream mode all lines are
numbered consecutively from the beginning of the report, and added to
the output file or window as soon as AIMMS encounters the newline
character ``/``. In page mode, AIMMS prints pages in their entirety, and
lines are numbered per page. As a result, you can write to any line
within the current page.

.. _sec:report.put.example:

Extended Example
----------------

.. rubric:: Example

This example builds upon the transport model used throughout the manual.
The following group of statements will produce a text report containing
the contents of the identifiers ``Supply(i)``, ``Demand(j)`` and
``Transport(i,j)``, in a combined tabular format separated into right
aligned columns of length 12.

.. rubric:: The statements

.. code-block:: aimms

	! Direct output to ResultFile
	put ResultFile ;

	! Construct a header for the table
	put @13, "Supply":>12, @30, "Transport":>12, /, @30 ;

	for ( j ) do   put j:>12 ;   endfor ;
	put // ;

	! Output the values for Demand
	put "Demand", @30 ;
	for ( j ) do   put Demand(j):>12:2 ;   endfor ;
	put // ;

	! Output Supply and Transport
	for ( i ) do
	    put i:<12, Supply(i):>12:2, @30 ;
	    for ( j ) do   put Transport(i,j):>12:2 ;   endfor;
	    put / ;
	endfor ;

	! Close ResultFile
	putclose ResultFile ;

.. rubric:: The produced report

For a particular small data set containing only three Dutch cities, the
above statements could result in the following report being generated.

.. code-block:: aimms

	                  Supply        Transport
	                                Amsterdam   Rotterdam    Den Haag

	Demand                               5.00       10.00       15.00

	Amsterdam          10.00             2.50        2.50        5.00
	Rotterdam          12.50             2.50        5.00        5.00
	Den Haag            7.50             0.00        2.50        5.00
