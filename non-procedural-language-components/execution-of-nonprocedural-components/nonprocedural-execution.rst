.. _sec:nonproc.exec:

Nonprocedural Execution
=======================

.. rubric:: Execution based on definitions

Execution based on definitions is typically not controlled by the user.
It takes place automatically, but only when up-to-date values of defined
sets or parameters are needed. Basically, execution can be triggered
automatically from within:

-  the body of a function or procedure, or

-  an object in the graphical user interface.

.. rubric:: Relating definitions and procedures

Consider a set or a parameter with a definition which is referenced in
an execution statement inside a function or a procedure. Whenever the
value of such a set or parameter is not up-to-date due to previous data
changes, AIMMS will compute its current value just prior to executing
the corresponding statement. This mechanism ensures that, during
execution of functions or procedures, the functional relationships
expressed in the definitions are always valid.

.. rubric:: Lazy evaluation

During execution AIMMS minimizes its efforts and updates only those
values of defined identifiers that are needed at the current point of
execution. Such *lazy evaluation* can avoid unnecessary computations and
reduces computational time significantly when the number of dependencies
is large, and when relatively few dependencies need to be resolved at
any particular point in time.

.. rubric:: GUI requests

For the graphical objects in an end-user interface you may specify
whether the data in that object must be up-to-date at all times, or just
when the page containing the object is opened. AIMMS will react
accordingly, and automatically update all corresponding identifiers as
specified.

.. _currentautoupdateddefinitions-LR:

.. _alldefinedsets-LR:

.. _alldefinedparameters-LR:

.. rubric:: The set :any:`CurrentAutoUpdatedDefinitions`

Which definitions are automatically updated in the graphical user
interface whenever they are out-of-date, is determined by the contents
of the predefined set :any:`CurrentAutoUpdatedDefinitions`. This set is a
subset of the predefined set :any:`AllIdentifiers`, and is initialized by
AIMMS to the union of the sets :any:`AllDefinedSets` and
:any:`AllDefinedParameters` by default.

.. rubric:: Exclude from auto-updating

To prevent auto-updating of particular identifiers in your model, you
should remove such identifiers from the set
:any:`CurrentAutoUpdatedDefinitions`. You can change its contents either
from within the language or from within the graphical user interface.
Typically, you should exclude those identifiers from auto-updating whose
computation takes a long time to finish. Instead of waiting for their
computation on every input change, it makes much more sense to collect
all input changes for such identifiers and request their re-computation
on demand.

.. rubric:: Requesting updates

All identifiers that are not contained in
:any:`CurrentAutoUpdatedDefinitions` must be updated manually under your
control. AIMMS provides several mechanisms:

-  you can call the ``UPDATE`` statement from within the language, or

-  you can attach update requests of particular identifiers as actions
   to buttons and pages in the end-user interface.

.. _update:

.. rubric:: The ``UPDATE`` statement

The ``UPDATE`` statement can be used to update the contents of one or
more identifiers during the execution of a procedure that is called by
the user. In this way, selected identifiers which are shown in the
graphical user interface and not kept up-to-date automatically, can be
made up-to-date once the procedure is activated by the user.

.. _update-statement:

.. rubric:: Syntax

*update-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 299.39735 73.866661"
	   height="73.866661"
	   width="299.39734"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,193.6)"
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
	             x="0">UPDATE</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 652,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1012,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,106.2,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1565.48,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 892,1000 20,50 h -40" /><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1188.74,1300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,125.274,126)"><tspan
	             id="tspan40"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1388.74,1300 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1685.48,1000 20,50 h -40" /><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 772,1000 20,50 h -40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1805.48,1000 20,50 h -40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1925.48,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g54"><text
	           id="text58"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,198.948,96)"><tspan
	             id="tspan56"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2125.48,1000 50,-20 v 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2245.48,1000 -50,20 v -40" /><path
	         id="path64"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 120 v 0 c 0,55.23 44.773,100 100,100 h 332 c 55.227,0 100,-44.77 100,-100 v 0 0 C 652,944.773 607.227,900 552,900 H 220 c -55.227,0 -100,44.773 -100,100 v 0 m 532,0 h 120 m 0,0 v 0 h 120 m 0,0 v 0 h 120 v 100 h 553.46 V 1000 900 H 1012 v 100 m 553.48,0 h 120 M 892,1000 v 200 c 0,55.23 44.773,100 100,100 h 76.74 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 76.74 c 55.22,0 100,-44.77 100,-100 v -200 h 120 M 772,1000 v 350 c 0,55.23 44.773,100 100,100 h 356.74 120 356.74 c 55.22,0 100,-44.77 100,-100 v -350 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.773 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. rubric:: Allowed identifiers

The following selections of identifiers are allowed in the ``UPDATE``
statement:

-  identifiers with a definition,

-  identifiers associated with a structural section in the model-tree,
   and

-  identifiers in a subset of the predefined set :any:`AllIdentifiers`.

.. rubric:: Example

The following execution statement inside a procedure will trigger AIMMS
to update the values of the identifiers ``FixedCost``, ``VariableCost``
and ``TotalCost`` upon execution.

.. code-block:: aimms

	Update FixedCost, VariableCost, TotalCost;