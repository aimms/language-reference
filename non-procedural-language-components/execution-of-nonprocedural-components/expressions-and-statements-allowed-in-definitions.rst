.. _sec:nonproc.allowed:

Expressions and Statements Allowed in Definitions
=================================================

.. rubric:: Complicated definitions

In most applications, the functional relationship between input and
output identifiers in the definition of a set or a parameter can be
expressed as an ordinary string-valued, set-valued, set element-valued or numerical
expression. In rare occasions where a functional relationship cannot be
written as a single symbolic statement, a function or procedure can be
used instead.

.. rubric:: Allowed definitions

In summary, you may use one of the following items in set and parameter
definitions:

-  a string-valued expression,

-  a set-valued expression,

-  an element-valued expression,

-  a numerical expression,

-  a call to a function, or

-  a call to a procedure.

.. rubric:: Limited selfreferencing allowed

Under some conditions, expressions used in the definition of a
particular parameter can contain references to the parameter itself.
Such self-referencing is allowed if the *serial* computation of the
definition over all elements in the index domain of the parameter does
not result in a cyclic reference to the parameter at the individual
level. This is useful, for instance, when expressing stock balances in a
functional manner with the use of lag operators.

.. rubric:: Example

The following definition illustrates a valid example of a
self-reference.

.. code-block:: aimms

	Parameter Stock {
	    IndexDomain  : t;
	    Definition   : {
	        if ( t = FirstPeriod ) then BeginStock
	            else Stock(t-1) + Supply(t) - Demand(t) endif
	    }
	}

If ``t`` is an index into a set ``Periods =``\ ``{0..3}``, and
``FirstPeriod`` equals ``0``, then at the individual level the
assignments with self-references are:

.. code-block:: aimms

	Stock(0) := BeginStock ;
	Stock(1) := Stock(0) + Supply(1) - Demand(1) ;
	Stock(2) := Stock(1) + Supply(2) - Demand(2) ;
	Stock(3) := Stock(2) + Supply(3) - Demand(3) ;

Since there is no cyclic reference, the above definition is allowed.

.. rubric:: Functions and procedures

You can use a call to either a function or a procedure to compute those
definitions that cannot be expressed as a single statement. If you use a
procedure, then 

#.  for sets, no arguments are allowed, 

#.  for parameters, some input arguments and at most one output argument are allowed. 

In addition,
the procedure cannot have any side-effects on other global sets or
parameters. This means that no direct assignments to other global sets
or parameters are allowed.

.. rubric:: Arguments and global references

The identifiers referenced in the actual arguments of a procedure call,
as well as the global identifiers that are referenced in the body of the
procedure, will be considered as input parameters for the computation of
the current definition. That is, data changes to any of these input
identifiers will trigger the re-execution of the procedure to make the
definition up-to-date. The same applies to functions used inside
definitions.

.. rubric:: Examples

The following two examples illustrate the use of functions and
procedures in definitions.

-  Consider a function ``TotalCostFunction`` which has a single argument
   for individual cost coefficients. Then the following declaration
   illustrates a definition with a function reference.

   .. code-block:: aimms
   
   	Parameter TotalCost {
   	    Definition : TotalCostFunction( CostCoefficient );
   	}

   AIMMS will consider the actual argument ``CostCoefficient``, as well
   any other global identifier referenced in the body of
   ``TotalCostFunction`` as input parameters of the definition of
   ``TotalCost``.

-  Similarly, consider a procedure ``TotalCostProcedure`` which performs
   the same computation as the function above, but returns the result
   via a (single) output argument. Then the following declaration
   illustrates an equivalent definition with a procedure reference.

   .. code-block:: aimms
   
   	Parameter TotalCost {
   	    Definition : TotalCostProcedure( CostCoefficient, TotalCost );
   	}

.. rubric:: One procedure for several definitions

Whenever the values of a number of identifiers are computed
simultaneously inside a single procedure without arguments, then this
procedure must be referenced inside the definition of each and all of
the corresponding identifiers. If you do not reference the procedure for
all corresponding identifiers, a compile-time error will result. All
other global identifiers used inside the body of the procedure count as
input identifiers.

.. rubric:: Example

Consider a procedure ``ComputeCosts`` which computes the value of the
global parameters ``FixedCost(m,p)`` and ``VariableCost(m,p)``
simultaneously. Then the following example illustrates a valid use of
``ComputeCosts`` inside a definition.

.. code-block:: aimms

	Parameter FixedCost {
	    IndexDomain  : (m,p);
	    Definition   : ComputeCosts;
	}
	Parameter VariableCost {
	    IndexDomain  : (m,p);
	    Definition   : ComputeCosts;
	}

Omitting ``ComputeCosts`` in either definition will result in a
compile-time error.