.. _sec:api.procedure:

Executing AIMMS Procedures
==========================

.. rubric:: Running AIMMS procedures

The AIMMS API allows you to execute procedures contained in the AIMMS
model from within an external application. Both procedures with and
without arguments can be executed, and scalar output results can be
directly passed back to the external application.
:ref:`this table <table:api.execution>` lists the AIMMS API functions offered to
obtain procedure handles, to execute AIMMS procedures or to schedule
AIMMS procedures for later execution.

.. _table:api.execution:

.. table:: AIMMS API functions for execution requests

   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureHandleCreate(char *procedure, int *handle, int *nargs, int *argtype)``        |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureHandleDelete(int handle)``                                                    |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureRun(int handle, int *argtype, AimmsValue *arglist, int *result)``             |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureArgumentHandleCreate(int prochandle, int argnumber, int *arghandle)``         |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureAsyncRunCreate(int handle, int *argtype, AimmsValue *arglist, int *request)`` |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureAsyncRunDelete(int request)``                                                 |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsProcedureAsyncRunStatus(int request, int *status, int *result)``                       |
   +---------------------------------------------------------------------------------------------------+
   | ``int AimmsExecutionInterrupt(void)``                                                             |
   +---------------------------------------------------------------------------------------------------+

.. rubric:: Obtaining procedure handles

With the function ``AimmsProcedureHandleCreate`` you can obtain a handle
to a procedure with the given name within the model. In addition, AIMMS
will return the number of arguments of the procedure, as well as the
type of each argument. The possible argument types are:

-  one of the storage types *double*, *integer*, *binary* or *string*
   (discussed in :ref:`sec:api.attribute`) for scalar formal arguments,
   or

-  a *handle* for non-scalar formal arguments.

In addition to indicating the storage type of each argument, the
``argtype`` argument will also indicate whether an argument is input,
output, or input- output. Through the function
``AimmsProcedureHandleDelete`` you can delete procedure handles created
with ``AimmsProcedureHandleCreate``.

.. rubric:: Calling procedures

You can use the function ``AimmsProcedureRun`` to run the AIMMS
procedure associated with a given handle. If the AIMMS procedure has
arguments, then you have to provide these, together with their types,
through the ``arglist`` and ``argtype`` arguments. The (integer) return
value of the procedure (see also :ref:`proc.ret-val.decl` and
:ref:`proc.ret-val.use`) is returned through the ``result`` argument. If
AIMMS is already executing another procedure (started by another
thread), the call to ``AimmsProcedureRun`` blocks until the other
execution request has finished. :ref:`sec:api.control` explains how to
prevent this blocking behavior by obtaining exclusive control over
AIMMS.

.. rubric:: Passing arguments

For each argument of the AIMMS procedure you have to provide both the
type and value through the ``argtype`` and ``arglist`` arguments in the
call to ``AimmsProcedureRun``. You have the following possibilities.

-  If the argument is scalar, the argument type can be

   -  the storage type returned by the function
      ``AimmsProcedureHandleCreate``, in which case the argument value
      must be a pointer to a buffer of the indicated type containing the
      argument, or

   -  a handle, in which case the argument value must be a handle
      associated with a scalar AIMMS identifier (slice) that you want to
      pass.

-  If the argument is non-scalar, the argument type can only be a
   handle, and the argument value must be a handle corresponding to the
   identifier (slice) that you want to pass.

If you pass an argument as an identifier handle, this can either be a
handle to a global identifier defined within the model, or a local
argument handle obtained through a call to the function
``AimmsProcedureArgumentHandleCreate`` (see below).

.. rubric:: Output values

When the input-output type of one or more of the arguments is ``inout``
or ``output``, AIMMS will update the values associated with any handle
argument, or, if a buffer containing a scalar value was passed, fill the
buffer with the new value of the argument.

.. rubric:: Obtaining argument handles

Through the function ``AimmsProcedureArgumentHandleCreate`` you can
obtain a handle to the local arguments of procedures within your model.
After creating these handles you can pass them as arguments to the
function ``AimmsProcedureRun``. The following rules apply.

-  After creation, handles created by
   ``AimmsProcedureArgumentHandleCreate`` have no associated data.

-  If the handle corresponds to an ``Input`` argument of the procedure,
   you can supply data prior to calling the procedure, and AIMMS will
   empty the handle after the execution of the procedure has completed.

-  If the handle corresponds to an ``InOut`` or ``Output`` argument of
   the procedure, AIMMS will not empty the handle after completion of
   the procedure. If you want to supply data to a handle corresponding
   to an ``InOut`` argument in subsequent calls, you have to make sure
   to empty the handle (through the function ``AimmsIdentifierEmpty``)
   prior to supplying the input data.

.. rubric:: Requesting asynchronous execution

With the function ``AimmsProcedureAsyncRunCreate`` you can request
asynchronous execution of a particular AIMMS procedure. The function
returns an integer request handle for further reference. AIMMS will
execute a requested procedure as soon as there are no other execution
requests currently being executed or waiting to be executed. *Note that
you should make sure that the ``AimmsValue`` array passed to AIMMS stays
alive during the asynchronous execution of the procedure.* Failure to do
so, may result in illegal memory references during the actual execution
of the AIMMS procedure. This is especially true when the array contains
references to scalar integer, double or string ``InOut`` or ``Output``
buffers within your application to be filled by the AIMMS procedure.

.. rubric:: Obtaining the status

Through the function ``AimmsProcedureAsyncRunStatus`` you can obtain the
status of an outstanding asynchronous execution request. The status of
such a request can be

-  pending,

-  running,

-  finished,

-  deleted, or

-  unknown (for an invalid request handle).

When the request is in the finished state, the return value of the AIMMS
procedure will be returned via the ``result`` argument.

.. rubric:: Deleting a request

You should make sure to delete all asynchronous execution handles
requested during a session using the function
``AimmsProcedureAsyncRunDelete``. *Failure to delete all finished
requests may result in a serious memory leak if your external DLL
generates many small asynchronous execution requests.* If you delete a
pending request, AIMMS will remove the request from the current
execution queue. The function will fail if you try to delete a request
that is currently being executed.

.. rubric:: Interrupting an existing run

When an AIMMS procedure has been started by a separate thread in your
program you can interrupt it using the function
``AimmsExecutionInterrupt``. This function returns ``AIMMSAPI_SUCCESS``
when AIMMS was idle and ``AIMMSAPI_FAILURE`` was executing a procedure.