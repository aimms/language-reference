.. _sec:extern.declaration:

Declaration of External Procedures and Functions
================================================

.. _external_procedure:

.. _external_function:

.. rubric:: External procedures and functions

External procedures and functions are special types of nodes in the
model tree. They have the same attributes as internal procedures and
functions with the exception of the ``Body`` and ``Derivative``
attributes, which are replaced by the attributes in
:numref:`table:extern.attr`.

.. _table:extern.attr:

.. table:: Additional attributes of external procedures and functions

   +--------------------+--------------------------------------+-----------------------------+
   | Attribute          | Value-type                           | See also page               |
   +====================+======================================+=============================+
   | ``DllName``        | *string*, *file-identifier*          |                             |
   +--------------------+--------------------------------------+-----------------------------+
   | ``ReturnType``     | ``integer``, ``double``              |                             |
   +--------------------+--------------------------------------+-----------------------------+
   | ``Property``       | ``FortranConventions``, ``UndoSafe`` | :ref:`here <attr:undosafe>` |
   +--------------------+--------------------------------------+-----------------------------+
   | ``BodyCall``       | *external-call*                      |                             |
   +--------------------+--------------------------------------+-----------------------------+
   | ``DerivativeCall`` | *external-call*                      |                             |
   +--------------------+--------------------------------------+-----------------------------+

.. _external_procedure.dll_name:

.. _external_function.dll_name:

.. rubric:: The ``DllName`` attribute

With the mandatory ``DllName`` attribute you can specify the name of the
DLL which contains the external procedure or function to which you want
to make a link in your AIMMS application. The value of the attribute
must be a string, a string parameter, or a ``File`` identifier,
representing the path to the external DLL.

.. rubric:: Search path

If you only specify a DLL name, AIMMS will search for the DLL in all
directories in the ``AIMMSUSERDLL`` environment variable, and the
``PATH`` environment variable on Windows, or the ``LD_LIBRARY_PATH``
environment variables on Linux, respectively. In addition, on Windows,
AIMMS will also search for the DLL in the project folder. If you specify
a relative path including a folder (possibly ./), AIMMS will take this
path relative to the project folder. If you specify an absolute path,
AIMMS will try to open the DLL at the specified location.

.. rubric:: ``File`` identifier and unit conventions

When you use a ``File`` identifier to specify an external DLL name,
AIMMS will use the ``Convention`` attribute of that ``File`` identifier
(if specified) to pass numeric values to any procedure or function in
that DLL according to the specified unit convention (see also
:ref:`sec:units.convention`). When the DLL name has not been specified
through a ``File`` identifier, or when its ``Convention`` attribute is
left empty, AIMMS will use the unit convention specified for the main
model.

.. rubric:: Default argument scaling

Without any such convention, AIMMS will use the default convention,
i.e. arguments will be scaled according to the unit specified for each
argument, and AIMMS will assume that the result of an external function
is scaled according to the unit specified in its Unit attribute.
Unit analysis for functions and procedures is discussed in full detail
in :ref:`sec:units.analysis.arg`.

.. _external_procedure.return_type:

.. _external_function.return_type:

.. rubric:: The ``ReturnType`` attribute

The ``ReturnType`` indicates the type of any *scalar* numerical value
returned by the DLL function. The possible values are ``integer`` and
``double``. AIMMS will use the value returned by the DLL function either
as the return value of the ``ExternalProcedure``, or as the (numerical)
function value of the ``ExternalFunction``, whichever is applicable. If
you do not specify the ``ReturnType`` attribute, AIMMS will discard any
value returned by the function.

.. rubric:: Restricted use

You cannot directly use the returned value of a DLL function as the
function value of an ``ExternalFunction`` when its return value is
either an indexed parameter, a set, a set element or a string. In such
cases you must pass the function name as an additional external argument
to the DLL function, and specify how the function value must be dealt
with.

.. rubric:: Example

Consider a ``C`` function ``Cobb_Douglas_Arg`` with prototype

.. code-block:: aimms

	void Cobb_Douglas_Arg( int n, double *a, double *c, double *CDValue );

which passes the Cobb-Douglas function value through the argument
``CDValue`` instead of as the return value. In this example ``CDValue``
is a scalar, which could have been passed as the result of the DLL
function as well. The following ``ExternalFunction`` declaration
provides a link with ``Cobb_Douglas_Arg`` and obtains its function value
via the argument list.

