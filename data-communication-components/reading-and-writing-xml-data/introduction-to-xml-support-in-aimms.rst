.. _sec:xml.aimms:

Introduction to XML Support in AIMMS
====================================

.. rubric:: XML support in AIMMS

In order to help you understand the XML support available within AIMMS
to its full extent, this section provides an explanation of the basic
concepts used in XML. If you are already familiar with XML and XML
schemas, the material in this section may help you to understand how the
XML concepts you are already familiar with are used by the XML
facilities in AIMMS.

.. rubric:: The XML data format

The XML data format is a text format built around just two syntactical
components, *elements* and *attributes*. Because the semantics of these
components are not fixed and can be user-defined, the XML data format
can be used to represent virtually any meaningful concept.

.. rubric:: XML elements

*XML elements* are denoted by a start tag (a word identifying the type
of element enclosed by the ``<`` and ``>`` characters) and an end
tag (the same element type enclosed by the ``</`` and ``>``
characters). Elements delimit the piece of XML data between its start
and end tag. Elements may hold only text or numeric data, or they can
provide depth to XML data, since the enclosed XML data may contain other
XML elements. An element in a stream of XML data is, in fact, a node in
the tree associated with the entire stream of XML data. The root node of
this tree corresponds to the *obligatory and unique* root element of the
XML data stream.

.. rubric:: XML elements without content

If an element does not contain any enclosed XML content, it is possible
to omit the end tag alltogether, and enclose the start tag between
``<`` and ``/>`` characters. This format is commonly used if the
element contains only attributes.

.. rubric:: XML attributes

*XML attributes* provide additional information about a particular
element in an XML data stream. Attributes are specified by the form
``name="value`` between the "``<`` and ``>`` (or ``/>``)
characters of the start tag of the element in question.

.. rubric:: The Data Reconciliation example

All examples in this chapter make use of a single AIMMS project that
comes with the AIMMS system, the *Data Reconciliation* project. In this
example, flows between units in a chemical plant, as well the chemical
composition of these flows, are measured. Unfortunately, such
measurements might not be internally consistent despite, for instance, a
physical requirement that the sum of all flows into any unit be equal to
the sum of all flows out of that unit (i.e. no material is created or
lost within a unit). Due to the inaccuracy of the measurement devices
(or, even worse, broken measurement devices), the measured values do not
necessarily satisfy such balances. The objective of the model is to find
a set of flow values and compositions which *are* internally consistent,
and lie as close as possible to the corresponding measured values. Such
consistent values are called *reconciled* values. Within the model the
measured and reconciled values are stored in the identifiers

-  ``MeasuredFlow(f)``,

-  ``MeasuredComposition(f,c)``,

-  ``Flow(f)``, and

-  ``Composition(f,c)``,

where ``f`` is an index into a set of ``Flows``, and ``c`` is an index
into a set of ``Components``. :ref:`this table <table:xml.example-data>` contains
the measured and reconciled flow values and compositions used throughout
this chapter.

.. _table:xml.example-data:

.. table:: Measured and reconciled values

	+---------------------+----------------------------------------------------------------------------+
	| **Flow name**       | **Measured values**                                                        |
	|                     +----------------+-----------------------------------------------------------+
	|                     | **Flow value** | **Flow composition [%]**                                  |
	|                     | **[ton/h]**    +--------------+--------------+--------------+--------------+
	|                     |                | :math:`N_2`  | :math:`H_2`  | :math:`NH_3` | :math:`Ar`   |
	+=====================+================+==============+==============+==============+==============+
	| Inflow              | 111.98         | 26.96        | 72.71        |              | 0.33         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Mix                 |                | 24.56        |              |              | 4.91         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| NH3-Mix             |                | 19.99        |              |              |              |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| NH3-Flow            | 105.59         |              |              |              |              |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Residue             |                |              | 69.68        |              |              |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Ar-Flow             |                |              |              |              |              |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Feedback            | 358.00         |              |              |              |              |
	+---------------------+----------------+--------------+--------------+--------------+--------------+

