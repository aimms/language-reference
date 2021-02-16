.. _sec:api.error.handling:

Raising and Handling Errors
===========================

.. rubric:: Raising and handling errors

The error passing described in the previous section is retained in AIMMS
3 in order not to break existing applications. The use of the error
handling described in this section, however, is encouraged as it is more
in line with the error handling framework described in
:ref:`sec:exec.error`. In addition, all errors, including all their
parts, can be retrieved. The AIMMS API functions in
:ref:`this table <table:api.handle.error>` enable the raising and handling of
errors and retrieving the current AIMMS status.

.. _table:api.handle.error:

.. table:: AIMMS Raising and handling errors in the AIMMS API

   +------------------------------------------------------------------+
   | ``int AimmsErrorStatus(void)``                                   |
   +------------------------------------------------------------------+
   | ``int AimmsErrorCount(void)``                                    |
   +------------------------------------------------------------------+
   | ``char *AimmsErrorMessage(int errNo)``                           |
   +------------------------------------------------------------------+
   | ``int AimmsErrorSeverity(int errNo)``                            |
   +------------------------------------------------------------------+
   | ``char *AimmsErrorCode(int errNo)``                              |
   +------------------------------------------------------------------+
   | ``char *AimmsErrorCategory(int errNo)``                          |
   +------------------------------------------------------------------+
   | ``int AimmsErrorNumberOfLocations(int errNo)``                   |
   +------------------------------------------------------------------+
   | ``char *AimmsErrorFilename(int errNo)``                          |
   +------------------------------------------------------------------+
   | ``char *AimmsErrorNode(int errNo, int pos)``                     |
   +------------------------------------------------------------------+
   | ``char *AimmsErrorAttributeName(int errNo, int pos)``            |
   +------------------------------------------------------------------+
   | ``int AimmsErrorLine(int errNo, int pos)``                       |
   +------------------------------------------------------------------+
   | ``int AimmsErrorColumn(int errNo)``                              |
   +------------------------------------------------------------------+
   | ``time_t AimmsErrorCreationTime(int errNo)``                     |
   +------------------------------------------------------------------+
   | ``int AimmsErrorDelete(int errNo)``                              |
   +------------------------------------------------------------------+
   | ``int AimmsErrorClear(void)``                                    |
   +------------------------------------------------------------------+
   | ``int AimmsErrorRaise(int severity, char *message, char *code)`` |
   +------------------------------------------------------------------+

.. rubric:: Global error collector manipulation

The functions ``AimmsErrorStatus``, ``AimmsErrorCount``,
``AimmsErrorGet``, ``AimmsErrorDelete`` and ``AimmsErrorClear`` all
manipulate the global error collector. The global error collector is
described in :ref:`sec:exec.error`. The function ``AimmsErrorStatus``
scans the contents of the global error collector and returns

``AIMMSAPI_SEVERITY_CODE_NEVER``
   if the global error collector is empty,

``AIMMSAPI_SEVERITY_CODE_WARNING``
   if it contains only warnings, or

``AIMMSAPI_SEVERITY_CODE_ERROR``
   if it contains at least one error.

The function ``AimmsErrorCount`` does not return a status code, instead
it directly returns the number of errors and warnings in the global
error collector. With the functions ``AimmsErrorMessage``,
``AimmsErrorSeverity``, ``AimmsErrorCategory``, ``AimmsErrorCode``,
``AimmsErrorNumberOfLocations``, ``AimmsErrorLine``, ``AimmsErrorNode``,
``AimmsErrorAttributeName``, ``AimmsErrorFilename``,
``AimmsErrorColumn``, and ``AimmsErrorCreationTime`` actual error
information is obtained. In these functions the ``errNo`` argument
should be in the range {1..\ ``AimmsErrorCount()``} and the ``pos``
argument should be in the range
{1..\ ``AimmsErrorNumberOfLocations(errNo)``}.

.. rubric:: Example for API calls

None of the AIMMS API functions throws an exception, nor do any of them
let an exception pass through. The example below serves as a simple
template to call ``AimmsProcedureRun`` and handle all errors occurring
during that execution run.

.. code-block:: c

	int ErrCount, errNo, apr_stat ;

	apr_stat = AimmsProcedureRun( procHandle, ... );
	ErrCount = AimmsErrorCount();
	if ( ErrCount ) {
	    for ( errNo = 1 ; errNo <= ErrCount ; errNo ++ ) {

	        // Handle the error; replace the next line as 
	        // appropriate for the application at hand.
	        printf( "Error %d: %s\n", errNo, AimmsErrorMessage(errNo) );

	    }
	    AimmsErrorClear();
	} else if ( apr_stat == AIMMSAPI_FAILURE ) {
	    printf("Aimms failed for an unknown reason.\n");
	}

.. rubric:: Raising an error

The function ``AimmsErrorRaise(severity, message, code)`` can raise
errors and warnings. These errors will be handled by the currently
active error handler as described in :ref:`sec:exec.error`. If there is
no currently active error handler, the error is directly placed in the
global error collector. The call to this function is similar to the
``RAISE`` statement, see :ref:`sec:exec.error.raising`. The ``code``
argument is optional. The ``severity`` argument should be either

``AIMMSAPI_SEVERITY_CODE_WARNING``
   indicating a warning or

``AIMMSAPI_SEVERITY_CODE_ERROR``
   indicating an error.

The category of an error raised by ``AimmsErrorRaise`` is fixed to
``'User'``.