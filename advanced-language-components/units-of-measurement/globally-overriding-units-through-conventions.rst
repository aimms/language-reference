.. _sec:units.convention:

Globally Overriding Units Through ``Conventions``
=================================================

.. rubric:: Unit conventions

In addition to locally overriding the unit definition of an identifier
in a particular statement, you can also *globally* override the default
format for data exchange using ``READ`` and ``WRITE``, ``DISPLAY`` and
``SOLVE`` statements by selecting an appropriate *unit convention*. A
convention offers a global medium to specify alternative (scaled) units
for multiple quantities, units, and identifiers. In addition, one can
specify alternative representations for a calendar in a convention.

.. rubric:: Effect of conventions

Once you have selected a convention, AIMMS will interpret all data
transfer with an external component according to the units that are
specified in the convention. When no convention has been selected for a
particular external component, AIMMS will use the default convention,
i.e. apply the unit as specified in the declaration of an identifier.
For a compound quantity not present in a convention, AIMMS will apply
the convention to all composing atomic units used in the compound
quantity.

.. _convention:

.. rubric:: Convention attributes

Conventions must be declared before their use. The list of attributes of
a ``Convention`` declaration are described in
:ref:`this table <table:units.attr-convention>`.

.. _table:units.attr-convention:

.. table:: 

	================== ============================= ==================
	Attribute          Value-type                    See also page
	================== ============================= ==================
	``Text``           *string*                         
	``Comment``        *comment string*                 
	``PerIdentifier``  *convention-list*/*reference*    
	``PerQuantity``    *convention-list*                
	``PerUnit``        *convention-list*                
	``TimeslotFormat`` *timeslot-format-list*        :ref:`sec:time.tz`
	================== ============================= ==================
	
.. _convention.per_identifier:

.. _convention.per_quantity:

.. _convention.per_unit:

.. _convention.timeslot_format:

.. rubric:: Convention list

A convention list is a simple list associating single quantities, units
and identifiers with a particular (scaled) unit expression. The
specified unit expressions must be consistent with the base unit of the
quantity, the specified unit, or the identifier unit, respectively.

.. _convention-list:

.. rubric:: Syntax

*convention-list:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 355.61067 137.2"
	   height="137.2"
	   width="355.61066"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,483.59999)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,3000 -20,-50 h 40" /><path
	         id="path16"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 400,2700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,45,266)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 953.48,2700 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1153.48,3000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 320.02,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g30"><text
	           id="text34"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,37.002,296)"><tspan
	             id="tspan32"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/the-quantity-declaration.html#unit-symbol">unit-symbol</a></tspan></text>
	</g><path
	         id="path36"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1033.46,3000 50,-20 v 40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 200,3000 20,50 h -40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 416.621,3300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g42"><text
	           id="text46"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,46.6621,326)"><tspan
	             id="tspan44"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/the-quantity-declaration.html#quantity">quantity</a></tspan></text>
	</g><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 936.859,3300 50,-20 v 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1153.48,3000 20,50 h -40" /><path
	         id="path52"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1253.48,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g54"><text
	           id="text58"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,131.748,296)"><tspan
	             id="tspan56"
	             y="0"
	             x="0">:</tspan></text>
	</g><path
	         id="path60"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1453.48,3000 50,-20 v 40" /><path
	         id="path62"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1553.48,3000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g64"><text
	           id="text68"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,160.348,296)"><tspan
	             id="tspan66"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/advanced-language-components/units-of-measurement/unit-expressions.html#unit-expression">unit-expression</a></tspan></text>
	</g><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2467.08,3000 50,-20 v 40" /><path
	         id="path72"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 100,3000 20,50 H 80" /><path
	         id="path74"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1233.54,3525 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g76"><text
	           id="text80"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,129.754,348.5)"><tspan
	             id="tspan78"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1433.54,3525 50,-20 v 40" /><path
	         id="path84"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2567.08,3000 20,50 h -40" /><path
	         id="path86"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2667.08,3000 -50,20 v -40" /><path
	         id="path88"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,3000 h 100 m 0,0 v 0 h 100 m 0,0 v -200 c 0,-55.23 44.773,-100 100,-100 v 0 h 100 v 100 H 953.461 V 2700 2600 H 400 v 100 m 553.48,0 h 100 v 0 c 55.23,0 100,44.77 100,100 v 200 M 200,3000 h 100 -79.98 100 v 100 h 713.42 V 3000 2900 H 320.02 v 100 m 713.44,0 h 100 20.02 M 200,3000 v 200 c 0,55.23 44.773,100 100,100 h 16.621 100 v 100 H 936.852 V 3300 3200 H 416.621 v 100 m 520.238,0 h 100.001 16.62 c 55.23,0 100,-44.77 100,-100 v -200 h 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 v 100 h 913.58 v -100 -100 h -913.58 v 100 m 913.6,0 h 100 M 100,3000 v 425 c 0,55.23 44.773,100 100,100 h 933.54 100 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 100 933.54 c 55.22,0 100,-44.77 100,-100 v -425 h 100" /></g></g></svg></div>

.. rubric:: Customizable conventions

In addition to a fixed convention list, the ``PerIdentifier`` attribute
also accepts a reference to a unit-valued parameter defined over the set
:any:`AllIdentifiers` or a subset thereof. In that case, the convention
will dynamically construct a convention list based on the contents of
the unit-valued parameter.

.. rubric:: Example

The following declaration illustrates the use of a ``Convention`` to
define the more common units in the Anglo-American unit system at the
quantity level, the unit level and the identifier level.

.. code-block:: aimms

	Convention AngloAmericanUnits {
	    PerIdentifier  : {
	        GasolinePurchase : gallon,
	        PersonalHeight   : feet
	    }
	    PerQuantity    : {
	        Velocity         : mph,
	        Temperature      : degF,
	        Length           : mile
	    }
	    PerUnit        : {
	        cm               : inch,
	        m                : yard,
	        km               : mile
	    }
	}

.. rubric:: Customizable example

Assuming that ``IdentifierUnits`` is a unit-valued parameter defined
over :any:`AllIdentifiers`, the following ``Convention`` declaration
illustrates a convention that can be customized at runtime by modifying
the contents of the unit parameter ``IdentifierUnits``.

.. code-block:: aimms

	Convention CustomizableConvention {
	    PerIdentifier  : IdentifierUnits;
	}

.. rubric:: Application order

For a particular identifier, AIMMS will select a unit from a convention
in the following order.

-  If a unit has been specified for the identifier, AIMMS will use it.

-  If the identifier can be associated with a specific quantity in the
   convention, AIMMS will use the unit specified for that quantity.

-  In all other cases AIMMS will apply the convention to an atomic unit
   directly, or to all composing atomic units used in a compound unit.

.. rubric:: Timeslot format list

In addition to globally overriding units, ``Conventions`` can also be
used, through the ``TimeslotFormat`` attribute, to override the time
slot format of calendars. You may need to specify alternative time slot
formats, for instance, when you are reading data from an external
database or file, in which all dates are not specified in the same time
zone as the one your model assumes. The ``TimeslotFormat`` attribute of
a ``Convention`` is discussed in full detail in :ref:`sec:time.tz`.

.. _database_table.convention:

.. _database_procedure.convention:

.. rubric:: The ``Convention`` attribute

You can declare more than one convention in your model. A ``Convention``
attribute can be specified for the following node types in the model
tree, which all correspond to an external component:

-  the main model (used for the end-user interface or as default for all
   other external components),

-  a mathematical program,

-  a file (also when used to refer to a DLL containing a library of
   external procedures and functions used by AIMMS), and

-  a database table or procedure.

The value of the ``Convention`` attribute can be a specific convention
declared in your model, or a string or element parameter referring to a
particular unit convention.

.. rubric:: Convention semantics

For data exchange with all aforementioned external components AIMMS will
select a unit convention in the following order.

-  If an external component has a nonempty ``Convention`` attribute,
   AIMMS will use that convention.

-  For display in the user interface, or for data exchange with external
   components without a ``Convention`` attribute, AIMMS will use the
   convention specified for the main model (see also
   :ref:`sec:module.model`), if present.

-  If the main model and external components have no ``Convention``
   attribute, AIMMS will use the default convention, i.e. use the unit
   as specified in the declaration of each identifier.

.. rubric:: Example

The following declaration of a ``File`` identifier shows the use of the
``Convention`` attribute. All the output to the file ``ResultFile`` will
be displayed in Anglo-American units.

.. code-block:: aimms

	File ResultFile {
	    Name       : "Output\\result.dat";
	    Convention : AngloAmericanUnits;
	}