.. table:: 

	+---------------------+----------------------------------------------------------------------------+
	| **Flow name**       | **Reconciled values**                                                      |
	|                     +----------------+-----------------------------------------------------------+
	|                     | **Flow value** | **Flow composition [%]**                                  |
	|                     | **[ton/h]**    +--------------+--------------+--------------+--------------+
	|                     |                | :math:`N_2`  | :math:`H_2`  | :math:`NH_3` | :math:`Ar`   |
	+=====================+================+==============+==============+==============+==============+
	| Inflow              | 117.03         | 26.96        | 72.71        | 0.00         | 0.33         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Mix                 | 475.03         | 23.95        | 71.08        | 0.05         | 4.91         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| NH3-Mix             | 475.03         | 19.99        | 59.08        | 15.27        | 5.66         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| NH3-Flow            | 105.59         | 0.00         | 0.00         | 100.00       | 0.00         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Residue             | 369.44         | 23.57        | 69.68        | 0.07         | 6.67         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Ar-Flow             | 11.44          | 89.19        | 0.00         | 0.00         | 10.81        |
	+---------------------+----------------+--------------+--------------+--------------+--------------+
	| Feedback            | 358.00         | 22.82        | 70.48        | 0.07         | 6.62         |
	+---------------------+----------------+--------------+--------------+--------------+--------------+

.. rubric:: XML data example

The XML fragment below illustrates a possible XML format to store the
measured and reconciled flows and compositions. The root element
``FlowMeasurementData`` has a ``date`` attribute to indicate the date of
the measurements. The root element contains one or more ``Flow``
elements which contain the measured (if any) and reconciled flow values
for all the flows in the network. Each ``Flow`` element contains a
single ``Composition`` element, which, in turn, contains one or more
``Component`` elements with the measured (if any) and reconciled
composition values for each component of the flow in question.

.. code-block:: aimms

	<FlowMeasurementData xmlns="http://www.aimms.com/Reconciliation" date="2001-10-01">
	    <Flow name="Inflow" measured="111.98" reconciled="117.03">
	        <Composition>
	            <Component name="N2" measured="26.96" reconciled="26.96"/>
	            <Component name="H2" measured="72.71" reconciled="72.71"/>
	            <Component name="Ar" measured="0.33" reconciled="0.33"/>
	        </Composition>
	    </Flow>
	    <Flow name="Mix" reconciled="475.03">
	        <Composition>
	            <Component name="N2" measured="24.56" reconciled="23.95"/>
	            <Component name="H2" reconciled="71.08"/>
	            <Component name="NH3" reconciled="0.05"/>
	            <Component name="Ar" measured="4.91" reconciled="4.91"/>
	        </Composition>
	    </Flow>
	    <Flow name="NH3-Mix" reconciled="475.03">
	        <Composition>
	            <Component name="N2" measured="19.99" reconciled="19.99"/>
	            <Component name="H2" reconciled="59.08"/>
	            <Component name="NH3" reconciled="15.27"/>
	            <Component name="Ar" reconciled="5.66"/>
	        </Composition>
	    </Flow>
	    <Flow name="NH3-Flow" measured="105.59" reconciled="105.59">
	        <Composition>
	            <Component name="NH3" reconciled="100.00"/>
	        </Composition>
	    </Flow>
	    <Flow name="Residue" reconciled="369.44">
	        <Composition>
	            <Component name="N2" reconciled="23.57"/>
	            <Component name="H2" measured="69.68" reconciled="69.68"/>
	            <Component name="NH3" reconciled="0.07"/>
	            <Component name="Ar" reconciled="6.67"/>
	        </Composition>
	    </Flow>
	    <Flow name="Ar-Flow" reconciled="11.44">
	        <Composition>
	            <Component name="N2" reconciled="89.19"/>
	            <Component name="Ar" reconciled="10.81"/>
	        </Composition>
	    </Flow>
	    <Flow name="Feedback" measured="358.00" reconciled="358.00">
	        <Composition>
	            <Component name="N2" reconciled="22.82"/>
	            <Component name="H2" reconciled="70.48"/>
	            <Component name="NH3" reconciled="0.07"/>
	            <Component name="Ar" reconciled="6.62"/>
	        </Composition>
	    </Flow>
	</FlowMeasurementData>

.. rubric:: Not unique

The XML data format illustrated above is not unique. For instance, the
measured and reconciled values could have been represented by child
elements of the ``Flow`` and ``Component`` elements instead of by
attributes. Thus, a different, but equally valid, XML representation of
the same data is illustrated in the XML data snippet below.

.. code-block:: aimms

	<Flow name="Inflow">
	    <MeasuredValue>111.984</MeasuredValue>
	    <ReconciledValue>117.034</ReconciledValue>
	    <Composition>
	        <Component name="N2">
	            <MeasuredValue>26.960</MeasuredValue>
	            <ReconciledValue>26.960</ReconciledValue>
	        </Component>
	        ...
	    </Composition>
	</Flow>

