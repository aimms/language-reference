.. _sec:api.control:

Thread Synchronization
======================

.. rubric:: Multiple threads

The AIMMS API allows multiple DLLs to be active within the context of a
single project. While some of these DLLs may only be useful when called
from within your AIMMS project itself, you may want other DLLs to run
independently in a separate thread of execution. Such behavior may be
necessary, for instance, when

-  you want to link AIMMS to an online data source, where an independent
   DLL collects the online data and passes it on to AIMMS whenever
   appropriate, or

-  you want to call AIMMS as an independent optimization engine from
   within your own program and need to pass data to AIMMS whenever
   necessary.

.. rubric:: AIMMS thread

When you open an AIMMS project by calling the function
``AimmsProjectOpen`` from within your own application, AIMMS will create
a new thread. This AIMMS thread will deal with

-  all end-user interaction initiated from within the AIMMS end-user
   interface (which is created as part of opening the project), and

-  all asynchronous execution requests that are initiated either from
   within your application, another external DLL linked to your AIMMS
   project, or from within the model itself.

.. rubric:: Thread initialization

Whenever you want to call AIMMS API functions from within a thread
started by yourself, you must make sure that the thread is well-equipped
to do so by calling the AIMMS thread (un)initialization functions listed
in :ref:`this table <table:api.thread-initialization>`.

.. _table:api.thread-initialization:

.. table:: AIMMS API functions for thread initialization

   +---------------------------------+
   | ``int AimmsThreadAttach(void)`` |
   +---------------------------------+
   | ``int AimmsThreadDetach(void)`` |
   +---------------------------------+

.. rubric:: Initializing threads...

Prior to calling any other AIMMS API function from within a newly
created thread, you should call the function ``AimmsThreadAttach``. It
will make sure that any thread-specific initialization required for
calling the AIMMS execution engine is performed properly. Similarly, you
should call the function ``AimmsThreadDetach`` just prior to exiting the
thread.

.. rubric:: ... includes COM initialization

Among others, a call to ``AimmsThreadAttach`` will initialize the
Microsoft COM library in a manner compatible with the COM apartment
model employed by AIMMS. Therefore, if you are using COM interfaces
within your thread, you should not call the COM SDK functions
``CoInitialize`` (or ``CoInitializeEx``) and ``CoUninitialize`` directly
to initialize the COM library, but rather call ``AimmsThreadAttach`` and
``AimmsThreadDetach``.

.. rubric:: Thread synchronization

Whenever an AIMMS project runs in a multi-threaded environment,
synchronization of the execution and data retrieval requests becomes of
the utmost importance. By default, AIMMS will make sure that no two
execution or data retrieval requests initiated from different threads
are dealt with simultaneously. However, this default synchronization
scheme does not preclude that the execution of two subsequent requests
from one thread is interrupted by a request from another thread.

.. rubric:: Obtaining exclusive control

When the proper functioning of your application requires that your
execution and data retrieval requests to AIMMS are not interrupted by
requests from competing threads, you can use the functions listed in
:ref:`this table <table:api.control>` to obtain exclusive control over the AIMMS
execution engine.

.. _table:api.control:

.. table:: AIMMS API functions for obtaining exclusive control

   +--------------------------------------+
   | ``int AimmsControlGet(int timeout)`` |
   +--------------------------------------+
   | ``int AimmsControlRelease(void)``    |
   +--------------------------------------+

.. rubric:: Obtaining and releasing control

With the function ``AimmsControlGet`` you can restrict control over the
current AIMMS session exclusively to the thread calling
``AimmsControlGet``. Execution and data retrieval requests from any
thread other than this controlling thread (including the AIMMS thread
itself) will block until the controlling thread has released the
control. The function ``AimmsControlRelease`` releases the exclusive
control over the AIMMS session. *Note that every successful call to
``AimmsControlGet`` must be followed by a corresponding call to
``AimmsControlRelease``*, or AIMMS will be inaccessible to all other
threads for the remainder of the session. ``AimmsControlRelease`` fails
when the calling thread does not have exclusive control.

.. rubric:: Waiting for the control

When another thread has exclusive control over AIMMS, either obtained
explicitly through a call to ``AimmsControlGet`` or implicitly through
an execution or data retrieval request, the function ``AimmsControlGet``
will block *timeout* milliseconds before returning with a failure. By
choosing a *timeout* of ``WAIT_INFINITE``, the function
``AimmsControlGet`` will block until it gets exclusive control.

.. rubric:: Nonblocking execution

If you want to make sure that a subsequent execution request will never
block, you can

-  call ``AimmsControlGet`` with a timeout of 0 milliseconds,

-  perform the execution request when successful, and

-  subsequently release the control.

The call to ``AimmsControlGet`` has the effect of verifying that no
other thread is using AIMMS at the moment. If you cannot get exclusive
control, you must store the request for later execution.