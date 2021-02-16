.. _sec:set-expr.elem:

Set Element Expressions
=======================

.. rubric:: Use of set element expressions

Set element expressions reference a particular element or element tuple
model from a set or a tuple domain. Set element expressions allow for
*sliced assignment*-executing an assignment only for a
lesser-dimensional subdomain by fixing certain dimensions to a specific
set element. Potentially, this may lead to a vast reduction in execution
times for time-consuming calculations.

.. rubric:: Passing elements from the GUI

The most elementary form of a set element expression is an element
parameter, which turns out to be a useful device for communicating set
element information with the graphical interface. You can instruct AIMMS
to locate the position in a table or other object where an end-user made
changes to a numerical value, and have AIMMS pass the corresponding set
element(s) to an element parameter. As a result, you can execute data
input checks defined over these element parameters, thereby limiting the
amount of computation. This issue is discussed in more detail in the
help regarding the Identifier Selection dialog.

.. rubric:: Element expressions

AIMMS supports several types of set element expressions, including
*references* to parameters and (bound) indices, *lag-lead-expressions*,
element-valued *functions*, and *iterative-expressions*. The last
category turns out to be a useful device for computing the proper value
of element parameters in your model.

.. _element-expression:

.. rubric:: Syntax

*element-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 242.704 227.2"
	   height="227.2"
	   width="242.70399"
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
	         d="m 340,10100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g18"><text
	           id="text22"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,39,1006)"><tspan
	             id="tspan20"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-expressions.html#iterative-expression">iterative-expression</a></tspan></text>
	</g><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1480.28,10100 50,-20 v 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.28,11000 -20,-50 h 40" /><path
	         id="path28"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path30"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 540.043,10400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g32"><text
	           id="text36"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,59.0039,1036)"><tspan
	             id="tspan34"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#function-call">function-call</a></tspan></text>
	</g><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1280.24,10400 50,-20 v 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.28,11000 -20,-50 h 40" /><path
	         id="path42"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 443.258,11000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g44"><text
	           id="text48"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,49.3258,1096)"><tspan
	             id="tspan46"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#quoted-element">quoted-element</a></tspan></text>
	</g><path
	         id="path50"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1377.02,11000 50,-20 v 40" /><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 373.301,10700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,42.3301,1066)"><tspan
	             id="tspan58"
	             y="0"
	             x="0">element-reference</tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1446.98,10700 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.28,11000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 446.68,9500 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g70"><text
	           id="text74"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,49.668,946)"><tspan
	             id="tspan72"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#enumerated-list">enumerated-list</a></tspan></text>
	</g><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1373.6,9500 50,-20 v 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.28,11000 -20,-50 h 40" /><path
	         id="path80"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,11000 -20,-50 h 40" /><path
	         id="path82"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 326.621,9800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g84"><text
	           id="text88"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,37.6621,976)"><tspan
	             id="tspan86"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#operator-expression">operator-expression</a></tspan></text>
	</g><path
	         id="path90"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1493.66,9800 50,-20 v 40" /><path
	         id="path92"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1700.28,11000 -20,-50 h 40" /><path
	         id="path94"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1820.28,11000 -50,20 v -40" /><path
	         id="path96"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,11000 h 120 m 0,0 v -800 c 0,-55.2 44.773,-100 100,-100 v 0 h 120 v 100 h 1140.25 v -100 -100 H 340 v 100 m 1140.28,0 h 120 v 0 c 55.23,0 100,44.8 100,100 v 800 M 120,11000 v -500 c 0,-55.2 44.773,-100 100,-100 h 200.039 120 v 100 h 740.181 v -100 -100 H 540.039 v 100 m 740.201,0 h 120 200.04 c 55.23,0 100,44.8 100,100 v 500 M 120,11000 h 100 103.258 120 v 100 H 1377 v -100 -100 H 443.258 v 100 m 933.762,0 h 120 203.26 M 120,11000 v -200 c 0,-55.2 44.773,-100 100,-100 h 33.301 120 v 100 H 1446.95 v -100 -100 H 373.301 v 100 m 1073.679,0 h 120 33.3 c 55.23,0 100,44.8 100,100 v 200 M 120,11000 V 9600 c 0,-55.23 44.773,-100 100,-100 h 106.68 120 v 100 h 926.89 V 9500 9400 H 446.68 v 100 m 926.92,0 h 120 106.68 c 55.23,0 100,44.77 100,100 v 1400 M 120,11000 V 9900 c 0,-55.23 44.773,-100 100,-100 h -13.379 120 v 100 H 1493.63 V 9800 9700 H 326.621 v 100 m 1167.039,0 h 120 -13.38 c 55.23,0 100,44.77 100,100 v 1100 h 120" /></g></g></svg></div>

