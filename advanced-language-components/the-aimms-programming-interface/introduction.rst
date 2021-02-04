.. _sec:api.intro:

Introduction
============

.. rubric:: Communication scenario's

One can think of several scenario's in which a path of communication
needs to be set up between AIMMS and an external software component. The
two most common scenario's are listed below.

-  You have a collection of functions within an external DLL which you
   want to use to perform certain data manipulations within your AIMMS
   model through calls to an ``ExternalProcedure`` or
   ``ExternalFunction``.

-  From within your own application you want to open an AIMMS project,
   pass input data to it, solve an optimization model, and retrieve the
   solution.

.. rubric:: Exchanging data

The most straightforward method to set up communication between AIMMS
and an external DLL is by calling an external procedure or function from
within your model. If, during such a call, the data of one or more
scalar or low-dimensional indexed identifiers need to be passed to the
DLL, the easiest way to exchange this data is by passing either a single
scalar value or a (dense) array of scalar values as arguments to the
corresponding DLL function. For higher- dimensional identifiers,
however, the memory requirements for passing array arguments may grow
out of hand, and additional control may be needed.

.. rubric:: Application-controlled execution

With only the possibility to call external procedures and functions from
within an AIMMS model, however, you have no possibility, from within an
external application, to

-  open an AIMMS project,

-  initiate the exchange of data, or

-  execute one or more procedures in your model.

.. rubric:: The AIMMS API

The AIMMS Application Programming Interface (API) described in this
chapter addresses both the drawbacks associated with dense data
transfer, and the need to control the execution of an AIMMS model from
within an external application. :numref:`fig:api.overview` provides a
schematic overview of the capabilities to communicate using both the
concept of external procedures and functions and the AIMMS API.

.. figure:: introduction-pspic1.svg
   :name: fig:api.overview

   Interaction between AIMMS and an external DLL

Left-to-right arrows are implemented through external procedure and
function calls within your model, while all right-to-left arrows are
provided for by the AIMMS API.

.. rubric:: Handles

Central to the AIMMS API is the concept of *handles*. Handles are
represented by unique integer numbers, and provide indirect access to
named identifiers and procedures within an AIMMS model. Access to the
associated objects within the model is through the functions of the API.
With every identifier or procedure in the model, multiple handles can be
associated, each of which may behave differently when passed to a
function in the AIMMS API depending on its declaration or on the
sequency of API functions previously applied to it (e.g. during sparse
data retrieval). Handles can be created by AIMMS and passed as arguments
to a DLL function, or can be created from within an external
application.

.. rubric:: API functions

Through the functions in the AIMMS API, you can initiate further actions
on a given identifier or procedure handle from within an external
application. More specifically, the API functions allow you to

-  obtain information about identifiers in the model, such as domain,
   range and type,

-  set up sparse data communication between an identifier in the AIMMS
   model and an external application, and

-  request either synchronous or asynchronous execution of a procedure
   within the AIMMS model.

.. rubric:: ``C`` interface

AIMMS only provides a ``C`` interface to the functions in its API. When
you are using a different language which requires a different interface,
you should implement the required interface yourself in ``C++`` or in a
compatible language.

.. rubric:: Single example

This remainder of this section will provide you with a simple
``ExternalProcedure`` declaration and the associated ``C`` function that
illustrates the basic use of the AIMMS API and further familiarizes you
with the basic concepts. Because of the many API functions and their
interdependence, it is practically impossible to provide illustrative
examples for each API function separately in the context of the this
language reference. Therefore, the subsequent sections will only explain
the semantics of each separate API function.

.. rubric:: Example: printing identifier info

The following ``C`` function accepts the name of an AIMMS identifier
with double-valued values. It queries AIMMS for a handle to that
identifier, the corresponding domain and all associated values. For the
sake of conciseness, the DLL function does not check all return values
passed by the AIMMS API functions.

.. code-block:: c

	#include <stdio.h> 
	#include <string.h> 
	#include <aimmsapi.h>

	DLL_EXPORT(void) print_double_aimms_identifier_info(char *name) {
	   int  handle, full, sliced, domain[AIMMSAPI_MAX_DIMENSION],
	        tuple[AIMMSAPI_MAX_DIMENSION], storage, i;
	   char file[256], buffer[256];
	   FILE *f;

	   AimmsValue  value;
	   AimmsString strvalue;

	   /* Create a handle associated with the identifier name passed */
	   AimmsIdentifierHandleCreate(name, NULL, NULL, 0, &handle);

	   /* Get the dimension, domain and storage type of the identifier
	      associated with the handle */
	   AimmsAttributeDimension (handle, &full, &sliced);
	   AimmsAttributeRootDomain(handle, domain);
	   AimmsAttributeStorage   (handle, &storage);

	   if ( storage != AIMMSAPI_STORAGE_DOUBLE ) return;

	   /* Open a file consisting of the identifier name with the extension .def,
	      and print the identifier's name and dimension */

	   strcpy(file, name); strcat(file, ".def");
	   if ( ! (f = fopen(file, "w")) ) return;
	   fprintf(f, "Identifier name: %s\n", name);
	   fprintf(f, "Dimension      : %d\n", full);

	   /* Prepare strvalue to hold the locally declared buffer */
	   strvalue.String = buffer;

	   /* Print a header containing the names of the domain sets */
	   fprintf(f, "\nData values    : \n");
	   for ( i = 0; i < full; i++ ) {
	       strvalue.Length = 256;
	       AimmsAttributeName(domain[i], &strvalue); fprintf(f, "%17s", buffer);
	   }
	   fprintf(f,"%16s\n","Double value");
	   for ( i = 0; i < full; i++ ) fprintf(f, "%17s", "----------------");
	   fprintf(f,"\n");

	   /* Print all tuples with nondefault data values */
	   AimmsValueResetHandle(handle);
	   while ( AimmsValueNext(handle, tuple, &value) ) {
	       for ( i = 0; i < full; i++ ) {
	           strvalue.Length = 256;
	           AimmsSetElementToName(domain[i], tuple[i], &strvalue);
	           fprintf(f,"%17s", buffer);
	       }
	       fprintf(f,"%17.5f\n", value.Double);
	   }

	   fclose(f);
	}

