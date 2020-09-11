.. _sec:extern.constraints:

External Functions in Constraints
=================================

.. rubric:: Variable arguments

AIMMS allows you to use external functions in the constraints of a
mathematical program. To accommodate this, AIMMS makes a distinction
between function arguments of type ``Parameter`` and arguments of type
``Variable``. When a function is executed as part of an expression in an
ordinary assignment, AIMMS makes no distinction between both types of
arguments. In the context of a mathematical program, however, AIMMS will
provide the solver with the derivative information for all variable
arguments of the function, while it will not do so for parameter
arguments. The actual computation of the derivatives is explained in the
next section.

.. _sec:intern.func.derivative:

Derivative Computation
----------------------

.. rubric:: Functions in constraints

Whenever you use external functions with variable arguments in
constraints of a mathematical program, the following rules apply.

-  AIMMS requires that the mathematical program dependent on these
   constraints be declared as nonlinear.

-  All the actual variable arguments must correspond to formal arguments
   which have been locally declared as ``Variables``.

If you fail to comply with these rules, a compiler error will result.

.. rubric:: Providing derivatives

During the solution process of a mathematical program containing such
functions, partial derivative information of the function with respect
to all the variable arguments must be passed to the solver. AIMMS
supports three methods to compute the derivatives of a function:

-  you provide the actual statements for computing the derivatives as a
   part of the function declaration,

-  AIMMS estimates the derivatives using a simple differencing scheme.

.. _external_function.derivative_call:

.. rubric:: The ``DerivativeCall`` attribute

In the ``DerivativeCall`` attribute of an external function you can
specify the call to the DLL procedure or function, to which the
derivative computation must be relayed. The syntax of the
``DerivativeCall`` attribute is the same as that of the ``BodyCall``,
and is most conveniently completed using the wizard in the Model
Explorer.

.. rubric:: Function value and derivative

If the nonlinear solver only needs a function value, AIMMS will simply
call the function specified in the ``BodyCall`` attribute. If the
nonlinear solver requests derivative information as well, AIMMS will
only call the function specified in the ``DerivativeCall`` attribute,
and require that this function compute the function value as well. By
combining these two computations in a single call, AIMMS allows you to
take advantage of any possible optimization that can be obtained in your
code from computing the function value and derivative at the same time.

.. _derivative:

.. rubric:: The :ref:`.Derivative` suffix

For every function argument which is a variable, you must assign the
partial derivative value(s) to the :ref:`.Derivative` suffix of that
variable. Note that this will have an impact on the number of indices.
If the result of a block-valued function is :math:`m`-dimensional, the
derivative information with respect to an :math:`n`-dimensional variable
argument will result in an :math:`(m+n)`-dimensional identifier holding
the derivative.

.. rubric:: Abstract example

Consider a function ``f`` with an index domain :math:`(i_1,\dots,i_m)`
and a variable argument ``x`` with index domain :math:`(j_1,\dots,j_n)`.
Then the matrix with partial derivatives of ``f`` with respect to the
argument ``x`` must be provided as assignments to the suffix
:math:`{\texttt{x.Derivative}}(i_1,\dots,i_m,j_1,\dots,j_n)`. Each
element of this identifier represents the partial derivative

.. math::

   \frac{\partial {\texttt{f}}(i_1,\dots,i_m)}
                {\partial {\texttt{x}}(j_1,\dots,j_n)}

.. rubric:: Cobb-Douglas function revisited

Consider the Cobb-Douglas function discussed above. Although AIMMS is
capable of computing its partial derivatives automatically, you may
verify that the derivative with respect to argument :math:`c_i` can also
be written more compactly as follows:

.. math:: \frac{\partial q}{\partial c_i} = \frac{a_i}{c_i}CD(c_1, \ldots, c_k)

.. rubric:: Implementation in C

Consider the following ``C`` function ``Cobb_Douglas_Der`` which
computes the Cobb-Douglas function and, if required, also the partial
derivatives with respect to the input argument ``c``. The function
``Cobb_Douglas_No_Der`` is added to support computation of the
Cobb-Douglas function without derivatives.

