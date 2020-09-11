.. _sec:mp.solve:

The ``SOLVE`` Statement
=======================

.. _solve:

.. rubric:: The ``SOLVE`` statement

With the ``SOLVE`` statement you can instruct AIMMS to compute the
solution of a ``MathematicalProgram``, resulting in the following
actions.

-  AIMMS determines which solution method(s) are appropriate, and checks
   whether the specified type is also appropriate.

-  AIMMS then generates the Jacobian matrix (first derivatives of all
   the constraints), the bounds on all variables and constraints, and an
   objective where appropriate.

-  AIMMS communicates the problem to an underlying solver that is able
   to perform the chosen solution method.

-  AIMMS finally reads the computed solution back from the solver.

.. rubric:: Syntax

In addition to initiating the solution process of a
``MathematicalProgram``, you can also use the ``SOLVE`` statement to
provide local overrides of particular AIMMS settings that influence the
way in which the solution process takes place. The syntax of the
``SOLVE`` statement follows.

.. _solve-statement:

*solve-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 493.47734 207.2"
	   height="207.2"
	   width="493.47733"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,1213.6)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,9000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,896)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">SOLVE</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 580,9000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 700,9000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,75,896)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1253.48,9000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1493.48,9000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,154.348,896)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">IN</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1737.48,9000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1977.48,9000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,202.748,896)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">REPLACE</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2581.48,9000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1857.48,9000 -20,-50 h 40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2049.48,8700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g58"><text
	           id="text62"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,209.948,866)"><tspan
	             id="tspan60"
	             y="0"
	             x="0">MERGE</tspan></text>
	</g><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2509.48,8700 50,-20 v 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2701.48,9000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2821.48,9000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g70"><text
	           id="text74"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,287.148,896)"><tspan
	             id="tspan72"
	             y="0"
	             x="0">MODE</tspan></text>
	</g><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3209.48,9000 50,-20 v 40" /><path
	         id="path78"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1373.48,9000 -20,-50 h 40" /><path
	         id="path80"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3329.48,9000 -20,-50 h 40" /><path
	         id="path82"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="m 3449.48,9000 h 240" /><path
	         id="path84"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:40, 20;stroke-dashoffset:0;stroke-opacity:1"
	         d="M 250,8000 H 490" /><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 730,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g88"><text
	           id="text92"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,78,796)"><tspan
	             id="tspan90"
	             y="0"
	             x="0">WHERE</tspan></text>
	</g><path
	         id="path94"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1190,8000 50,-20 v 40" /><path
	         id="path96"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1430,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g98"><text
	           id="text102"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,148,796)"><tspan
	             id="tspan100"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/execution-statements/the-option-and-property-statements.html#option">option</a></tspan></text>
	</g><path
	         id="path104"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1856.88,8000 50,-20 v 40" /><path
	         id="path106"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1976.88,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g108"><text
	           id="text112"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,202.688,796)"><tspan
	             id="tspan110"
	             y="0"
	             x="0">:=</tspan></text>
	</g><path
	         id="path114"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2220.88,8000 50,-20 v 40" /><path
	         id="path116"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2340.88,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g118"><text
	           id="text122"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,239.088,796)"><tspan
	             id="tspan120"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/index.html#expression">expression</a></tspan></text>
	</g><path
	         id="path124"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3021.08,8000 50,-20 v 40" /><path
	         id="path126"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1310,8000 20,50 h -40" /><path
	         id="path128"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2125.54,8300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g130"><text
	           id="text134"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,218.954,826)"><tspan
	             id="tspan132"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path136"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2325.54,8300 50,-20 v 40" /><path
	         id="path138"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3141.08,8000 20,50 h -40" /><path
	         id="path140"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 610,8000 -20,-50 h 40" /><path
	         id="path142"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3261.08,8000 -20,-50 h 40" /><path
	         id="path144"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3381.08,8000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g146"><text
	           id="text150"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,344.508,796)"><tspan
	             id="tspan148"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path152"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3581.08,8000 50,-20 v 40" /><path
	         id="path154"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3701.08,8000 -50,20 v -40" /><path
	         id="path156"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,9000 h 120 v 0 c 0,55.23 44.773,100 100,100 h 260 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 220 c -55.227,0 -100,44.77 -100,100 v 0 m 460,0 h 120 v 100 h 553.46 V 9000 8900 H 700 v 100 m 553.48,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 404 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -404 c -55.23,0 -100,44.77 -100,100 v 0 m 604,0 h 120 m -844,0 v -200 c 0,-55.23 44.77,-100 100,-100 h -28 120 v 0 c 0,55.23 44.77,100 100,100 h 260 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -260 c -55.23,0 -100,44.77 -100,100 v 0 m 460,0 h 120 -28 c 55.23,0 100,44.77 100,100 v 200 h 120 v 0 c 0,55.23 44.77,100 100,100 h 188 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -188 c -55.23,0 -100,44.77 -100,100 v 0 m 388,0 h 120 m -1956,0 v -350 c 0,-55.23 44.77,-100 100,-100 h 818 120 818 c 55.23,0 100,44.77 100,100 v 350 h 120 M 490,8000 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.773,100 100,100 h 260 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 H 830 c -55.227,0 -100,44.77 -100,100 v 0 m 460,0 h 120 m 0,0 v 0 h 120 v 100 h 426.87 V 8000 7900 H 1430 v 100 m 426.88,0 h 120 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.77 -100,100 v 0 m 244,0 h 120 v 100 h 680.19 v -100 -100 h -680.19 v 100 m 680.2,0 h 120 M 1310,8000 v 200 c 0,55.23 44.77,100 100,100 h 595.54 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 595.54 c 55.22,0 100,-44.77 100,-100 v -200 h 120 M 610,8000 v -350 c 0,-55.23 44.773,-100 100,-100 h 1165.54 120 1165.54 c 55.22,0 100,44.77 100,100 v 350 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. rubric:: Replace and merge mode

