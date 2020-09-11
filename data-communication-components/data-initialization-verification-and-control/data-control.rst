.. _sec:data.control:

Data Control
============

.. rubric:: Why data control?

The contents of domain sets in your model may change through running
procedures or performing other actions from within the graphical user
interface. When elements are removed from sets, there may be data for
domain elements that are no longer in the domain sets. In addition, data
may exist for intermediate parameters, which is no longer used in the
remainder of your model session. For these situations, AIMMS offers
facilities to eliminate or activate data elements that fall outside
their current domain of definition. This section provides you with
housekeeping data control statements, which can be combined with
ordinary assignments to keep your model data consistent and maintained.

.. _data-control-statement:

.. rubric:: Facilities

AIMMS offers the following data control tools:

-  the ``EMPTY`` statement to remove the contents from all or a selected
   number of identifiers,

-  the ``CLEANUP`` and ``CLEANDEPENDENTS`` statements to clean up all,
   or a selected number of identifiers,

-  the ``REBUILD`` statement to manually instruct AIMMS to reclaim
   unused memory from the internal data structures used to the store the
   data of a selected number of identifiers,

-  the procedure :any:`FindUsedElements` to find all elements of a
   particular set that are in use in a given collection of indexed model
   identifiers, and

-  the procedure :any:`RestoreInactiveElements` to find and restore all
   inactive elements of a particular set for which inactive data exists
   in a given collection of indexed model identifiers.

.. _empty:

.. rubric:: The ``EMPTY`` statement

The ``EMPTY`` statement can be used to discard the complete contents of
all or selected identifiers in your model. Its syntax follows.

.. _empty-statement:

*empty-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 512.62398 101.86666"
	   height="101.86666"
	   width="512.62396"
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
	         d="m 120,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,296)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">EMPTY</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 580,3000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 940,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,99,296)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#reference">reference</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1546.88,3000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 820,3000 20,50 h -40" /><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1143.44,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,120.744,326)"><tspan
	             id="tspan40"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1343.44,3300 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1666.88,3000 20,50 h -40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1906.88,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,195.688,296)"><tspan
	             id="tspan52"
	             y="0"
	             x="0">IN</tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2150.88,3000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2270.88,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,232.088,296)"><tspan
	             id="tspan62"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/data-communication-components/communicating-with-databases/the-databasetable-declaration.html#database-table">database-table</a></tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3164.68,3000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1786.88,3000 -20,-50 h 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3284.68,3000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 700,3000 -20,-50 h 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3404.68,3000 -20,-50 h 40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3524.68,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g78"><text
	           id="text82"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,358.868,296)"><tspan
	             id="tspan80"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path84"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3724.68,3000 50,-20 v 40" /><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3844.68,3000 -50,20 v -40" /><path
	         id="path88"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 v 0 c 0,55.23 44.773,100 100,100 h 260 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 220 c -55.227,0 -100,44.77 -100,100 v 0 m 460,0 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 606.87 V 3000 2900 H 940 v 100 m 606.88,0 h 120 M 820,3000 v 200 c 0,55.23 44.773,100 100,100 h 103.44 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 103.44 c 55.23,0 100,-44.77 100,-100 v -200 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.78,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.22,0 -100,44.77 -100,100 v 0 m 244,0 h 120 v 100 h 893.78 v -100 -100 h -893.78 v 100 m 893.8,0 h 120 m -1497.8,0 v -200 c 0,-55.23 44.78,-100 100,-100 h 588.9 120 588.9 c 55.23,0 100,44.77 100,100 v 200 h 120 M 700,3000 v -260 c 0,-55.23 44.773,-100 100,-100 h 1192.34 120 1192.34 c 55.23,0 100,44.77 100,100 v 260 h 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. rubric:: Empty AIMMS identifiers

The ``EMPTY`` operator operates on a list of references to AIMMS
identifiers and takes the following actions.

-  For parameters, variables (arcs) and constraints (nodes) AIMMS
   discards their values plus the contents of all their suffices.

-  For sets, AIMMS will discard their contents plus the contents of all
   corresponding subsets. If a set is a domain set, AIMMS will remove
   the data from *all* parameters and variables that are defined over
   this set or any of its subsets.

-  For slices of an identifier, AIMMS will discard all values associated
   with the slice.

-  For sections in your model text, AIMMS will discard the contents of
   all sets, parameters and variables declared in this section.

-  For a subset of the predefined set :any:`AllIdentifiers`, AIMMS will
   discard the contents of all identifiers contained in this subset.

.. rubric:: Use in databases