.. code-block:: aimms

	ExternalFunction CobbDouglasArgument {
	    Arguments     : (a,c);
	    Range         : nonnegative;
	    DllName       : "Userfunc.dll";
	    BodyCall      : {
	        Cobb_Douglas_Arg( card : InputFactors, array: a, array: c,
	            scalar: CobbDouglasArgument );
	    }
	}

.. _external_procedure.property:

.. _external_function.property:

.. rubric:: The ``Property`` attribute

With the ``Property`` attribute you can specify through the
``FortranConventions`` property whether the external function is based
on ``FORTRAN`` calling conventions. By default, AIMMS will assume that
the DLL function is written in a ``C``-like languages such as ``C``, ++
or ``PASCAL``. The precise differences between both calling conventions
are explained in full detail in :ref:`sec:extern.language`. In addition,
for external procedures, you can specify the ``UndoSafe`` property. The
semantics of the ``UndoSafe`` property is discussed in
:ref:`sec:intern.proc`.

.. rubric:: Formal argument types

As with internal procedures and functions, all formal arguments of an
external procedure or function must be declared as local identifiers.
AIMMS supports the following identifier types for formal arguments of
external procedures and functions:

-  simple sets and relations,

-  scalar and indexed ``Parameters``,

-  scalar and indexed ``Variables`` (external functions only), and

-  ``Handles`` (external procedures only).

.. rubric:: Argument handling

Many details regarding the handling of arguments of internal procedures
and functions also apply to external procedures and functions. Thus,
arguments of external procedures and functions can be defined over
global and local sets, and their associated units of measurement can be
specified in terms of either global units or locally defined unit
parameters, completely similar to internal procedures and functions (see
:ref:`sec:intern.proc`).

.. _handle:

.. rubric:: ``Handle`` arguments

The ``Handle`` identifier type is only supported for formal arguments of
external procedures, i.e. it is not possible to declare global
identifiers of type ``Handle``. The following rules apply:

-  ``Handle`` arguments are always declared as scalar local identifiers,

-  ``Handle`` arguments can only be passed to the DLL function as an
   integer ``Handle`` (see below), and

-  the actual argument in a call to the external procedure corresponding
   to a formal ``Handle`` argument can be a (sliced) reference to an
   identifier in your model *of any type and of any dimension*.

``Handle`` arguments allow you to completely circumvent any type
checking on actual arguments with respect to the dimension and the
respective index domains of the corresponding formal arguments in the
call to an external procedure. As a result of this, however, the actual
data transfer of ``Handle`` arguments to the DLL function must
completely take place via the AIMMS API (see also :ref:`chap:api`).

.. _external_procedure.body_call:

.. _external_function.body_call:

.. _DLL-function:

.. rubric:: The ``BodyCall`` attribute

In the mandatory ``BodyCall`` attribute you must specify the call to the
DLL procedure or function, to which the execution of the
``ExternalProcedure`` or ``Function`` must be relayed. Such an external
call specifies:

-  the name of the DLL function or procedure that must be called, and

-  how the actual AIMMS arguments must be translated into arguments
   suitable for the DLL function or procedure.

Any external call must be specified according to the syntax below. In
the Model Explorer, you can specify all components of the ``BodyCall``
attribute using a wizard which will guide you through most of the
necessary detail.

.. _external-call:

.. rubric:: Syntax

*external-call:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 432.528 93.866661"
	   height="93.866661"
	   width="432.52798"
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
	         d="m 110,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,16,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/external-procedures-and-functions/declaration-of-external-procedures-and-functions.html#DLL-function">DLL-function</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 890.281,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1110.28,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,117.428,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1310.28,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1530.28,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,158.028,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/external-procedures-and-functions/declaration-of-external-procedures-and-functions.html#external-argument">external-argument</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2603.96,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1420.28,2000 20,50 h -40" /><path
	         id="path46"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1967.12,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g48"><text
	           id="text52"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,203.112,226)"><tspan
	             id="tspan50"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2167.12,2300 50,-20 v 40" /><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2713.96,2000 20,50 h -40" /><path
	         id="path58"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2823.96,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g60"><text
	           id="text64"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,288.796,196)"><tspan
	             id="tspan62"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3023.96,2000 50,-20 v 40" /><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1000.28,2000 -19.999,-50 h 39.999" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3133.96,2000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3243.96,2000 -50,20 v -40" /><path
	         id="path74"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 110 v 100 H 890.262 V 2000 1900 H 110 v 100 m 780.281,0 h 109.999 m 0,0 v 0 h 110 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 110 m 0,0 v 0 h 110 v 100 H 2603.93 V 2000 1900 H 1530.28 v 100 m 1073.68,0 h 110 m -1293.68,0 v 200 c 0,55.23 44.77,100 100,100 h 336.84 110 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 110 336.84 c 55.23,0 100,-44.77 100,-100 v -200 h 110 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 110 m -2133.68,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 911.84 110 911.84 c 55.23,0 100,44.77 100,100 v 200 h 110" /></g></g></svg></div>