You can instruct AIMMS to read back the solution in either *replace* or
*merge* mode. If you do not specify a mode, AIMMS assumes replace mode.
In replace mode AIMMS will, before reading back the solution of the
mathematical program, remove the values of the variables in the
``Variables`` set of the mathematical program for all index tuples
except those that are fixed

-  because they are not within their current domain (i.e. inactive),

-  through the ``NonvarStatus`` attribute or the ``.NonVar`` suffix of
   the variable,

-  because they are outside the planning interval of a ``Horizon`` (see
   :ref:`sec:time.horizon`), or

-  because their upper and lower bounds are equal.

In merge mode AIMMS will only replace the *individual variable values*
involved in the mathematical program. This mode is very useful, for
instance, when you are iteratively solving subproblems which correspond
to slices of the symbolic variables in your model.

.. rubric:: Infeasible and unbounded problems

Whenever the invoked solver finds that a mathematical program is
infeasible or unbounded, AIMMS will assign one of the special values
``na``, ``inf`` or ``-inf`` to the objective variable. For you, this
will serve as a reminder of the fact that there is a problem even when
you do not check the ``ProgramStatus`` and ``SolverStatus`` suffices.
For all other variables, AIMMS will read back the last values computed
by the solver just before returning with infeasibility or unboundedness.

.. rubric:: Temporary option settings

Sometimes you may need some temporary option settings during a single
``SOLVE`` statement. Instead of having to change the relevant options
using the ``OPTION`` statement and set them back afterwards, AIMMS also
allows you to specify values for options that are used only during the
current ``SOLVE`` statement. The syntax is similar to that of the
``OPTION`` statement.

.. rubric:: Also for attributes

Apart from specifying temporary option settings you can also use the
``WHERE`` clause to override the ``type`` and ``direction`` attributes
specified in the declaration of the mathematical program, as well as the
``solver`` to use for the solution process.

.. rubric:: Example

The following ``SOLVE`` statement selects ``'cplex'`` as its solver,
sets the model type to ``'rmip'``, and sets the CPLEX option
``LpMethod`` to ``'Barrier'``.

.. code-block:: aimms

	solve TransportModel in replace mode
	    where solver    := 'cplex',
	          type      := 'rmip',
	          LpMethod  := 'Barrier' ;