You can also use the ``EMPTY`` statement in conjunction with databases.
With the ``EMPTY`` statement you can either empty single columns in a
database table, or discard the contents of an entire table. This use is
discussed in detail in :ref:`sec:db.control`. You should note, however,
that applying the ``EMPTY`` statement to a subset of :any:`AllIdentifiers`
does *not* apply to any database table contained in the subset to avoid
inadvertent deletion of data.

.. rubric:: Examples

The following statements illustrate the use of the ``EMPTY`` operator.

-  Remove all data of the variable ``Transport``.

   .. code-block:: aimms
   
   	empty Transport ;

-  Remove all data in the set ``Cities``, but also all data depending on
   ``Cities``, like e.g. ``Transport``.

   .. code-block:: aimms
   
   	empty Cities ;

-  Remove all the data of the indicated slice of the variable
   ``Transport``

   .. code-block:: aimms
   
   	empty Transport(DiscardedCity, j);

-  Remove all data of all identifiers in the model tree node CityData.

   .. code-block:: aimms
   
   	empty CityData ;

.. _inactive_data:

.. rubric:: Inactive data

When you remove some but not all elements from a domain set, AIMMS will
not automatically discard the data associated with those elements for
every identifier defined over the particular domain set. AIMMS will also
not automatically discard data that does not satisfy the current domain
restriction of a given identifier. Instead, it will consider such data
as *inactive*. During the execution of your model, no reference will be
made to inactive data, but such data may still be visible in the user
interface. In addition, AIMMS will not directly reclaim the memory that
is freed up when the cardinality of a multidimensional identifier in
your model decreases.

.. rubric:: When useful

The facility to create inactive data in AIMMS allows you to temporarily
remove elements from domain sets when this is required by your model.
You can then restore the data after the relevant parts of the model have
been executed.

.. _cleanup:

.. _rebuild:

.. rubric:: Discard inactive data
   :name: cleandependents

If you want to discard inactive data that has been introduced in a
particular data set, you can apply the ``CLEANUP`` statement to
parameters and variables, or the ``CLEANDEPENDENTS`` statement to root
sets in your model. Through the ``REBUILD`` statement you can instruct
AIMMS to reclaim the unused memory associated with one or more
identifiers in your model. The syntax follows.

.. _cleanup-statement:

*cleanup-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 444.46401 113.86666"
	   height="113.86666"
	   width="444.46399"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,460.26666)"
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
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,39,266)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">CLEANDEPENDENTS</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1520,2700 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1740,3000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 628,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67.8,296)"><tspan
	             id="tspan32"
	             y="0"
	             x="0">CLEANUP</tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1232,3000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,3000 20,50 h -40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 628,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g42"><text
	           id="text46"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67.8,326)"><tspan
	             id="tspan44"
	             y="0"
	             x="0">REBUILD</tspan></text>
	</g><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1232,3300 50,-20 v 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1740,3000 20,50 h -40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2100,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g54"><text
	           id="text58"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,215,296)"><tspan
	             id="tspan56"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2653.48,3000 50,-20 v 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1980,3000 20,50 h -40" /><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2276.74,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g66"><text
	           id="text70"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,234.074,326)"><tspan
	             id="tspan68"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2476.74,3300 50,-20 v 40" /><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2773.48,3000 20,50 h -40" /><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1860,3000 20,50 h -40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2893.48,3000 20,50 h -40" /><path
	         id="path80"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3013.48,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g82"><text
	           id="text86"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,307.748,296)"><tspan
	             id="tspan84"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path88"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3213.48,3000 50,-20 v 40" /><path
	         id="path90"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3333.48,3000 -50,20 v -40" /><path
	         id="path92"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 120 m 0,0 v -200 c 0,-55.23 44.773,-100 100,-100 v 0 h 120 v 0 c 0,55.23 44.773,100 100,100 h 980 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 H 440 c -55.227,0 -100,44.77 -100,100 v 0 m 1180,0 h 120 v 0 c 55.23,0 100,44.77 100,100 v 200 m -1620,0 h 100 288 120 v 0 c 0,55.23 44.773,100 100,100 h 404 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 H 728 c -55.227,0 -100,44.77 -100,100 v 0 m 604,0 h 120 388 m -1620,0 v 200 c 0,55.23 44.773,100 100,100 h 288 120 v 0 c 0,55.23 44.773,100 100,100 h 404 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 H 728 c -55.227,0 -100,44.77 -100,100 v 0 m 604,0 h 120 288 c 55.23,0 100,-44.77 100,-100 v -200 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 553.46 V 3000 2900 H 2100 v 100 m 553.48,0 h 120 m -793.48,0 v 200 c 0,55.23 44.77,100 100,100 h 76.74 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 76.74 c 55.23,0 100,-44.77 100,-100 v -200 h 120 M 1860,3000 v 350 c 0,55.23 44.77,100 100,100 h 356.74 120 356.74 c 55.22,0 100,-44.77 100,-100 v -350 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. rubric:: Rules