.. _external-argument:

*external-argument:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 500.53868 133.86667"
	   height="133.86667"
	   width="500.53867"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,706.93332)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,5000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 400,4400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,45,436)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/external-procedures-and-functions/declaration-of-external-procedures-and-functions.html#translation-modifier">translation-modifier</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1520.24,4400 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1720.24,5000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,5000 -20,-50 h 40" /><path
	         id="path30"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 426.582,4700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g32"><text
	           id="text36"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,47.6582,466)"><tspan
	             id="tspan34"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/external-procedures-and-functions/declaration-of-external-procedures-and-functions.html#external-data-type">external-data-type</a></tspan></text>
	</g><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1493.66,4700 50,-20 v 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1720.24,5000 -20,-50 h 40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 499.961,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g44"><text
	           id="text48"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,54.9961,496)"><tspan
	             id="tspan46"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/external-procedures-and-functions/declaration-of-external-procedures-and-functions.html#translation-type">translation-type</a></tspan></text>
	</g><path
	         id="path50"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1420.28,5000 50,-20 v 40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,5000 20,50 H 80" /><path
	         id="path54"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.24,5000 20,50 h -40" /><path
	         id="path56"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1920.24,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g58"><text
	           id="text62"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,198.424,496)"><tspan
	             id="tspan60"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2120.24,5000 50,-20 v 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2220.24,5000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g68"><text
	           id="text72"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,227.024,496)"><tspan
	             id="tspan70"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/external-procedures-and-functions/declaration-of-external-procedures-and-functions.html#actual-external-argument">actual-external-argument</a></tspan></text>
	</g><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3654.04,5000 50,-20 v 40" /><path
	         id="path76"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3754.04,5000 -50,20 v -40" /><path
	         id="path78"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,5000 h 100 m 0,0 v 0 h 100 m 0,0 v -500 c 0,-55.23 44.773,-100 100,-100 v 0 h 100 v 100 H 1520.2 V 4400 4300 H 400 v 100 m 1120.24,0 h 100 v 0 c 55.22,0 100,44.77 100,100 v 500 M 200,5000 v -200 c 0,-55.23 44.773,-100 100,-100 h 26.582 100 v 100 H 1493.64 V 4700 4600 H 426.582 v 100 m 1067.078,0 h 100 26.58 c 55.23,0 100,44.77 100,100 v 200 M 200,5000 h 100 99.961 100 v 100 H 1420.26 V 5000 4900 H 499.961 v 100 m 920.319,0 h 100 199.96 100 M 100,5000 v 200 c 0,55.23 44.773,100 100,100 h 710.121 99.999 710.12 c 55.22,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.22,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.78,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 v 100 H 3654 V 5000 4900 H 2220.24 v 100 m 1433.8,0 h 100" /></g></g></svg></div>

.. _translation-type:

.. rubric:: Mandatory translation type

The mandatory translation type indicates the type of the external
argument into which the actual argument must be translated before being
passed to the external procedure. The following translation types are
supported.

-  ``scalar``: the actual scalar AIMMS argument is passed on as a
   scalar of the indicated external data type.

-  ``literal``: the literal specified in the external call is passed
   on as a scalar of the indicated external data type, i.e. a
   ``literal`` argument does *never* correspond to an actual AIMMS
   argument, but is specified directly in the ``BodyCall`` attribute.

-  ``array``: the AIMMS argument is passed on as an array of values
   according to the indicated translation type and external data type.
   The precise manner in which the translation takes place is discussed
   below.

-  ``card``: the cardinality of a set argument is passed on as an
   integer value. The set argument can be either a set passed as an
   actual AIMMS argument or the domain set of a multi-dimensional
   parameter passed as an actual argument.

-  ``handle``: an integer handle to a (sliced) set or parameter
   argument is passed on. Within the external procedure you must use
   functions from the AIMMS API (see also :ref:`chap:api`) to obtain the
   dimension, domain and range associated with the handle, or to
   retrieve or change its data values.

