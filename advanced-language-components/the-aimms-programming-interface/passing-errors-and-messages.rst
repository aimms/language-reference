.. _sec:api.status:

Passing Errors and Messages
===========================

.. rubric:: Passing errors and messages

The AIMMS API functions in :numref:`table:api.error` let you send error
and warning messages to AIMMS and get the current AIMMS status. In
addition, you can obtain the error number and description of the last
AIMMS API error.

.. _table:api.error:

.. table:: AIMMS API functions for error messages

   +----------------------------------------------------------+
   | ``int AimmsAPIPassMessage(int severity, char *message)`` |
   +==========================================================+
   | ``int AimmsAPIStatus(int *status)``                      |
   +----------------------------------------------------------+
   | ``int AimmsAPILastError(int *code, char *message)``      |
   +----------------------------------------------------------+

.. rubric:: Passing errors and messages

With the function ``AimmsAPIPassMessage`` you can send error and warning
messages to the end-user of your DLL in AIMMS. Such errors and warnings
are displayed to the end-user in the AIMMS message window. For every
message you must indicate a severity code, the complete list of which is
included in the ``aimmsapi.h`` header file. When AIMMS receives a
message with error severity, a run-time error is generated. The end-user
of an application can set execution options to filter out those warning
messages which are below a certain severity threshold.

.. rubric:: Setting :any:`CurrentErrorMessage`

If a function in your DLL is called from within an AIMMS project, and
you want to pass back an error message to the model without
automatically opening the AIMMS message window, you should not use the
function ``AimmsAPIPassMessage``, but instead assign the message to the
predefined AIMMS string parameter :any:`CurrentErrorMessage`. To assign a
value to it, you should create a handle to it via the function
``AimmsIdentifierHandleCreate`` and assign the message using the
function ``AimmsValueAssign``. It is then up to the model developer
calling your function, whether the message stored in
:any:`CurrentErrorMessage` should be displayed (e.g. in the AIMMS message
window).

.. rubric:: Obtaining the execution status

Through the function ``AimmsAPIStatus`` you can obtain the current
status of the AIMMS execution engine, such as executing, solving, ready,
etc. The complete list of possible status codes and their meaning is
included in the ``aimmsapi.h`` header file.

.. rubric:: Obtaining API errors

Whenever a call to an AIMMS API function fails, the function returns
``AIMMSAPI_FAILURE`` as its return value. In such a case, you can obtain
the precise error code and a message describing the error through the
function ``AimmsAPILastError``. The complete list of error codes is
contained in the ``aimmsapi.h`` header file. By modifying the
API-related execution options, you can also enforce that every API error
is listed in the AIMMS message window.