.. code-block:: aimms

	double Cobb_Douglas_Der( int n, double *a, double *c, double *c_der ) {
	  int i;
	  double CD = 1.0 ;

	  for ( i = 0; i < n; i++ )
	    CD = CD * pow(c[i],a[i]) ;

	  /* Check if derivatives are needed */
	  if ( c_der )
	    for ( i = 0; i < n; i++ )
	      c_der[i] = CD * a[i] / c[i] ;

	  return CD;
	}

	double Cobb_Douglas_No_Der( int n, double *a, double *c ) {
	  return Cobb_Douglas_Der( n, a, c, NULL );
	}

.. rubric:: Always skip unwanted derivatives

Note that in the above example the derivative computation is skipped
whenever the pointer ``c_der`` is null. You should *always* check for
this condition when implementing a derivative computation, because AIMMS
will pass a null pointer (and hence reserve no memory for storing the
derivative) whenever the corresponding actual argument is not a variable
but a parameter.

.. rubric:: ...in ``FORTRAN`` code

When an internal function makes a call to a ``FORTRAN`` procedure to
compute derivative values, then it is not so easy to discover the
presence of null pointer argument. To overcome this, you can call your
``FORTRAN`` procedure from within a wrapper function written in ``C``,
and provide your ``FORTRAN`` code with the information whether or not
derivatives need to be computed for a particular variable argument via
an additional argument to your ``FORTRAN`` routine.

.. rubric:: Passing derivative arguments

To pass the partial derivatives computed in the external procedure back
to AIMMS, the argument list of the external procedure called in the
``Derivative`` attribute of the internal function should contain
arguments for the :ref:`.Derivative` suffices of all variable arguments.
AIMMS will implicitly consider such derivative arguments as ``Output``
arguments. They can be passed either as a full array or as an integer
``handle``. In the latter case AIMMS API functions have to be used to
pass back the relevant partial derivatives (see also :ref:`chap:api`).

.. rubric:: Example continued

The following external function declaration provides an interface to the
above Cobb-Douglas function with derivative computations, which is ready
to be used both inside and outside the context of constraints.

.. code-block:: aimms

	ExternalFunction CobbDouglasPlusDerivative {
	    Arguments       : (a,c);
	    Range           : nonnegative;
	    DLLName         : "Userfunc.dll";
	    ReturnValue     : double;
	    BodyCall        : Cobb_Douglas_No_Der( card : InputFactors, array: a, array: c );
	    DerivativeCall  : {
	        Cobb_Douglas_Der( card : InputFactors, array: a,
	            array: c, array: c.Derivative );
	    }
	}

.. rubric:: Numerical differencing

When the ``DerivativeCall`` attribute to compute the derivatives of an
external function has not been specified, AIMMS employs a simple
differencing scheme to estimate the derivatives. For example, if AIMMS
requires the derivative of a function :math:`f(x_1, x_2,\ldots, x_k)` at
the point :math:`(\bar x_1, \bar x_2, \ldots, \bar x_k)`, then AIMMS
will approximate each partial derivative as follows:

.. math::

   \frac{\partial}{\partial x_i}f(\bar x_1, \bar x_2, \ldots, \bar x_k)
     \approx \frac{{f(\bar x_1,\ldots, \bar x_i + \varepsilon, \ldots,
     \bar x_k ) - f(\bar x_1, \ldots, \bar x_k)}}{\varepsilon}

where :math:`\varepsilon` is the current value of the global option
``Differencing_Delta``.

.. rubric:: Disadvantages of numerical differencing

While the numerical differencing scheme does not require any action from
the user, there are two distinct disadvantages.

-  First of all, numerical differencing is not always a stable process,
   and the results may not be accurate enough. As a result, a nonlinear
   solver may have trouble converging to a solution.

-  Secondly, the process can be computationally very expensive.

In general, it is recommended that you do not rely on numerical
differencing. This is especially the case when the function body is
quite extensive, or when the function, at the individual level, has a
lot of variable arguments or contains conditional loops.