-  ``work``: an array of the indicated type is passed as a temporary
   workspace to the external procedure. The actual argument must be an
   integer expression and is interpreted as the size of the array to be
   passed on. This translation type is useful for programmers of
   languages such as standard F77 ``FORTRAN`` which lack facilities for
   dynamic memory allocation.

.. _actual-external-argument:

.. rubric:: Actual external argument

The actual external argument specified in an external argument of the
``BodyCall`` attribute can be

-  a reference to a formal argument of the ``ExternalProcedure`` at hand
   (for the ``scalar``, ``array``, ``card``, ``handle`` and ``work``
   translation types),

-  a reference to a domain set of a formal multi-dimensional argument of
   the ``ExternalProcedure`` at hand (for the ``card`` translation
   type), or

-  an integer, double or string literal (such as ``12345``, ``123.45``
   or ``"This is a string"``) directly specified within the ``BodyCall``
   attribute (for the ``literal`` translation type).

.. rubric:: Input-output type

For every formal argument of an ``ExternalProcedure``, you can specify
its associated *input-output* type through the ``Input``, ``InOut``
(default) or ``Output`` properties in the ``Propert`` attribute of the
local argument declaration. With it, you indicate whether or not AIMMS
should consider any changes made to the argument by the DLL function.
For each input-output type, AIMMS performs the following actions:

-  ``Input``: AIMMS initializes the external argument, but discards
   all changes made to it by the DLL function,

-  ``InOut``: AIMMS initializes the external argument, and passes
   back to the model the values returned by the DLL function, or

-  ``Output``: AIMMS allocates memory for the external argument, but
   does not initialize it; the values returned by the DLL function are
   passed back to the model.

As with internal functions, all ``ExternalFunction`` arguments are
``Input`` by definition. The return value of an ``ExternalProcedure``
and the function value of an ``ExternalFunction`` are considered as an
(implicit) ``Output`` argument when passed to the ``DLL`` function as an
external argument.

.. _external-data-type:

.. rubric:: External data type

In translating AIMMS arguments into values (or arrays of values)
suitable as arguments for an external procedure or function, AIMMS
supports the external data types listed in
:numref:`table:extern.external-types`.

.. _table:extern.external-types:

.. table:: External data types

   ================== =======================================
   External data type Passed as
   ================== =======================================
   ``integer``        4-byte (signed) integer
   ``double``         8-byte double precision floating number
   ``string``         ``C``-style string
   ``integer8``       1-byte (signed) integer
   ``integer16``      2-byte (signed) integer
   ``integer32``      4-byte (signed) integer
   ================== =======================================

.. rubric:: Allowed combinations

Not all combinations of input-output types, translation types and
external data types are supported (or even useful).
:numref:`table:extern.translation-types` describes all allowed
combinations, as well as the resulting argument type that is passed on
to the external procedure. The external data types printed in bold are
the default, and can be omitted if appropriate. Throughout the table,
the data type ``integer`` can be replaced by any of the other integer
types ``integer8``, ``integer16`` or ``integer32``.

.. _table:extern.translation-types:

.. table:: Allowed combinations of translation, input-output and data types
   
   +--------------------------------------------+------------------------+-----------------+
   | Allowed types                              | AIMMS argument         | Passed as       |
   +--------------+--------------+--------------+                        |                 |
   | Translation  | Input-Output | Data         |                        |                 |
   +==============+==============+==============+========================+=================+
   | ``scalar``   | ``input``    | ``integer``  | scalar expression      | integer         |
   |              |              +--------------+                        +-----------------+
   |              |              | **double**   |                        | double          |
   |              |              +--------------+                        +-----------------+
   |              |              | ``string``   |                        | string          |
   |              +--------------+--------------+------------------------+-----------------+
   |              | **inout**,   | ``integer``  | scalar reference       | integer pointer |
   |              | ``output``   +--------------+                        +-----------------+
   |              |              | **double**   |                        | double pointer  |
   |              |              +--------------+                        +-----------------+
   |              |              | ``string``   |                        | string          |
   +--------------+--------------+--------------+------------------------+-----------------+
   | ``literal``  | *n/a*        | ``integer``  | *n/a*                  | integer         |
   |              |              +--------------+                        +-----------------+
   |              |              | **double**   |                        | double          |
   |              |              +--------------+                        +-----------------+
   |              |              | ``string``   |                        | string          |
   +--------------+--------------+--------------+------------------------+-----------------+
   | ``card``     | *n/a*        | *n/a*        | set, parameter         | integer         |
   +--------------+--------------+--------------+------------------------+-----------------+
   | ``array``    | ``input``,   | ``integer``  | parameter              | integer array   |
   |              | **inout**,   +--------------+                        +-----------------+
   |              | ``output``   | **double**   |                        | double array    |
   |              |              +--------------+------------------------+-----------------+
   |              |              | **integer**  | element parameter      | integer array   |
   |              |              +--------------+------------------------+-----------------+
   |              |              | ``string``   | set                    | string array    |
   |              |              +--------------+------------------------+-----------------+
   |              |              | **string**   | string/unit parameter  | string array    |
   +--------------+--------------+--------------+------------------------+-----------------+
   | ``handle``   | ``input``,   | *n/a*        | set, parameter, handle | integer         |
   |              | **inout**,   |              |                        |                 |
   |              | ``output``   |              |                        |                 |
   +--------------+--------------+--------------+------------------------+-----------------+
   | ``work``     | *n/a*        | ``integer``  | integer expression     | integer array   |
   |              |              +--------------+                        +-----------------+
   |              |              | **double**   |                        | double array    |
   +--------------+--------------+--------------+------------------------+-----------------+