The format of list expressions are the same for element and numerical
expressions. They are discussed in :ref:`sec:expr.num.list`.

.. rubric:: Element references

An element reference is any reference to either an element parameter or
a (bound) index.

.. _sec:set-expr.elem.functions:

Intrinsic Functions for Sets and Set Elements
---------------------------------------------

.. _ord-LR:

.. _card-LR:

.. _element-LR:

.. _elementcast-LR:

.. _val-LR:

.. rubric:: The element-related functions...

AIMMS supports functions to obtain the position of an element within a
set, the cardinality (i.e. number of elements) of a set, the
:math:`n`-th element in a set, the element in a non-compatible set with
the identical string representation, and the numerical value represented
by a set element. If ``S`` is a set identifier, ``i`` an index bound to
``S``, :math:`l` an element, and :math:`n` a positive integer, then
possible calls to the :any:`Ord`, :any:`Card`, :any:`Element`, :any:`ElementCast`
and :any:`Val` functions are given in :ref:`this table <table:set-expr.set-func>`.

.. _table:set-expr.set-func:

.. table:: Intrinsic functions operating on sets and set elements

   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Function                           | Value       | Meaning                                                                                                                                          |
   +====================================+=============+==================================================================================================================================================+
   | ``Ord(i)``                         | *integer*   | Ordinal, returns the relative position of the index ``i`` in the set ``S``. Does *not* bind ``i``.                                               |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | ``Ord(``\ :math:`l`\ ``,S)``       | *integer*   | Returns the relative position of the element :math:`l` in set ``S``. Returns zero if :math:`l` is not an element of ``S``.                       |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | ``Card(S)``                        | *integer*   | Cardinality of set ``S``.                                                                                                                        |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | ``Element(S,``\ :math:`n`\ ``)``   | *element*   | Returns the element in set ``S`` at relative position :math:`n`. Returns the empty element tuple if ``S`` contains less then :math:`n` elements. |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | ``ElementCast(S``,:math:`l`\ ``)`` | *element*   | Returns the element in set ``S``, which corresponds to the textual representation of an element :math:`l` in any other index set.                |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | ``Val(``\ :math:`l`\ ``)``         | *numerical* | Returns the numerical value represented by :math:`l`, or a runtime error if :math:`l` cannot be interpreted as a number                          |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Max`:math:`(e_1,\dots,e_n)`  | *Max*       | Returns the set element with the highest ordinal                                                                                                 |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :any:`Min`:math:`(e_1,\dots,e_n)`  | *Min*       | Returns the set element with the lowest ordinal                                                                                                  |
   +------------------------------------+-------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

.. rubric:: ...for simple sets

The :any:`Ord`, :any:`Card` and :any:`Element` functions can be applied to simple
sets. In fact you can even apply :any:`Card` to parameters and variables-it
simply returns the number of nondefault elements associated with a
certain data structure.

.. rubric:: Crossing root set boundaries

By default, AIMMS does not allow you to use indices associated with one
root set hierarchy in your model, in references to index domains
associated with another root set hierarchy of your model. The function
:any:`ElementCast` allows you to cross root set boundaries, by returning
the set element in the root set associated with the first (set) argument
that has the identical name as the element (in another root set) passed
as the second argument. The function :any:`ElementCast` has an optional
third argument *create* (values 0 or 1, with a default of 0), through
which you can indicate whether you want elements which cannot be cast to
the indicated set must be created within that set. In this case, a call
to :any:`ElementCast` will never fail. You can find more information about
root sets, as well as an illustrative example of the use of
:any:`ElementCast`, in :ref:`sec:bind.rules`.

.. rubric:: Example

In this example, we again use the set ``Cities`` initialized through the
statement

.. code-block:: aimms

	Cities := DATA { Amsterdam, Rotterdam, 'The Hague', London, Paris, Berlin, Madrid } ;

The following table illustrates the intrinsic element-valued functions.

.. table:: 

	============================ ============================
	Expression                   Result
	============================ ============================
	``Ord('Amsterdam', Cities)`` 1
	``Ord('New York', Cities)``  0 (i.e. not in the set)
	``Card(Cities)``             7
	``Element(Cities, 1)``       ``'Amsterdam'``
	``Element(Cities, 8)``       ``"`` (i.e. no 8-th element)
	============================ ============================
	
.. rubric:: The :any:`Val` function

If your model contains a set with elements that represent numerical
values, you cannot directly use such elements as a numerical value in
numerical expressions, unless the set is an integer set (see
:ref:`sec:set.integer`). To obtain the numerical value of such set
elements, you can use the :any:`Val` function. You can also apply the
:any:`Val` function to strings that represent a numerical value. In both
cases, a runtime error will occur if the element or string argument of
the :any:`Val` function cannot be interpreted as a numerical value.

.. rubric:: The :any:`Min` and :any:`Max` functions

The element-valued :any:`Min` and :any:`Max` functions operate on two or more
element-valued expressions *in the same (sub-)set hierarchy*. If the
arguments are references to element parameters (or bound indices), then
the ``Range`` attributes of these element parameters or indices must be
sets in a single set hierarchy. Through these functions you can obtain
the elements with the lowest and highest ordinal relative to the set
equal to highest ranking range set in the subset hierarchy of all its
arguments. If one or more of the arguments are explicit labels, then
AIMMS will verify that these labels are contained in that set, or will
return an error otherwise. A compiler error will result, if no such set
can be determined (i.e., when the function call refers to explicit
labels only).

.. _sec:set-expr.elem.iter:

Element-valued Iterative Expressions
------------------------------------

.. _first-LR:

.. _last-LR:

.. _nth:

.. _argmin:

.. _argmax:

.. rubric:: Selecting elements

AIMMS offers special iterative operators that let you select a specific
element from a domain. :ref:`this table <table:set-expr.elem-iter>` shows all such
operators that result in a set element value. The syntax of iterative
operators is explained in :ref:`sec:set-expr.set.sort`. The second
column in this table refers to the required number of expression
arguments following the binding domain argument.

.. _table:set-expr.elem-iter:

.. table:: Element-valued iterative operators

   +--------------+---------+------------------------------------------------------------------------------------------------+
   | Name         | # Expr. | Computes for all elements in the domain                                                        |
   +==============+=========+================================================================================================+
   | :any:`First` | 0       | the first element (tuple)                                                                      |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | :any:`Last`  | 0       | the last element (tuple)                                                                       |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | ``Nth``      | 1       | the :math:`n`-th element (tuple)                                                               |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | :any:`Min`   | 1       | the value of the element expression for which the expression reaches its minimum ordinal value |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | :any:`Max`   | 1       | the value of the element expression for which the expression reaches its maximum ordinal value |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | ``ArgMin``   | 1       | the first element (tuple) for which the expression reaches its minimum value                   |
   +--------------+---------+------------------------------------------------------------------------------------------------+
   | ``ArgMax``   | 1       | the first element (tuple) for which the expression reaches its maximum value                   |
   +--------------+---------+------------------------------------------------------------------------------------------------+

.. rubric:: Single index

The binding domain of the :any:`First`, :any:`Last`, ``Nth``, :any:`Min`,
:any:`Max`, ``ArgMin``, and ``ArgMax`` operator can only consist of a
single index in either a simple set, and the result is a single element
in that domain. You can use this result directly for indexing or
referencing an indexed parameter or variable. Alternatively, you can
assign it to an element parameter in the appropriate domain.

.. rubric:: Compared expressions

The ``ArgMin`` and ``ArgMax`` operators return the element for which an
expression reaches its minimum or maximum value. The allowed expressions
are:

-  numerical expressions, in which case AIMMS performs a numerical
   comparison,

-  string expressions, in which case AIMMS uses the normal alphabetic
   ordering, and

-  element expressions, in which case AIMMS compares the ordinal numbers
   of the resulting elements.

For element expressions, the iterative :any:`Min` and :any:`Max` operators
return expression *values* with the minimum and maximum ordinal value.

.. rubric:: Example

The following assignments illustrate the use of some of the domain
related iterative operators. The identifiers on the left are all element
parameters.

.. code-block:: aimms

	FirstNonSupplyCity    := First ( i | not Exists(j | Transport(i,j)) ) ;
	SecondSupplyCity      := Nth   ( i | Exists(j | Transport(i,j)), 2  ) ;
	SmallestSupplyCity    := ArgMin( i, Sum(j, Transport(i,j))          ) ;
	LargestTransportRoute := ArgMax( r, Transport(r)                    ) ;

Note that the iterative operators ``Exists`` and ``Sum`` are used here
for illustrative purposes, and are not set- or element-related. They are
treated in :ref:`sec:expr.logic.iter` and :ref:`sec:expr.num.iter`,
respectively.

.. _sec:set-expr.elem.lag-lead:

Lag and Lead Element Operators
------------------------------

.. rubric:: Lag and lead operators...

There are four binary element operators, namely the lag and lead
operators ``+``, ``++``, ``-`` and ``--``. The first operand of each of
these operators must be an element reference (such as an index or
element parameter), while the second operand must be an integer
numerical expression. There are no unary element operators.

.. rubric:: ...explained

Lag and lead operators are used to relate an index or element parameter
to preceding and subsequent elements in a set. Such correspondence is
well-defined, except when a request extends beyond the bounds of the
set.

.. rubric:: Noncircular versus circular

There are two kinds of lag and lead operators, namely *noncircular* and
*circular* operators which behave differently when pushed beyond the
beginning and the end of a set.

-  The noncircular operators (``+`` and ``-``) consider the ordered set
   elements as a *sequence* with no elements before the first element or
   after the last element.

-  The circular operators (``++`` and ``--``) consider ordered set
   elements as a *circular chain*, in which the first and last elements
   are linked.

.. rubric:: Definition

Let ``S`` be a set, ``i`` a set element expression, and :math:`k` an
integer-valued expression. The lag and lead operators ``+``, ``++``,
``-``, ``--`` return the element of ``S`` as defined in
:ref:`this table <table:set-expr.lag-lead>`. Please note that these operators are
also available in the form of ``+=``, ``-=``, ``++=`` and ``--=``. The
operators in this form can be used in statements like:

.. code-block:: aimms

	CurrentCity := 'Amsterdam';
	CurrentCity --= 1; ! Equal to CurrentCity := CurrentCity -- 1;

.. _table:set-expr.lag-lead:

.. table:: Lag and lead operators

   +------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | Lag/lead expr.                           | Meaning                                                                                                        |
   +==========================================+================================================================================================================+
   | :math:`\mathtt{i}\mathbin{\mathrm{+}}k`  | The element of ``S`` positioned :math:`k` elements after ``i``; the empty element if there is no such element. |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | :math:`\mathtt{i}\mathbin{\mathrm{++}}k` | The circular version of :math:`\mathtt{i}\mathbin{\mathtt{+}}k`.                                               |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | :math:`\mathtt{i}\mathbin{\mathrm{-}}k`  | The member of ``S`` positioned :math:`k` elements before ``i``; the empty element if there is no such element. |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | :math:`\mathtt{i}\mathbin{\mathrm{--}}k` | The circular version of :math:`\mathtt{i}\mathbin{\mathtt{-}}k`.                                               |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------+

.. rubric:: Lag and lead operators for integer sets

For elements in integer sets, AIMMS may interpret the ``+`` and ``-``
operators either as lag/lead operators or as numerical operators.
:ref:`sec:set.integer` discusses the way in which you can steer which
interpretation AIMMS will employ.

.. rubric:: Not for literal elements

You cannot always use lag and lead operators in combination with literal
set elements. The reason for this is clear: a literal element can be an
element of more than one set, and in general, unless the context in
which the lag or lead operator is used dictates a particular (domain)
set, it is impossible for AIMMS to determine which set to work with.

.. rubric:: Verify the effect of lags and leads

Lag and lead operators are frequently used in indexed parameters and
variables, and may appear on the left- and right-hand side of
assignments. You should be careful to check the correct use of the lag
and lead operators to avoid making conceptual errors. For more specific
information on the lag and lead operators refer to
:ref:`sec:exec.assign`, which treats assignments to parameters and
variables.

.. rubric:: Example

Consider the set ``Cities`` initialized through the assignment

.. code-block:: aimms

	Cities := DATA { Amsterdam, Rotterdam, 'The Hague', London, Paris, Berlin, Madrid } ;

Assuming that the index ``i`` and the element parameter ``CurrentCity``
both currently refer to ``'Rotterdam'``,
:ref:`this table <table:set-expr.lag-lead-examp>` illustrates the results of
various lag/lead expressions.

.. _table:set-expr.lag-lead-examp:

.. table:: Example of lag and lead operators

   =================== ===============
   Lag/lead expression Result
   =================== ===============
   ``i+1``             ``'The Hague'``
   ``i+6``             ``"``
   ``i++6``            ``'Amsterdam'``
   ``i++7``            ``'Rotterdam'``
   ``i-2``             ``"``
   ``i-2``             ``'Madrid'``
   ``CurrentCity+2``   ``'London'``
   ``'Rotterdam' + 1`` ERROR
   =================== ===============