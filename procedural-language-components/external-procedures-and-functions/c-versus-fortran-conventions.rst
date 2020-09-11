.. _sec:extern.language:

``C`` Versus ``FORTRAN`` conventions
====================================

.. rubric:: Language conventions

For any external procedure or function you can specify whether the DLL
procedure or function to which the execution is relayed, is written in
``C``-like languages (such as ``C`` and ``C++``) or ``FORTRAN`` (see
also :ref:`sec:extern.declaration`). For ``FORTRAN`` code AIMMS will
make sure that

-  scalar values are always passed by reference (i.e. as a pointer), and

-  multidimensional arrays are ordered in a ``FORTRAN``-compatible
   manner.

By default, AIMMS will use ``C`` conventions when passing arguments to
the DLL procedure or function.

.. rubric:: Strings excluded

AIMMS will not directly translate strings into ``FORTRAN`` format,
because most ``FORTRAN`` compilers use their own particular string
representation. Thus, if you want to pass strings to a ``FORTRAN``
subroutine, you should write your own ``C`` interface which converts
``C`` strings into the format appropriate for your ``FORTRAN`` compiler.

.. rubric:: Array dimensions and ordering

When a multidimensional parameter (or parameter slice) is specified as a
``array`` argument to an external procedure, AIMMS passes an array of
the specified type which is constructed as follows. If the actual
argument has :math:`n` remaining (i.e. non-sliced) dimensions of
cardinality :math:`N_1,\dots,N_n`, respectively, then the associated
values are passed as a (one-dimensional) array of length
:math:`N_1\cdots N_n`. The value associated with the tuple
:math:`(i_1,\dots,i_n)` is mapped onto the element

.. math::

   i_n + N_n\bigl( i_{n-1} + N_{n-1}\bigl( \cdots \bigl( i_2 +
            N_2 i_1\bigr) \cdots \bigr)\bigr)

for running indices :math:`i_j=0,\dots,N_j-1` (``C``-style programming).
For ``Pascal``-like languages (with indices running from
:math:`1,\dots,N`) all running indices in this formula must be decreased
by 1, and the final result increased by 1. This ordering is compatible
with the ``C`` declaration of e.g. the multidimensional array

   double arr[:math:`N_1`][:math:`N_2`]...[:math:`N_n`];

.. rubric:: Multidimensional example in C

The ``C`` function ``ComputeAverage`` defined below computes the average
of a 2-dimensional parameter ``a(i,j)`` passed as an argument in AIMMS.

.. code-block:: aimms

	DLL_EXPORT(void) ComputeAverage( double *a, int card_i, int card_j, double *average )
	{ int i, j;
	  double sum_a = 0.0;

	#define __A(i,j)    a[j + i*card_j]

	  for ( i = 0; i < card_i; i++ )
	    for ( j = 0; j < card_j; j++ )
	      sum_a += __A(i,j);

	  *average = sum_a / (card_i*card_j);
	}

Within your AIMMS model, you can call this procedure via an external
procedure declaration ``ExternalAverage`` defined as follows.

.. code-block:: aimms

	ExternalProcedure ExternalAverage {
	    Arguments     : (x,res);
	    DLLName       : "Userfunc.dll";
	    BodyCall      : ComputeAverage(double array: x, card: i, card: j, double scalar: res);
	}

where the argument ``x`` and ``res`` are declared as

.. code-block:: aimms

	Parameter x {
	    IndexDomain   : (i,j);
	    Property      : Input;
	}
	Parameter res {
	    Property      : Output;
	}

.. rubric:: ``FORTRAN`` array ordering

When you specify the ``FORTRAN`` language convention for an external
procedure, AIMMS will order the array passed to the external procedure
such that the tuple :math:`(i_1,\dots,i_n)` is mapped onto the element

.. math::

   i_1 + N_1\bigl( i_{2} - 1 + N_{2}\bigl( \cdots \bigl( i_{n-1} -1 +
            N_{n-1} \bigl(i_n-1\bigr)\bigr) \cdots \bigr)\bigr)

for running indices :math:`i_j=1,\dots,N_j`. This is compatible with the
default storage of multidimensional arrays in ``FORTRAN``, and allows
you to access such array arguments using the ordinary multidimensional
notation.

.. rubric:: Example

Consider a parameter ``a(i,j)``, where the index ``i`` is associated
with the set {``1``, ``2``} and ``j`` with the set {``1``, ``2``,
``3``}. When this parameter is passed as a ``array`` argument to an
external procedure, the resulting array (as a one-dimensional array with
6 elements) is ordered as follows in the ``C`` convention (default).

.. math::

   \begin{array}{|l|c|c|c|c|c|c|}
   \hline
   \mathbf{Element\:\#} & 0 & 1 & 2 & 3 & 4 & 5 \\
   \hline \mathbf{Value} & \mathtt{a(1,1)} & \mathtt{a(1,2)} & \mathtt{a(1,3)} &
   \mathtt{a(2,1)} & \mathtt{a(2,2)} & \mathtt{a(2,3)} \\
   \hline
   \end{array}

With the ``FORTRAN`` language convention, the ordering is changed as
follows.

.. math::

   \begin{array}{|l|c|c|c|c|c|c|}
   \hline
   \mathbf{Element\:\#} & 1 & 2 & 3 & 4 & 5 & 6 \\
   \hline \mathbf{Value} & \mathtt{a(1,1)} & \mathtt{a(2,1)} & \mathtt{a(1,2)} &
   \mathtt{a(2,2)} & \mathtt{a(1,3)} & \mathtt{a(2,3)} \\
   \hline
   \end{array}