.. rubric:: Passing array arguments

When you are passing a multidimensional AIMMS identifier to an external
procedure or function as a ``array`` argument, AIMMS passes a
one-dimensional buffer in which all values are stored in a manner that
is compatible with the storage of multidimensional arrays in the
language which you have specified through the ``Property`` attribute.
The precise array numbering conventions for both ``C``-like and
``FORTRAN`` arrays are explained in :ref:`sec:extern.language`.

.. _string_parameter.encoding:

.. rubric:: Encoding of string arguments

The strings communicated with your DLL have an encoding. This encoding
is set by the option ``external_string_character_encoding``, which has a
default of ``UTF8``. This option can be overridden by using the
``Encoding`` attribute of string parameters, similar to the ``Encoding``
attribute of a ``File``, see :ref:`attr.file.encoding`. On Windows,
using the encoding ``UTF-16LE`` and on Linux, using the encoding
``UTF-32LE``, the strings are passed as a ``wchar_t*`` array, otherwise
the strings are passed as a ``char *`` array.

.. _String.Passed.BufferSize:

.. rubric:: Output string arguments

When you pass a scalar or multidimensional output string argument, AIMMS
will pass a single ``char`` buffer of fixed length, or an array of such
buffers. The length is determined by the option ``external``
``function`` ``string`` ``buf`` ``size``. The default of this option is
2048. You must use the ``C`` function ``strcpy`` or a similar function
to copy the string data in your DLL to the appropriate ``char`` buffer
associated with the output string argument.

.. rubric:: Full versus sparse data transfer

When considering your options on how to pass a high-dimensional
parameter to an external procedure, you will find that passing it as an
array is often not the best solution. Not only will the memory
requirements grow rapidly for increasing dimension, but also running
over all elements in the array inside your DLL function may turn out to
be a very time-consuming process. In such a case, it is much better
practice to pass the argument as an integer ``handle``, and use the
AIMMS API functions discussed in :ref:`sec:api.value` to retrieve only
the nondefault values associated with the handle. You can then set up
your own sparse data structures to deal with high-dimensional parameters
efficiently.

.. _translation-modifier:

.. rubric:: Translation modifiers ...

In addition to the translation types, input-output types and external
data types you can specify one or more translation modifiers for each
external argument. Translation modifiers allow you to slightly modify
the manner in which AIMMS will pass the arguments to the DLL function.
AIMMS supports translation modifiers for specifying the precise manner
in which

-  special values,

-  the data associated with handles, and

-  set elements,

are passed.

.. rubric:: ... for special values

When a parameter or variable that you want to pass to an external DLL
contains special values like ``ZERO`` or ``INF``, AIMMS will, by
default, pass ``ZERO`` as 0.0, ``INF`` and ``-INF`` as
:math:`\pm`\ 1.0e150, and will not pass any of the values ``NA`` and
``UNDF``. When you specify the translation modifier ``retainspecials``,
AIMMS will pass all special numbers by their internal representation as
a double precision floating point number. You can use the AIMMS API
functions discussed in :ref:`sec:api.value` to obtain the :any:`MapVal`
value (see also :numref:`table:expr.arith-ext`) associated with each
number. The translation modifier ``retainspecials`` can be specified for
numeric arguments that are passed either as a full array or as an
integer handle.

