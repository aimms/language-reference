.. _sec:data.assert:

Assertions
==========

.. rubric:: Data validity is important

In almost all modeling applications it is important to check the
validity of input data prior to its use. For instance, in a
transportation model it makes no sense if the total demand exceeds the
total supply. In general, data consistency checks guard against
unexplainable or even infeasible model results. As a result, these
checks are essential to obtain customer acceptance of your application.
In rigorous model-based applications it is not uncommon that the error
consistency checks form a significant part of the total model text.

.. _assertion:

.. rubric:: ``Assertion`` declaration and attributes

To provide you with a mechanism to implement data validity checks, AIMMS
offers a special ``Assertion`` data type. With it, you can easily
specify and verify logical conditions for all elements in a particular
domain, and take appropriate action when you find an inconsistency.
Assertions can be verified from within the model through the ``ASSERT``
statement, or automatically upon data changes by the user from within
the graphical user interface. The attributes of the ``Assertion`` type
are given in :ref:`this table <table:data.attr-assertion>`.

.. _table:data.attr-assertion:

.. table:: 

	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| Attribute       | Value-type           | See also page                                                                                                                                   |
	+=================+======================+=================================================================================================================================================+
	| ``IndexDomain`` | *index-domain*       | :ref:`The IndexDomain attribute for Parameters <attr:par.index-domain>`, :ref:`The IndexDomain attribute for Variables <attr:var.index-domain>` |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Text``        | *string*             | :ref:`The Text and Comment attributes <attr:prelim.text>`, :ref:`The Text attribute for Parameters <attr:par.text>`                             |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Property``    | ``WarnOnly``         |                                                                                                                                                 |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``AssertLimit`` | *integer*            |                                                                                                                                                 |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Definition``  | *logical-expression* | :ref:`The Definition attribute <attr:set.definition>`, :ref:`The Definition attribute for Parameters <attr:par.definition>`                     |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Action``      | *statements*         |                                                                                                                                                 |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	| ``Comment``     | *comment string*     | :ref:`The Text and Comment attributes <attr:prelim.comment>`                                                                                    |
	+-----------------+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
	
.. _assertion.definition:

.. rubric:: The ``Definition`` attribute

The ``Definition`` attribute of an ``Assertion`` contains the logical
expression that must be satisfied by every element in the index domain.
If the logical expression is not true for a particular element in the
index domain, the specified action will be undertaken. Examples follow.

.. rubric:: Examples

.. code-block:: aimms

	Assertion SupplyExceedsDemand {
	    Text         :  Error: Total demand exceeds total supply;
	    Definition   : { 
	        Sum( i in Cities, Supply(i) ) >=
	        Sum( i in Cities, Demand(i) )
	    }
	}
	Assertion CheckTransportData {
	    IndexDomain  :  (i,j) | Distance(i,j);
	    Text         :  Please supply proper transport data for transport (i,j);
	    AssertLimit  :  3;
	    Definition   : { 
	        UnitTransportCost(i,j) and
	        MinShipment(i,j) <= MaxShipment(i,j)
	    }
	}

The assertion ``SupplyExceedsDemand`` is a global check. The assertion
``CheckTransportData(i,j)`` is verified for every pair of cities ``i``
and ``j`` for which ``Distance(i,j)`` assumes a nonzero value. AIMMS
will terminate further verification when the assertion fails for the
third time.

.. _assertion.text:

.. rubric:: The ``Text`` attribute

The ``Text`` attribute of an ``Assertion`` is the text that is used as
warning or error message when the assertion fails for an element in its
domain. If the text contains indices from the assertions index domain,
these are expanded to identify the elements for which the assertion
failed. If you have overridden the default response by means of the
``Action`` attribute (see below), then the text attribute is ignored.

.. _assertion.property:

.. rubric:: The ``Property`` attribute

The ``Property`` attribute of an assertion can only assume the value
``WarnOnly``. With it you indicate that a failed assertion should only
result in a warning being triggered, instead of an error. This attribute
is also ignored if the ``Action`` is overridden.

.. _assertion.assert_limit:

.. rubric:: The ``AssertLimit`` attribute

By default, AIMMS will verify an assertion for every element in its
index domain, and call the (default) action for every element for which
the assertion fails. With the ``AssertLimit`` attribute you can limit
the number of verifications that are made. When the number of failed
assertions reaches the ``AssertLimit``, AIMMS will stop the verification
of any further elemens in the index domain. By default, the
``AssertLimit`` is set to 1.

.. _assertion.action:

.. rubric:: The ``Action`` attribute

The default response to a failing assertion is that either an error or a
warning is raised, based on the ``Property`` setting. You can use the
``Action`` attribute if you want to specify a nondefault response to a
failed assertion. Like the body of a procedure, the ``Action`` attribute
can contain multiple statements which together implement the appropriate
response. During the execution of the statements in the ``Action``
attribute, the indices occurring in the index domain of the assertion
are bound to the currently offending element. This allows you to control
the interaction with the end-user. For instance, you can request that
all detected errors in the index domain are changed appropriately, or
perhaps implement an auto-correct on invalid values.

.. _failcount:

.. rubric:: The ``FailCount`` operator

