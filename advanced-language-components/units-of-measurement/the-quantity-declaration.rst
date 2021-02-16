.. _sec:units.quantity:

The ``Quantity`` Declaration
============================

.. _quantity:

.. rubric:: Declaration

In AIMMS, all units are uniquely coupled to declared quantities. For
each declared ``Quantity`` you must specify an identifier together with
one or more of its attributes listed in
:ref:`this table <table:units.attr-quantity>`.

.. _table:units.attr-quantity:

.. table:: Quantity attributes

   ============== ====================== =========
   Attribute      Value-type             Mandatory
   ============== ====================== =========
   ``BaseUnit``   [*unit-symbol*] [=]    yes
                  [*unit-expression*]       
   ``Text``       *string*                  
   ``Conversion`` *unit-conversion-list*    
   ``Comment``    *comment string*          
   ============== ====================== =========

.. _quantity.base_unit:

.. _unit-symbol:

.. rubric:: The ``BaseUnit`` attribute

You must always specify a base unit for each quantity that you declare.
Its value is either

-  an *atomic* unit symbol,

-  a *unit expression*, or

-  a *compound* unit symbol with unit expression.

A unit symbol can be any sequence of the characters ``a``-``z``, the
digits ``0``-``9``, and the symbols ``_``, ``@``, ``&``, ``%``, ``|``,
as well as a currency symbol not starting with a digit, or one of the
special unit symbols ``1`` and ``-``. The latter two special unit
symbols allow you, for instance, to declare model identifiers without
unit, or to express unitless numerical data in terms of percentages.

.. rubric:: Currency symbols

AIMMS supports the currency symbols as defined by the Unicode committee,
see http://unicode.org/charts/PDF/U20A0.pdf.

.. rubric:: Separate namespace

AIMMS stores unit symbols in namespaces separate but parallel to the
identifier namespaces. Hence, you are free to choose unit symbols equal
to the names of global identifiers within your model. Namespaces in
AIMMS are discussed in full detail in :ref:`sec:module.module`.

.. rubric:: Backward compatibility

AIMMS 3.8 and older use only a singleton unit namespace which was a
potential cause of nameclashes when units with the same name are
declared from quantities or unit parameters declared in different
namespaces. In order to obtain the old behaviour one can make sure that
all units are declared within the global namespace or set the option
``singleton_unit_namespace`` to ``on``. This option can be found in the
backward compatibility category.

.. rubric:: Example

The following example illustrates the three types of base units.

.. code-block:: aimms

	Quantity Length {
	    BaseUnit   : {
	        m                     ! atomic unit
	    }
	}

.. code-block:: aimms

	Quantity Time {
	    BaseUnit   : {
	        s                     ! atomic unit
	    }
	}
	Quantity Velocity {
	    BaseUnit   : {
	        m/s                   ! unit expression
	    }
	}
	Quantity Frequency {
	    BaseUnit   : {
	        Hz = 1/s              ! compound unit symbol with unit expression
	    }
	}

The atomic unit symbols ``m`` and ``s`` are the base units for the
quantities ``Length`` and ``Time``. The unit expression ``m/s`` is the
base unit for the quantity ``Velocity``. The compound unit symbol
``Hz``, defined by the unit expression ``1/s``, is the base unit of the
quantity ``Frequency``.

.. rubric:: Derived can be used as basic

The previous example strictly adheres to the SI standards, and, for
example, defines the base unit of the derived quantity ``Frequency`` in
terms of the base unit of ``Time``. In general, this is not necessary.
If ``Time`` is not used anywhere else in your model, you can just
provide the base unit ``Hz`` for ``Frequency`` without providing its
translation in SI base units. ``Frequency`` then becomes a basic
quantity, and ``Hz`` becomes an atomic base unit.

.. rubric:: Unit expressions

The unit expressions that you can enter in the ``BaseUnit`` attribute
can only consist of

-  unit symbols (base and/or related units),

-  constant factors,

-  the two operators ``*`` and ``/``,

-  parentheses, and

-  the power operator ``^`` with integer exponent.

The common precedence order of the operators ``*``, ``/`` and
``^`` is as described in :ref:`sec:expr.oper-prec`. Unit expressions
are discussed in full detail in :ref:`sec:units.expr`.

.. _quantity.conversion:

.. rubric:: The ``Conversion`` attribute

With the ``Conversion`` attribute you can declare and define one or more
related unit symbols by specifying the (linear) transformation to the
associated base unit.