.. rubric:: ... for handles

When passing a multidimensional identifier handle to an external DLL,
AIMMS can provide several methods of access to the data associated with
the handle by specifying one of the following translation modifiers:

-  ``ordered``: the data retrieval functions will pass the data values
   according to the particular ordering imposed any of the domain sets
   of the identifier associated with the handle. By default, AIMMS will
   use the natural ordering determined by the data entry order of all
   domain sets.

-  ``raw``: the data retrieval functions will also pass inactive data
   (see also :ref:`sec:data.control`). By default, AIMMS will not pass
   inactive data.

The details of ordered versus unordered and raw data transfer are
discussed in full detail in :ref:`sec:api.value`.

.. rubric:: ... for set elements

AIMMS can pass set elements (in the context of element parameters and
sets) to external procedures in various manners. More specifically, set
elements can be translated into:

-  an ``integer`` external data type, or

-  a ``string`` external data type.

When the external data type is ``string``, AIMMS will pass the element
name for each set element. Transfer of element names is always input
only. In general, when the external data type is ``integer``, AIMMS can
pass either

-  the ordinal number with respect to its associated subset domain
   (``ordinalnumber`` modifier), or

-  the element number with respect to its associated root set
   (``elementnumber`` modifier).

Alternatively, when set elements are passed in the context of a set you
can specify the ``indicator`` modifier in combination with the
``integer`` external data type. This will result in the transfer of a
multidimensional binary parameter which indicates whether a particular
tuple is or is not contained in the set.

.. rubric:: Passing element parameters

When you pass an element parameter as an integer ``scalar`` or ``array``
argument, AIMMS will assume the ``ordinalnumber`` modifier by default.
When passed as integer, element parameters can be input, output or inout
arguments. When element parameters are passed as string arguments, they
can be input only.

.. rubric:: When to use

Element numbers and ordinal numbers each can have their use within an
DLL function. Element numbers remain identical throughout a modeling
session using a single data set, regardless of addition and deletion of
set elements, or any change in set ordering. For this reason, it is best
to use element numbers when the set elements need to be used in multiple
calls of the DLL function. Ordinal numbers, on the other hand, are the
most convenient means for passing permutations that are used within the
current external call only. With it, you can directly access a permuted
reference in other array arguments.

.. rubric:: Passing set arguments

Sets can be passed as ``array`` arguments to an external DLL function.
When passing set arguments, you have to make a distinction between
one-dimensional root sets, one-dimensional subsets (both either simple
or relation), and multidimensional subsets and indexed sets. The
following rules apply.

.. rubric:: Pass as onedimensional array

One-dimensional root sets and subsets can be passed as a one-dimensional
array of length equal to the cardinality of the set. To accomplish this,
you can must pass such a set as

-  an array of ``integer`` numbers, representing either the ordinal or
   element numbers of each element in the set (using the
   ``ordinalnumber`` or ``elementnumber`` modifier), or

-  a ``string`` array, representing the names of all elements in the
   set.

One-dimensional set arguments passed in this manner can only be input
arguments. As a specific consequence, you cannot modify the contents of
root sets passed as array arguments.

.. rubric:: Pass as indicator parameter

You can pass any subset (whether it is simple, relation or indexed) as a
multidimensional ``integer indicator`` array defined over its respective
domain sets, indicating whether a particular tuple of domain set
elements is contained in the subset (value equals 1) or not (value
equals 0). The dimension of such indicator parameters is given by the
following set of rules:

-  the dimension for a *simple subset* is 1,

-  the dimension for a multidimensional relation is the dimension of the
   Cartesian product of which the set is a subset,

-  the dimension of an *indexed set* is the dimension of the index
   domain of the set plus 1.

Set arguments passed as an ``indicator`` argument can be of input,
output, or inout type. In the latter two cases modifications to the 0-1
values of the indicator parameter are translated back into the
corresponding element memberships of the subset.

.. rubric:: Set argument defaults

When you pass set arguments to an external DLL, AIMMS will assume no
default translation methods when the set is passed as an ``integer``
array, as each type of set does not allow every translation method. For
integer set arguments you should therefore always specify one of the
translation modifiers ``ordinalnumber``, ``elementnumber`` or
``indicator``.

.. rubric:: Passing set handles

Sets can also be passed by an integer handle. AIMMS offers various API
functions (see also :ref:`sec:api.attribute`) to obtain information
about the domain of the set, its cardinality and elements, and to add or
remove elements to the set.