If the DLL function is part of a DLL ``"Userfunc.dll"``, then it can be
called from within AIMMS by the following ``ExternalProcedure``
declaration.

.. code-block:: aimms

	ExternalProcedure PrintParameterInfo {
	    Arguments  : (param);
	    DLLName    : "Userfunc.dll";
	    BodyCall   : print_double_aimms_identifier_info(string scalar: param);
	}

Its only argument is an element parameter into the predefined set
:any:`AllIdentifiers`. It can therefore be called with any identifier name.

.. code-block:: aimms

	ElementParameter param {
	    Range      : AllIdentifiers;
	    Property   : input;
	}

.. rubric:: Call example

Consider a two-dimensional parameter ``TransportCost(i,j)`` which
contains the following data.

.. code-block:: aimms

	TransportCost := DATA TABLE
	                Rotterdam       Antwerp         Berlin
	!               ---------       ---------       ---------
	Amsterdam        1.00            2.50           10.00
	Rotterdam                        1.20           10.00
	Antwerp                                         11.00
	;

Then the procedure call ``PrintParameterInfo('TransportCost')`` will
result in the creation of a file ``TransportCost.def`` with the
following contents.

.. code-block:: none

	Identifier name: TransportCost
	Dimension      : 2

	Data values    :
	Cities            Cities           Double value
	----------------- ---------------- ---------------
	Amsterdam         Rotterdam                1.00000
	Amsterdam         Antwerp                  2.50000
	Amsterdam         Berlin                  10.00000
	Rotterdam         Antwerp                  1.20000
	Rotterdam         Berlin                  10.00000
	Antwerp           Berlin                  11.00000

.. rubric:: ``aimmsapi.h`` header file

The prototypes of all the available AIMMS API functions, as well as all
``C`` macro definitions that are relevant for the execution of the API
functions are provided in a single header file ``aimmsapi.h``. You
should include this header file in all your source files that make use
of the AIMMS API functions.

.. rubric:: Two flavors of API

The AIMMS API functions are provided in two flavors: ASCII and Unicode.
For each of the functions mentioned in this chapter, there is an
implementation postfixed with ``A`` for the ASCII flavor, and an
implementation postfixed with ``W`` for the Unicode flavor. For
instance, when ``UNICODE`` is defined, a call to
``AimmsIdentifierHandleCreate`` will be mapped to the implemented
function ``AimmsIdentifierHandleCreateW``. For the Unicode flavor, on
Windows, double-byte character arrays are used to communicate strings
corresponding to the UTF-16LE character encoding. For the Unicode
flavor, on Linux, quadruple-byte character arrays are used to
communicate strings corresponding to the UTF-32LE character encoding.
This corresponds to the ``wchar_t*`` type on both platforms. Please make
sure that the option ``external_string_character_encoding`` is set to
corresponding encoding. For the ASCII flavor, both on Windows and on
Linux, multibyte character arrays are used, and the encoding is
determined by the option ``external_string_character_encoding``.

.. rubric:: ``libaimms3.lib`` import library

The AIMMS API functions are provided in the form of a Visual ``C``/C++
import library ``libaimms3.lib`` to the ``libaimms3.dll`` DLL, which can
be included in the link step of your external AIMMS DLL. When you are
using the Visual ``C``/C++ compiler, this import library will take care
that all the relevant API functions are imported from the AIMMS
executable when your AIMMS application loads the external DLL. For other
compilers, you should consult the compiler documentation on how to
import the functions in ``libaimms3.dll`` into your program.

.. rubric:: Return values

All AIMMS API functions provide an integer return value. When the
requested operation has succeeded, the value ``AIMMSAPI_SUCCESS`` is
returned. When the operation has failed, AIMMS will return the value
``AIMMSAPI_FAILURE``. In the latter case, you can obtain an error code
and string through the API function ``AimmsAPILastError`` (see also
:ref:`sec:api.status`).

.. rubric:: Only identifiers with data

AIMMS will only allow you to pass or create handles for identifier types
with which data is associated, i.e. sets, parameters and variables. In
addition, you can pass or create handles to suffices of identifiers as
long as the resulting suffix results in a set or parameter.
