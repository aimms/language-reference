.. _sec:extern.intro:

Introduction
============

.. rubric:: Getting started

The aim of this section is to give you a quick feel for the effort
required to make a link to an external function or procedure through a
short illustrative example linking a ``C`` implementation of the
Cobb-Douglas function (discussed in :ref:`examp:Cobb-Douglas`) into an
AIMMS application. :ref:`sec:api.intro` contains a more elaborate
example of an external procedure which uses AIMMS API functions to
obtain additional information about the passed arguments.

.. rubric:: External procedures and functions

The interface to external procedures and functions is arranged through
special ``ExternalProcedure`` and ``ExternalFunction`` declarations
which behave just like internal procedures and functions. Instead of
specifying a body to initiate internal AIMMS computations, the execution
of external procedures and functions is relayed to the indicated
procedures and functions inside one or more DLL's.

.. rubric:: The Cobb-Douglas function

Consider the ``Cobb-Douglas`` function discussed in
:ref:`examp:Cobb-Douglas`. Given the cardinality ``n`` of the set
``InputFactors`` and two arrays ``a`` and ``c`` of doubles representing
the one-dimensional input arguments of the Cobb-Douglas function (both
defined over ``InputFactors``), the following simple ``C`` function
computes its value.

.. code-block:: aimms

	double Cobb_Douglas( int n, double *a, double *c ) {
	  int i;
	  double CD = 1.0 ;

	  for ( i = 0; i < n; i++ )
	    CD = CD * pow(c[i],a[i]) ;

	  return CD;
	}

In the sequel it is assumed that this function is contained in a DLL
named ``"Userfunc.dll"``.

.. rubric:: Linking to AIMMS

In order to make the function available in AIMMS you have to declare an
``ExternalFunction`` ``CobbDouglasExternal``, which just relays its
execution to the ``C`` implementation of the Cobb-Douglas function
discussed above. The declaration of ``CobbDouglasExternal`` looks as
follows.

.. code-block:: aimms

	ExternalFunction CobbDouglasExternal {
	    Arguments     : (a,c);
	    Range         : nonnegative;
	    DLLName       : "Userfunc.dll";
	    ReturnType    : double;
	    BodyCall      : Cobb_Douglas( card : InputFactors, array: a, array: c );
	}

The arguments ``a`` and ``c`` must be declared in the same way as for
the internal ``CobbDouglas`` function discussed on
:ref:`examp:Cobb-Douglas`, with the exception that for the external
implementation we will also compute the Jacobian with respect to the
argument ``c(f)``. For this reason, the argument ``c(f)`` is declared as
a ``Variable``.

.. code-block:: aimms

	Set InputFactors {
	    Index        : f;
	}
	Parameter a {
	    IndexDomain  : f;
	}
	Variable c {
	    IndexDomain  : f;
	}

.. rubric:: Explanation

The translation type ``card`` of the set argument ``InputFactors``
causes AIMMS to pass the cardinality of the set as an integer value to
the external function ``Cobb_Douglas``. The translation type ``array``
of the arguments ``a`` and ``c`` are instructions to AIMMS to pass these
arguments as full arrays of double precision values. As function
arguments are always of type ``Input``, AIMMS will disregard any changes
made to the arguments by the external function. The ``double`` return
value of the ``C`` function ``Cobb_Douglas`` will become the result of
the function ``CobbDouglasExternal``.

.. rubric:: Calling external functions

After the declaration of an external function or procedure you can use
it as if it were an internal function or procedure. Thus, to call the
external function ``CobbDouglasExternal`` in the body of a procedure the
following statement suffices.

.. code-block:: aimms

	CobbDouglasValue := CobbDouglasExternal(a,c) ;

Of course, any two (possibly sliced) identifiers with single common
index domain could have been used as arguments. AIMMS will determine
this common index domain, and pass its cardinality to the external
function.

.. rubric:: Use in constraints

Unlike internal functions, external functions can be called inside
constraints. To accomplish this, the declaration has to be extended with
a ``DerivativeCall`` attribute. For this attribute you specify the
external call that has to be made when AIMMS also needs the partial
derivatives of all variable arguments inside constraints of mathematical
programs. In the absence of a ``DerivativeCall`` attribute, AIMMS will
use a differencing scheme to estimate these derivatives. The details of
using external functions in constraints, as well as the obvious
extension to compute the derivative of the Cobb-Douglas function
directly, are given in :ref:`sec:extern.constraints`.

.. rubric:: Setting up external libraries

Once you have developed a collection of external functions and
procedures, it may be a good idea to make this available in the form of
a library for use in AIMMS applications. In this way, the users of your
library do not have to spend any time translating their AIMMS arguments
into external arguments of the appropriate type in the external
procedure and function declarations.

.. rubric:: Save library as include file

To provide a library as an entity on its own, you can store all the
external procedures and functions in a separate model section, and save
this section as a source file. The functions and procedures in the
library can then be made available by simply including this source file
into a model.

.. rubric:: Hiding the interface

When you want to protect the interface to your external library, you can
accomplish this by encrypting the include file containing the function
library. Thus, the interface to the
external library becomes invisible, effectively preventing misuse of the
library outside AIMMS.