The following rules apply when you call the ``CLEANUP`` statement.

-  When you apply the ``CLEANDEPENDENTS`` statement to a set, all
   inactive elements are discarded from the set itself and from all of
   its subsets. In addition, AIMMS will discard all inactive data
   throughout the model caused by the changes to the set.

-  When you apply the ``CLEANUP`` statement to a parameter or variable,
   all inactive data associated with the identifier is removed. This
   includes inactive data that is caused by changes in domain and range
   sets, as well as data that has become inactive by changes in the
   domain condition of the identifier.

-  When you apply the ``CLEANDEPENDENTS``, ``CLEANUP``, or ``REBUILD``
   statement to a section, AIMMS will remove the inactive data of all
   sets, or parameters and variables declared in it, respectively.

After using the ``CLEANUP`` or ``CLEANDEPENDENTS`` statement for a
particular identifier, all its associated inactive data is permanently
lost.

.. rubric:: Resorting root set elements

In addition to discarding inactive data from your model that is caused
by the existence of inactive elements in a root set, the
``CLEANDEPENDENTS`` operator will also completely resort a root set and
all data defined of it whenever possible and necessary. The following
rules apply.

-  Resorting will only take place if the current storage order of a root
   set differs from its current ordering principle.

-  AIMMS will not resort sets for which explicit elements are used in
   the model formulation.

As a call to ``CLEANDEPENDENTS`` requires a complete rebuild of all
identifiers defined over the root sets involved, the ``CLEANDEPENDENTS``
statement may take a relatively long time to complete. For a more
detailed description of the precise manner in which root set elements
and multidimensional data is stored in AIMMS refer to
:ref:`sec:eff.set.ordering`. This section also explains the benefits of
resorting a root set.

.. rubric:: Generated Mathematical Programs

The ``CLEANDEPENDENTS`` statement will also check whether any variable
or constraint is affected; and if so will remove any generated
mathematical program that is generated from such a variable or
constraint.

.. rubric:: Restricted usage in AIMMS GUI

You should not call the ``CLEANDEPENDENTS`` statement in procedures that
have been linked to edit actions in graphical objects in an AIMMS
end-user GUI via the **Procedures** tab of the object **Properties**
dialog box. During these actions, AIMMS does not expect the element
numbering to change.

.. rubric:: Efficiency considerations

If you want to apply the ``CLEANDEPENDENTS`` statement to multiple sets,
applying the operation to all sets in a single call of the
``CLEANDEPENDENTS`` statement will, in general, be more efficient than
using a separate call for every single set. If an identifier depends on
two or more of the sets to which you want to apply the
``CLEANDEPENDENTS`` operation, the data of such an identifier will only
be traversed and/or rebuild once, rather than multiple times.

.. rubric:: Examples

-  The following ``CLEANDEPENDENTS`` statement will remove all data from
   your application that depends on the removed element ``'Amsterdam'``,
   including, for instance, all previously assigned values to
   ``Transport`` departing from or arriving at ``'Amsterdam'``.

   .. code-block:: aimms
   
   	Cities -= 'Amsterdam' ;
   
   	cleandependents Cities ;

-  The following ``CLEANUP`` statement will remove the data of the
   identifier ``Transport`` for all tuples that either lie outside the
   current contents of ``Cities``, or do not satisfy the domain
   restriction.

   .. code-block:: aimms
   
   	cleanup Transport;

-  Consider a parameter ``A(i,j)`` where ``i`` is an index into a set
   ``S`` and ``j`` an index into a set ``T``, then

   .. code-block:: aimms
   
   	cleandependents S,T;

   will be more efficient than

   .. code-block:: aimms
   
   	cleandependents S;
   	cleandependents T;

   because the latter may require ``A(i,j)`` to be rebuilt twice.

.. _findusedelements-LR:

.. rubric:: Finding used elements

When you want to remove the elements in a set that are no longer used in
your application, you first have to make sure which elements are
currently in use. To find these elements easily, AIMMS provides the
procedure :any:`FindUsedElements`. It has the following three arguments:

-  a set *SearchSet* for which you want to find the used elements,

-  a subset *SearchIdentifiers* of the predefined set :any:`AllIdentifiers`
   consisting of all identifiers that you want to be investigated, and

-  a subset *UsedElements* of the set *SearchSet* containing the result
   of the search.

Upon execution, AIMMS will return that subset of *SearchSet* for which
the elements are used in the combined data of the identifiers contained
in *SearchIdentifiers*. When the identifiers *SearchSet* and
``UsedElements`` are contained in ``SearchIdentifiers`` they are
ignored.

.. rubric:: Example

The following call to :any:`FindUsedElements` will find the elements of the
set ``Cities`` that are used in the identifiers ``Supply``, ``Demand``,
and ``Distance``, and store the result in the set ``UsedCities``.

.. code-block:: aimms

	SearchIdentifiers := DATA { Supply, Demand, Distance };

	FindUsedElements( Cities, SearchIdentifiers, UsedCities );

If these cities are the only ones of interest, you can place them into
the set ``Cities``, and thereby overwrite its previous contents. After
that you can cleanup your entire dataset by eliminating data dependent
on cities other than the ones currently contained in the set ``Cities``.
This process is accomplished through the following two statements.

.. code-block:: aimms

	Cities := UsedCities;

	cleandependents Cities;

.. _restoreinactiveelements-LR:

.. rubric:: Finding and restoring inactive elements

Inactive data in AIMMS results when elements are removed from (domain)
sets. Such data will be inaccessible, unless the corresponding set
elements are brought back into the set. When this is necessary, you can
use the procedure :any:`RestoreInactiveElements` provided by AIMMS. This
procedure has the following three arguments:

-  a set *SearchSet* for which you want to verify whether inactive data
   exists,

-  a subset *SearchIdentifiers* of the predefined set :any:`AllIdentifiers`
   consisting of those identifiers that you want to be investigated, and

-  a subset *InactiveElements* of the set *SearchSet* containing the
   result of the search.

Upon execution AIMMS will find all elements for which inactive data
exists in the identifiers in *SearchIdentifiers*. The elements found
will not only be placed in the result set *InactiveElements*, but also
be added to the search set. This latter extension of *SearchSet* implies
that the corresponding inactive data is restored.

.. rubric:: Example

The following call to :any:`RestoreInactiveElements` will verify whether
inactive data exists for the set ``Cities`` in :any:`AllIdentifiers`.

.. code-block:: aimms

	RestoreInactiveElements( Cities, AllIdentifiers, InactiveCities );

After such a call the set ``InactiveCities`` could contain the element
``'Amsterdam'``. In this case, the set ``Cities`` has been extended with
``'Amsterdam'`` as well. If you subsequently decide that cleaning up the
set ``Cities`` is harmless, the following two statements will do the
trick.

.. code-block:: aimms

	Cities -= InactiveCities;

	cleandependents Cities;

.. rubric:: Reclaiming memory

If the cardinality of a multidimensional identifier in your model
decreases, AIMMS will not automatically reclaim the memory that is freed
up because of the decreased amount of data to store. Instead, it will
keep the memory available to store additional data that is associated
with subsequent changes to the identifier. If the cardinality of an
identifier decreases dramatically during a run the of a model, this may
lead to a huge amount of memory getting stuck up with a single
identifier in your model.

.. rubric:: Memory fragmentation

In addition, if a model is running for a prolonged period of time, and
an identifier has undergone huge amounts of structural changes during
that time, the memory associated with that identifier may become heavily
fragmented. In the long run, memory fragmentation may lead to decreased
performance of your model. Rebuilding the internal data structures
associated with such an identifier will resolve the fragmentation
problem.

.. rubric:: Automatic reclamation

Prior to solving a mathematical program, AIMMS will perform a quick
check comparing the total amount of memory used by an identifier to the
amount of unused memory associated with that identifier. By adding to
and removing elements from identifiers, memory may become fragmented and
the fraction of unused memory may grow. If the fraction of unused memory
compared to the total amount of memory in use becomes too large, AIMMS
will automatically rebuild such an identifier in order to reclaim the
unused memory. AIMMS will also reclaim the memory of an identifier
whenever it becomes empty during the run of a model.

.. rubric:: the ``REBUILD`` statement

Through the ``REBUILD`` statement you can manually instruct AIMMS to
rebuild the internal data structures associated with one or more
identifiers. During the ``REBUILD`` statement AIMMS uses a more thorough
check to verify whether a rebuild of an identifier is worthwhile prior
to solving a mathematical program.