If you raise an error or call the ``HALT`` statement during the
execution of an ``Action`` attribute, the current model execution will
terminate. When you use it in conjunction with the predefined
``FailCount`` operator, you can implement a more sophisticated version
of the ``AssertLimit``. The ``FailCount`` operator evaluates to the
number of failures encountered during the current execution of the
assertion. It cannot be referenced outside the context of an assertion.

.. rubric:: Verifying assertions

Assertions can be verified in two ways:

-  by explicitly calling the ``ASSERT`` statement during the execution
   of your model, or

-  automatically, from within the graphical user interface, when the
   end-user of your application changes input values in particular
   graphical objects.

.. _assert:

.. rubric:: The ``ASSERT`` statement

With the ``ASSERT`` statement you verify assertions at specific places
during the execution of your model. Thus, you can use it, for instance,
during the execution of the ``MainInitialization`` procedure, to verify
the consistency of data that you have read from a database. Or, just
prior to solving a mathematical program, to verify that all currently
accrued data modifications do not result in data inconsistencies. The
syntax of the ``ASSERT`` statement is simple.

.. _assert-statement:

.. rubric:: Syntax

*assert-statement:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 523.44002 93.866661"
	   height="93.866661"
	   width="523.44"
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
	         d="m 120,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,17,196)"><tspan
	             id="tspan18"
	             y="0"
	             x="0">ASSERT</tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 652,2000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 892,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g26"><text
	           id="text30"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,94.2,196)"><tspan
	             id="tspan28"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/identifier-declarations.html#identifier">identifier</a></tspan></text>
	</g><path
	         id="path32"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1445.48,2000 50,-20 v 40" /><path
	         id="path34"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1685.48,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g36"><text
	           id="text40"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,174.948,196)"><tspan
	             id="tspan38"
	             y="0"
	             x="0">(</tspan></text>
	</g><path
	         id="path42"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1885.48,2000 50,-20 v 40" /><path
	         id="path44"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2005.48,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g46"><text
	           id="text50"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,205.548,196)"><tspan
	             id="tspan48"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#binding-domain">binding-domain</a></tspan></text>
	</g><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2925.8,2000 50,-20 v 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3045.8,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,310.98,196)"><tspan
	             id="tspan58"
	             y="0"
	             x="0">)</tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3245.8,2000 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1565.48,2000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3365.8,2000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 772,2000 20,50 h -40" /><path
	         id="path70"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2028.9,2300 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g72"><text
	           id="text76"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,209.29,226)"><tspan
	             id="tspan74"
	             y="0"
	             x="0">,</tspan></text>
	</g><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 2228.9,2300 50,-20 v 40" /><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3485.8,2000 20,50 h -40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3605.8,2000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-variant:normal;font-size:12px;font-family:'Courier New';-inkscape-font-specification:LucidaSans-Typewriter;writing-mode:lr-tb;fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,366.98,196)"><tspan
	             id="tspan86"
	             y="0"
	             x="0">;</tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3805.8,2000 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 3925.8,2000 -50,20 v -40" /><path
	         id="path94"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,2000 h 120 v 0 c 0,55.23 44.773,100 100,100 h 332 c 55.227,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.773,-100 -100,-100 H 220 c -55.227,0 -100,44.77 -100,100 v 0 m 532,0 h 120 m 0,0 v 0 h 120 v 100 h 553.46 V 2000 1900 H 892 v 100 m 553.48,0 h 120 m 0,0 v 0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 v 100 h 920.29 v -100 -100 h -920.29 v 100 m 920.32,0 h 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.23,0 -100,44.77 -100,100 v 0 m 200,0 h 120 m -1800.32,0 v -200 c 0,-55.23 44.77,-100 100,-100 h 740.16 120 740.16 c 55.23,0 100,44.77 100,100 v 200 h 120 M 772,2000 v 200 c 0,55.23 44.773,100 100,100 h 1036.9 120 v 0 c 0,55.23 44.77,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120 1036.9 c 55.23,0 100,-44.77 100,-100 v -200 h 120 v 0 c 0,55.23 44.78,100 100,100 v 0 c 55.23,0 100,-44.77 100,-100 v 0 0 c 0,-55.23 -44.77,-100 -100,-100 v 0 c -55.22,0 -100,44.77 -100,100 v 0 m 200,0 h 120" /></g></g></svg></div>

.. rubric:: Example

The following statement illustrates a basic use of the ``ASSERT``
statement.

.. code-block:: aimms

	assert SupplyExceedsDemand, CheckTransportData;

It will verify the assertion ``SupplyExceedsDemand``, as well as the
*complete* assertion ``CheckTransportData``, i.e. checks are performed
for every element (``i``,\ ``j``) in its domain.

.. rubric:: Sliced verification

AIMMS allows you to explicitly supply a binding domain for an indexed
assertion. By doing so, you can limit the assertion verification to the
elements in that binding domain. This is useful when you know a priori
that the data for only a small subset of the elements in a large index
domain has changed. You can use such sliced verification, for instance,
during the execution of a procedure that is called upon a single data
change in a graphical object on a page.

.. rubric:: Example

Assume that ``CurrentCity`` takes the value of the city for which an
end-user has made a specific data change in the graphical user
interface. Then the following ``ASSERT`` statement will verify the
assertion ``CheckTransportData`` for only this specific city.

.. code-block:: aimms

	assert CheckTransportData(CurrentCity,j),
	       CheckTransportData(i,CurrentCity);