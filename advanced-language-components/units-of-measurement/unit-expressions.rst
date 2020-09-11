.. _sec:units.expr:

Unit Expressions
================

.. rubric:: Unit expressions

Unit expressions can be used at various places in an AIMMS model, such
as:

-  the ``BaseUnit`` attribute of a ``Quantity`` declaration (defined in
   :ref:`sec:units.quantity`),

-  in a local unit override of a numerical (sub-)expression (discussed
   in :ref:`sec:units.local-override`)

-  in a convention list of the ``PerUnit``, ``PerQuantity`` or
   ``PerIdentifier`` attributes of a ``Convention`` (see also
   :ref:`sec:units.convention`), or

-  on the right hand side of an assignment to a unit parameter (see
   :ref:`sec:units.unit-par`).

The syntax of a unit expression is straightforward, and given below.

.. _unit-expression:

.. rubric:: Syntax

*unit-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 297.81333 227.2"
	   height="227.2"
	   width="297.81332"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,1480.2666)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 340,9500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,40.4,946)"><tspan
	             id="tspan20"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 540,9500 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 660,9500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,71,946)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/unit-expressions.html#unit-expression">unit-expression</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1573.6,9500 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1693.6,9500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g38"><text
	           id="text42"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,175.76,946)"><tspan
	             id="tspan40"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path44"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1893.6,9500 50,-20 v 40" /><path
	         id="path46"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2113.6,11000 -20,-50 h 40" /><path
	         id="path48"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 760.082,11000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g50"><text
	           id="text54"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,81.0078,1096)"><tspan
	             id="tspan52"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/the-quantity-declaration.html#unit-symbol">unit-symbol</a></tspan></text>
	</g><path
	         id="path56"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1473.52,11000 50,-20 v 40" /><path
	         id="path58"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path60"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 696.66,10700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g62"><text
	           id="text66"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,74.666,1066)"><tspan
	             id="tspan64"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/unit-expressions.html#unit-reference">unit-reference</a></tspan></text>
	</g><path
	         id="path68"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1536.94,10700 50,-20 v 40" /><path
	         id="path70"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2113.6,11000 -20,-50 h 40" /><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 533.281,10400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g76"><text
	           id="text80"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,58.3281,1036)"><tspan
	             id="tspan78"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#operator-expression">operator-expression</a></tspan></text>
	</g><path
	         id="path82"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.32,10400 50,-20 v 40" /><path
	         id="path84"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2113.6,11000 -20,-50 h 40" /><path
	         id="path86"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path88"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 746.703,10100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g90"><text
	           id="text94"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,79.6699,1006)"><tspan
	             id="tspan92"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#function-call">function-call</a></tspan></text>
	</g><path
	         id="path96"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1486.9,10100 50,-20 v 40" /><path
	         id="path98"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2113.6,11000 -20,-50 h 40" /><path
	         id="path100"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path102"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 469.918,9800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g104"><text
	           id="text108"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,51.9918,976)"><tspan
	             id="tspan106"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#conditional-expression">conditional-expression</a></tspan></text>
	</g><path
	         id="path110"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1763.68,9800 50,-20 v 40" /><path
	         id="path112"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2113.6,11000 -20,-50 h 40" /><path
	         id="path114"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2233.6,11000 -50,20 v -40" /><path
	         id="path116"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,11000 h 120 m 0,0 V 9600 c 0,-55.23 44.773,-100 100,-100 v 0 h 120 v 0 c 0,55.23 44.773,100 100,100 v 0 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 v 0 c -55.227,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 913.58 V 9500 9400 H 660 v 100 m 913.6,0 h 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 0 c 55.23,0 100,44.77 100,100 v 1400 m -1993.6,0 h 100 420.078 120 v 100 H 1473.5 v -100 -100 H 760.078 v 100 m 713.442,0 h 120 520.08 m -1993.6,0 v -200 c 0,-55.2 44.773,-100 100,-100 h 356.66 120 v 100 h 840.26 v -100 -100 H 696.66 v 100 m 840.28,0 h 120 356.66 c 55.23,0 100,44.8 100,100 v 200 m -1993.6,0 v -500 c 0,-55.2 44.773,-100 100,-100 h 193.281 120 v 100 H 1700.29 v -100 -100 H 533.281 v 100 m 1167.039,0 h 120 193.28 c 55.23,0 100,44.8 100,100 v 500 m -1993.6,0 v -800 c 0,-55.2 44.773,-100 100,-100 h 406.699 120 v 100 h 740.181 v -100 -100 H 746.699 v 100 m 740.201,0 h 120 406.7 c 55.23,0 100,44.8 100,100 v 800 M 120,11000 V 9900 c 0,-55.23 44.773,-100 100,-100 h 129.918 120 v 100 H 1763.64 V 9800 9700 H 469.918 v 100 m 1293.762,0 h 120 129.92 c 55.22,0 100,44.77 100,100 v 1100 h 120" /></g></g></svg></div>

.. _unit-reference:

.. rubric:: Unit symbols and references

The simplest form of unit expression is just a unit symbol, as defined
in either the ``BaseUnit`` or the ``Conversion`` attribute of a
``Quantity`` declaration. A reference to either a (scalar or indexed)
unit parameter (see :ref:`sec:units.unit-par`) or to the ``.Unit``
suffix of any identifier with an associated unit (see
:ref:`sec:units.ident`), is a second form of unit expression.

.. rubric:: Unit operators and functions

More complex unit expressions can be obtained by applying the binary
unit operators ``*``, ``/`` and ``^``, with the usual left-to-right
evaluation order. The following rules apply:

-  the operand on the right of the ``*`` operator must be a unit
   expression, while the operand on the left can either be a unit
   expression or a numerical expression (expressing a numeric scale
   factor),

