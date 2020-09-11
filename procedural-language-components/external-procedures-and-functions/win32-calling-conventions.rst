.. _sec:extern.win32:

``Win32`` Calling Conventions
=============================

.. rubric:: ``Win32`` calling conventions

The 32-bit Windows environment (``Win32``) supports several calling
conventions that influence the precise manner in which arguments are
passed to a function, and how the return value must be retrieved. When
calling an external function or procedure in this environment, AIMMS
will *always* assume the ``WINAPI`` calling convention. The following
macro in ``C`` makes sure that the ``WINAPI`` calling convention is
used. That same macro also makes sure that the function or procedure is
automatically exported from the DLL.

.. code-block:: aimms

	#include <windows.h>
	#define DLL_EXPORT(type) __declspec(dllexport) type WINAPI

You can add this macro to the implementation of any function that you
want to call from within AIMMS, as illustrated below.

.. code-block:: aimms

	DLL_EXPORT(double) Cobb_Douglas( int n, double *a, double *c )
	{
	    /* Implementation of Cobb_Douglas goes here */
	}

.. rubric:: Prevent ++ name mangling

By default, ++ compilers will perform a process referred to as *name
mangling*, modifying each function name in your source code according to
its prototype. By doing this, ++ is able to deal with the same function
name defined for different argument types. If you want to export a DLL
function to AIMMS, however, you must prevent name mangling to take
place, ensuring that AIMMS can find the exported function name within
the DLL. You can do this by declaring the prototype of the function
using the following macro, which accounts for both ``C`` and ++.

.. code-block:: aimms

	#ifdef __cplusplus
	#define DLL_EXPORT_PROTO(type) extern "C" __declspec(dllexport) type WINAPI
	#else
	#define DLL_EXPORT_PROTO(type) extern __declspec(dllexport) type WINAPI
	#endif

Thus, to make sure that a ++ implementation of ``Cobb_Douglas`` is
exported without name mangling, declare its prototype as follows before
providing the function implementation.

.. code-block:: aimms

	DLL_EXPORT_PROTO(double) Cobb_Douglas( int n, double *a, double *c );

Function declarations like this are usually stored in a separate header
file. Note that along with this prototype declaration, you must still
use the ``DLL_EXPORT`` macro in the implementation of ``Cobb_Douglas``.

.. rubric:: DLL initialization

When your external DLL requires initialization statements to be executed
when the DLL is loaded, or requires the execution of some cleanup
statements when the DLL is closed, you can accomplish this by adding a
function ``DllMain`` to your DLL. When the linker finds a function named
``DllMain`` in your DLL, it will execute this function when opening and
closing the DLL. The following example provides a skeleton ``DllMain``
implementation which you can directly copy into your DLL source code.

.. code-block:: aimms

	#include <windows.h>

	BOOL WINAPI DllMain(HINSTANCE hdll, DWORD reason, LPVOID reserved)
	{
	    switch( reason ) {
	       case DLL_THREAD_ATTACH:
	           break;
	       case DLL_PROCESS_ATTACH:
	           /* Your DLL initialization code goes here */
	           break;
	       case DLL_THREAD_DETACH:
	           break;
	       case DLL_PROCESS_DETACH:
	           /* Your DLL exit code goes here */
	           break;
	    }
	    return 1; /* Return 0 in case of an error */
	}

To prevent name mangling to take place, you can best declare the
function ``DllMain`` as follows.

.. code-block:: aimms

	#ifdef __cplusplus
	extern "C" BOOL WINAPI DllMain(HINSTANCE hdll, DWORD reason, LPVOID reserved);
	#else
	BOOL WINAPI DllMain(HINSTANCE hdll, DWORD reason, LPVOID reserved);
	#endif