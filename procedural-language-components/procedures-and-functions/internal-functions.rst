.. _sec:intern.func:

Internal Functions
==================

.. rubric:: Similar to procedures

The specification of a function is very similar to that of a procedure.
The following items provide a summary of their similarities.

-  Arguments, together with their attributes, must be declared in a
   local declaration subnode.

-  The domain and range of indexed arguments can be in terms of either
   global or local sets.

-  The units of arguments can be expressed in terms of globally defined
   units of measurement, or in locally defined unit parameters.

-  Optional arguments must be scalar, and you must specify a default
   value.

-  AIMMS performs range checking on the actual arguments at runtime.

-  Both functions and procedures can have a ``RETURN`` statement.

.. rubric:: There are differences

There are also differences between a function and a procedure, as
summarized below:

-  Functions return a result that can be used in numerical expressions.
   The result can be either scalar-valued or indexed, and can have an
   associated unit of measurement.

-  Functions cannot have side effects either on global identifiers or on
   their arguments, i.e. every function argument is of type ``Input`` by
   definition.

.. rubric:: Not allowed in constraints

AIMMS only allows the (possibly multi-dimensional) result of a function
to be used in constraints if none of the function arguments are
variables. Allowing function arguments to be variables, would require
AIMMS to compute the Jacobian of the function with respect to its
variable arguments, which is not a straightforward task. External
functions in AIMMS do support variables as arguments (see also
:ref:`sec:extern.constraints`).

.. rubric:: Example: the Cobb-Douglas function
   :name: examp:Cobb-Douglas

The Cobb-Douglas (CD) function is a scalar-valued function that is often
used in economical models. It has the following form:

.. math:: q = CD_{(a_1,\ldots,a_k)}(c_1, \ldots, c_k) = \prod_f c_f^{a_f},

where

+-------------+-------------------------------------------------------+
| :math:`q`   | is the quantity produced,                             |
+-------------+-------------------------------------------------------+
| :math:`c_f` | is the factor input :math:`f`,                        |
+-------------+-------------------------------------------------------+
| :math:`a_f` | is the share parameter satisfying :math:`a_f\geq 0`   |
|             | and :math:`\sum_f a_f = 1`.                           |
+-------------+-------------------------------------------------------+

In its simplest form, the declaration of the Cobb-Douglas function could
look as follows.

.. code-block:: aimms

	Function CobbDouglas {
	    Arguments  : (a,c);
	    Range      : nonnegative;
	    Body       : {
	        CobbDouglas := prod[f, c(f)^a(f)]
	    }
	}

The arguments of the ``CobbDouglas`` function must be declared in a
local declaration subnode. The following declarations describe the
arguments.

.. code-block:: aimms

	Set InputFactors {
	    Index        : f;
	}
	Parameter a {
	    IndexDomain  : f;
	}
	Parameter c {
	    IndexDomain : f;
	}

.. _function:

.. rubric:: Function attributes

The attributes of functions are listed in
:numref:`table:intern.attr-func`. Most of them are the same as those of
procedures.

.. _table:intern.attr-func:

.. table:: 

	=============== ================= ====================================
	Attribute       Value-type        See also
	=============== ================= ====================================
	``Arguments``   *argument-list*      
	``IndexDomain`` *index-domain*    :ref:`here <attr:par.index-domain>`
	``Range``       *range*           :ref:`here <attr:par.range>`
	:any:`Unit`     *unit-expression* :ref:`here <attr:par.unit>`
	``Property``    ``RetainsValue``     
	``Body``        *statements*      :ref:`chap:exec`
	``Comment``     *comment string*     
	=============== ================= ====================================
	
.. _function.index_domain:

.. rubric:: Returning the result

By providing an index domain to the function, you indicate that the
result of the function is multidimensional. Inside the function you can
use the function name with its indices as if it were a locally defined
parameter. The result of the function must be assigned to this
'parameter'. As a consequence, the body of any function should contain
at least one assignment to itself to be useful. Note that the ``RETURN``
statement cannot have a return value in the context of a function body.

.. rubric:: The ``Range`` attribute
   :name: attr:function.range

.. _function.range:

Through the ``Range`` attribute you can specify in which numerical, set,
element or string range the function should assume its result. If the
result of the function is numeric and multidimensional, you can specify
a range using multidimensional parameters which depend on all or only a
subset of the indices specified in the ``IndexDomain`` of the function.
This is similar as for parameters (see also page :ref:`attr:par.range`).
Upon return from the function, AIMMS will verify that the function
result lies within the specified range.

.. rubric:: The :any:`Unit` attribute
   :name: attr:function.unit

.. _function.unit:

Through the :any:`Unit` attribute of a function you can associate a unit
with the function result. AIMMS will use the unit specified here during
the unit consistency check of each assignment to the result parameter
within the function body, based on the units of the global identifiers
and function arguments that are referenced in the assigned expression.
In addition, AIMMS will use the value of the :any:`Unit` attribute during
unit consistency checks of all expressions that contain calls to the
function at hand. You can find general information on the use of units
in :ref:`chap:units`. :ref:`sec:units.analysis.arg` focusses on unit
consistency checking for functions and procedures.

.. rubric:: Example: computing the shortest distance

The procedure ``ComputeShortestDistance`` discussed in the previous
section can also be implemented as a function ``ShortestDistance``,
returning an indexed result. In this case, the declaration looks as
follows.

.. code-block:: aimms

	Function ShortestDistance {
	    Arguments    : (City, DistanceMatrix);
	    IndexDomain  : j;
	    Range        : nonnegative;
	    Comment      : {
	        "This procedure computes the distance along the shortest path
	         from City to any other city j, given DistanceMatrix."
	    }
	    Body         : {
	        ShortestDistance(j) := DistanceMatrix(City,j);

	        for ( j | not ShortestDistance(j) ) do
	            /*
	             *  Compute the shortest path and the corresponding distance
	             *  for cities j without a direct connection to City.
	             */
	        endfor
	    }