The conversion syntax is as follows.

.. _unit-conversion-list:

.. rubric:: Syntax

*unit-conversion-list:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 563.79732 67.199997"
	   height="67.199997"
	   width="563.7973"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,186.93333)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,25,96)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/the-quantity-declaration.html#unit-symbol">unit-symbol</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 913.441,1000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1013.44,1000 -49.999,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,106.344,96)"><tspan
	             id="tspan28"
	             y="0"
	             x="0">-&gt;</tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1257.44,1000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1357.44,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,140.744,96)"><tspan
	             id="tspan38"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/the-quantity-declaration.html#unit-symbol">unit-symbol</a></tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2070.88,1000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2170.88,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,223.488,96)"><tspan
	             id="tspan48"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2370.88,1000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2470.88,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,253.488,96)"><tspan
	             id="tspan58"
	             y="0"
	             x="0">#</tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2670.88,1000 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2770.88,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g66"><text
	           id="text70"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,282.088,96)"><tspan
	             id="tspan68"
	             y="0"
	             x="0">-&gt;</tspan></text>
	</g><path
	         id="path72"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3014.88,1000 50,-20 v 40" /><path
	         id="path74"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3114.88,1000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g76"><text
	           id="text80"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,316.488,96)"><tspan
	             id="tspan78"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/the-quantity-declaration.html#unit-conversion">unit-conversion</a></tspan></text>
	</g><path
	         id="path82"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4028.48,1000 50,-20 v 40" /><path
	         id="path84"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,1000 20,50 H 80" /><path
	         id="path86"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2014.24,1300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g88"><text
	           id="text92"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,207.824,126)"><tspan
	             id="tspan90"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path94"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2214.24,1300 50,-20 v 40" /><path
	         id="path96"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4128.48,1000 20,50 h -40" /><path
	         id="path98"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 4228.48,1000 -50,20 v -40" /><path
	         id="path100"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,1000 h 100 m 0,0 v 0 h 100 v 100 H 913.422 V 1000 900 H 200 v 100 m 713.441,0 h 99.999 v 0 c 0,55.23 44.77,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 h -44 c -55.23,0 -100,44.773 -100,100 v 0 m 244,0 h 100 v 100 h 713.42 V 1000 900 h -713.42 v 100 m 713.44,0 h 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.773 -100,100 v 0 m 200,0 h 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.773 -100,100 v 0 m 200,0 h 100 v 0 c 0,55.23 44.78,100 100,100 h 44 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.227 -44.77,-100 -100,-100 h -44 c -55.22,0 -100,44.773 -100,100 v 0 m 244,0 h 100 v 100 h 913.58 V 1000 900 h -913.58 v 100 m 913.6,0 h 100 M 100,1000 v 200 c 0,55.23 44.773,100 100,100 h 1714.24 100 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 100 1714.24 c 55.23,0 100,-44.77 100,-100 v -200 h 100" /></g></g></svg></div>

.. _unit-conversion:

.. rubric:: Unit conversion explained

A unit conversion must be defined using a linear expression of the form
:math:`(\hbox{\texttt{\#}}\cdot a+b)` where ``#`` is a special token,
and the operator :math:`\cdot` stands for either multiplication or
division. The coefficients :math:`a` and :math:`b` can be either
numerical constants or references to scalar parameters. An example in
which the use of scalar parameters is particularly convenient is the
conversion between currencies parameterized by a varying exchange rate.

.. rubric:: Example

.. code-block:: aimms

	Quantity Length {
	    BaseUnit    : m;
	    Conversions : {
	        km   -> m    :  # -> # * 1000,
	        mile -> m    :  # -> # * 1609
	    }
	}
	Quantity Temperature {
	    BaseUnit    : degC;
	    Conversions : degC -> degF :  # -> # * 1.8 + 32;
	}
	Quantity Energy {
	    BaseUnit    : J = kg * m^2 / s^2;
	    Conversions : {
	        kJ  -> J     :  # -> # * 1000 ,
	        MJ  -> J     :  # -> # * 1.0e6,
	        kWh -> J     :  # -> # * 3.6e6
	    }
	}
	Quantity Currency {
	    BaseUnit    : US$;
	    Conversion  : {
	        DM  -> US$   : # -> # * ExchangeRate('DM') ,
	        DFl -> US$   : # -> # * ExchangeRate('DFl')
	    }
	}
	Quantity Unitless {
	    BaseUnit    : 1;
	    Conversions : % -> 1      : # -> # / 100;
	}