The particular XML data format chosen may be a matter of taste, or the
result of a formal agreement between several parties who wish to use the
corresponding XML data.

.. rubric:: XML schema

To support you in defining a particular XML data format in a formal
manner, XML provides an XML-based standard to specify such definitions.
This standard is called *XML Schema*. It allows you, among other things,
to specify

-  the allowed (tree) structure of a particular XML data format in terms
   of all possible elements and their child elements,

-  the minimum and maximum number of times a particular element can
   occur,

-  which attributes are supported by particular elements,

-  whether attributes are optional or required, and

-  the intended data types of elements and attributes in your XML data
   format.

To create an XML schema file that matches an intended XML data format,
it is best to use one of the tools available for this purpose. For more
detailed information about XML schema, as well as the tools available
for creating an XML schema file, refer to `this page <https://www.w3.org/XML/Schema>`_.

.. rubric:: XML schema example

The following XML schema definition, formally defines the XML data
format as used in the XML data example above.

.. code-block:: aimms

	<xs:schema targetNamespace="http://www.aimms.com/Reconciliation"
	           xmlns="http://www.aimms.com/Reconciliation"
	           xmlns:xs="http://www.w3.org/2001/XMLSchema"
	           elementFormDefault="qualified" attributeFormDefault="unqualified">
	  <xs:element name="FlowMeasurementData">
	    <xs:complexType>
	      <xs:sequence>
	        <xs:element name="Flow" maxOccurs="unbounded">
	          <xs:complexType>
	            <xs:sequence>
	              <xs:element name="Composition" minOccurs="0">
	                <xs:complexType>
	                  <xs:sequence>
	                    <xs:element name="Component" maxOccurs="unbounded">
	                      <xs:complexType>
	                        <xs:attribute name="name" type="xs:string" use="required"/>
	                        <xs:attribute name="measured" type="xs:double" use="optional"/>
	                        <xs:attribute name="reconciled" type="xs:double" use="optional"/>
	                      </xs:complexType>
	                    </xs:element>
	                  </xs:sequence>
	                </xs:complexType>
	              </xs:element>
	            </xs:sequence>
	            <xs:attribute name="name" type="xs:string" use="required"/>
	            <xs:attribute name="measured" type="xs:double" use="optional"/>
	            <xs:attribute name="reconciled" type="xs:double" use="optional"/>
	          </xs:complexType>
	        </xs:element>
	      </xs:sequence>
	      <xs:attribute name="date" type="xs:date" use="required"/>
	    </xs:complexType>
	  </xs:element>
	</xs:schema>

.. rubric:: Schema namespaces

An XML schema definition can specify a namespace by which the schema is
to be known. In the example above, the ``targetNamespace`` attribute of
the ``xs:schema`` element specifies that the schema that follows defines
the namespace ``http://www.aimms.com/XMLSchema/ReconciliationExample``.
In the XML data example listed earlier in this section, the ``xmlns``
attribute of the root element specifies that all element and attribute
names underneath the root element are to be interpreted in the context
of that namespace.

.. rubric:: Two modes of XML support

AIMMS allows you to read and write XML data from within your model in
two modes:

-  it lets AIMMS generate and read XML data based on identifier
   definitions in your model, or

-  it lets AIMMS generate and read XML data according to a given XML
   schema specification.

.. rubric:: AIMMS-generated XML

In the first mode, AIMMS will generate and read XML for the subset of
identifiers that you specify. The format of the generated XML closely
resembles the declaration of the identifiers in your model, generates
XML data for one identifier at a time, and adds a tree level for each
dimension. Letting AIMMS generate XML data for your model is the fastest
way of getting XML data that corresponds to your model, but

-  gives you little control over the final result, and

-  programs that use the generated XML data have to adhere to the
   generated format.

.. rubric:: User-defined XML

In the second mode, AIMMS assumes that you already have a XML schema
file that specifies the precise XML data format that you want to
generate from within AIMMS, or want to read from an external XML data
file. AIMMS provides a tool to let you map the elements and attributes
in the XML schema onto sets and multidimensional identifiers in your
model. Based on this mapping, and the data in your model, you can let
AIMMS generate XML data according to the specified schema, or let AIMMS
fill the corresponding identifiers according to an XML data file in the
specified format.