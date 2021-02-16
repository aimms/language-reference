.. _sec:api.interrupt:

Interrupts
==========

.. rubric:: Interrupts

During the execution of a procedure in your model, the AIMMS thread will
block. This effectively prevents you from interrupting the AIMMS
execution, for instance, to update data in the model, or just to abort
the current procedure execution. Likewise, while a function in your DLL
that was executed from within an AIMMS procedure is still running, AIMMS
cannot service any end-user requests. The functions listed in this
section allow your DLL and AIMMS to work together in a cooperative
manner in such situations.

.. rubric:: Handling interrupts

You can use the functions listed in :ref:`this table <table:api.interrupt>` to
handle two-way interrupts.

.. _table:api.interrupt:

.. table:: AIMMS API functions for handling interrupts

   +------------------------------------------------------------------+
   | ``int AimmsInterruptCallbackInstall(AimmsInterruptCallback cb)`` |
   +------------------------------------------------------------------+
   | ``int AimmsInterruptPending(void)``                              |
   +------------------------------------------------------------------+

.. rubric:: Installing a callback

With the function ``AimmsInterruptCallbackInstall`` you can pass a
function pointer with a prescribed prototype to AIMMS, which AIMMS will
call on a regular basis during subsequent execution of an AIMMS
procedure. Note that the installed callback is *thread-local*, i.e.,
AIMMS will only call the callback procedure from within an AIMMS
procedure that is executing in the same thread in which you called
``AimmsInterruptCallbackInstall`` to install the callback.

.. rubric:: Within a callback

Within a callback function AIMMS allows you to request or modify model
data, or to run model procedures, which would normally be prohibited
because calls to the AIMMS API block when AIMMS is executing (see also
:ref:`sec:api.control`). Through the argument of the callback function
AIMMS passes its current state (just executing, or within a solve),
while you can indicate, through the return value of the callback
function, whether you

-  want to interrupt the current solve but continue the remainder of the
   current execution,

-  want to interrupt the current execution all together, or

-  do not want to interrupt the current execution at all.

Because AIMMS will call a callback procedure quite regularly, it is
advisory to keep the actions executed within it to a minimum, or AIMMS
could be slowed down unacceptably.

.. rubric:: Uninstalling the callback

You can uninstall a previously installed callback function by simply
calling the function ``AimmsInterruptCallbackInstall`` with a null
pointer as the callback function argument. Note that it is even possible
to uninstall a callback function-or modify a callback function-during a
call (by AIMMS) to the currently installed callback function.

.. rubric:: Pending interrupts

When AIMMS calls a function within an external DLL, this would normally
prevent AIMMS from servicing end-user requests to update end-user pages,
modify model data, or even to interrupt the execution of the current
AIMMS execution, i.e. the execution of your function. This is not a
problem when a call to your function only takes a small amount of time
to execute, but might be unacceptable when your function takes a long
time to complete. In such situations, you might consider to insert calls
to the function ``AimmsInterruptPending`` at strategic places in your
source code. With it, you allow AIMMS to service such requests, and to
call any callback functions installed by other DLLs. On return,
``AimmsInterruptPending`` returns

-  ``AIMMSAPI_TRUE`` when AIMMS received a request to interrupt the
   current execution, or

-  ``AIMMSAPI_FALSE`` when there was no interrupt request.

When an interrupt was requested you should abort the execution of your
external function as soon as possible.