-  both operands of the ``/`` operator must be unit expressions, and

-  the operand on the left of the ``^`` operator must be a unit
   expression, while the exponent operand must be an integer numerical
   expression.

In addition, AIMMS supports a number of unit functions, which can create
new unit values or construct associated unit values from a given unit
expression (see :ref:`sec:units.expr.func`).

.. rubric:: Three types of unit expressions

However, AIMMS requires that any unit expressions uniquely falls into
one of the three categories

-  unit constant,

-  simple unit expression, or

-  computed unit expression.

.. rubric:: Unit constants

*Unit constants* are unit expressions which consist solely of unit
symbols, scalar constants and the three unit operators ``*``, ``/`` and
``^``. Unit constants can be used in

-  the ``BaseUnit`` attribute of a ``Quantity``,

-  the lists associated with a ``Convention``, and

-  the unit-valued function :any:`Unit`.

In addition, unit constants can be

-  displayed and entered via the AIMMS graphical user interface,

-  assigned to unit parameters through data statements (see
   :ref:`chap:text.data.file`), and

-  exchanged with external data sources via the ``READ`` and ``WRITE``
   statements (see :ref:`chap:rw`).

.. rubric:: Simple unit expressions

*Simple unit expressions* are an extension of unit constants. They are
unit expressions which consist solely of unit symbols, unit references
without indexing, scalar constants and the three unit operators ``*``,
``/`` and ``^``. Simple unit expressions can be used in

-  local unit overrides, and

-  assignments to unit parameters.

.. rubric:: Computed unit expressions

Computed unit expression can use the full range of unit expressions,
with the exception of unit constants. If you want to refer to unit
constants within the context of a computed unit expression, you must
embed it within a call to the function :any:`Unit`, discussed in the next
section. Computed unit expressions can be used

-  in assignments to unit parameters, and

-  as an argument of the functions :any:`ConvertUnit`, :any:`AtomicUnit` and
   :any:`EvaluateUnit` (see :ref:`sec:units.expr.func` and
   :ref:`sec:units.expr.eval`).

.. _sec:units.expr.func:

Unit-valued Functions
---------------------

.. rubric:: Unit-valued functions

AIMMS supports the following unit-valued functions:

-  :any:`Unit`\ (*unit-constant*)

-  :any:`StringToUnit`\ (*unit-string*)

-  :any:`AtomicUnit`\ (*unit-expr*)

-  :any:`ConvertUnit`\ (*unit-expr*, *convention*)

.. rubric:: The function :any:`Unit`

The function :any:`Unit` simply returns its argument, which must be a unit
constant. The function :any:`Unit` is available to allow the usage of unit
constants within computed unit expressions (as discussed in the previous
section).

.. rubric:: The function :any:`StringToUnit`

The function :any:`StringToUnit` converts a string, which represents a unit
expression, to the corresponding unit value. You can use this function,
for instance, after reading external string data that needs to be
converted to real unit values for further use in your model.

.. rubric:: The function :any:`AtomicUnit`

With the function :any:`AtomicUnit` you can retrieve the atomic unit
expression corresponding to the unit expression passed as the argument
to the function. Thus, the unit expression

.. code-block:: aimms

	AnIdentifier.Unit / AtomicUnit(AnIdentifier.Unit)

will result in a (unitless) unit value that exactly represents the scale
factor between the unit of an identifier and its associated atomic unit
expression. You can obtain the corresponding numerical value, to be used
in numerical expressions, by applying the function :any:`EvaluateUnit`
discussed in the next section.

.. rubric:: The function :any:`ConvertUnit`

The function :any:`ConvertUnit` returns the unit value corresponding to the
unit expression of the first argument, but taking into consideration the
convention specified in the second argument. If the first argument
contains a reference to a ``.Unit`` suffix, AIMMS will apply the full
range of conversions including those specified in the ``PerIdentifier``
attribute of the convention.

.. rubric:: Examples

The expression

.. code-block:: aimms

	ConvertUnit(AnIdentifier.Unit, ConventionUsed)

returns the associated unit of the identifier ``AnIdentifier`` as if the
convention ``ConventionUsed`` were active. A further example of the use
of the function :any:`ConvertUnit` is given in :ref:`sec:units.scaling.mp`.

.. _sec:units.expr.eval:

Converting Unit Expressions to Numerical Expressions
----------------------------------------------------

.. rubric:: Numeric value of a unit expression

Although numerical values and unit values are two very distinct data
types in AIMMS, the distinction between the two in real life
applications is not always as strict. For instance, in the previous
section the computation of the ratio between a unit and its associated
atomic unit expression returned a unit value, which represents nothing
more than a (unitless) scale factor. In practice, however, it is the
numeric scale factor value that is of interest, and can be used in
numerical computations.

.. rubric:: The function :any:`EvaluateUnit`

Using the function :any:`EvaluateUnit` you can compute the numerical value
associated with a computed unit expression. Its syntax is:

-  :any:`EvaluateUnit`\ (*computed-unit-expression*)

The numeric function value precisely corresponds to one unit of the
specified computed unit expression, measured in the evaluated unit of
its argument.

.. rubric:: Example

The following assignment to the scalar parameter ``ScaleFactor``
computes the (unitless) scale factor between the unit of an identifier
and its associated atomic unit expression.

.. code-block:: aimms

	ScaleFactor := EvaluateUnit( AnIdentifier.Unit / AtomicUnit(AnIdentifier.Unit) );

.. rubric:: Extension of local overrides

As you will see in the next section, the function :any:`EvaluateUnit`
offers extension the local unit override capability. The argument of
:any:`EvaluateUnit` can be a computed unit expression (see
:ref:`sec:units.expr`), whereas local unit overrides can only accept
simple unit expressions.