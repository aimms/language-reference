.. _sec:api.project:

Opening and Closing a Project
=============================

.. rubric:: Opening and closing a project

The AIMMS API functions in :ref:`this table <table:api.project>` allow you to open
and close an AIMMS project from within your own application.

.. _table:api.project:

.. table:: AIMMS API functions for opening and closing projects

   +----------------------------------------------------------------+
   | ``int AimmsProjectOpen(char *commandline, int *handle)``       |
   +----------------------------------------------------------------+
   | ``int AimmsServerProjectOpen(char *commandline, int *handle)`` |
   +----------------------------------------------------------------+
   | ``int AimmsProjectClose(int handle, int interactive)``         |
   +----------------------------------------------------------------+
   | ``int AimmsProjectWindow(HWND *window)``                       |
   +----------------------------------------------------------------+

.. rubric:: Opening a project

If you want to use AIMMS as an optimization engine from within an
external program, you can use the function ``AimmsProjectOpen`` to open
the AIMMS project which contains the model that you want to connect to.
To open an AIMMS project you must specify the command line containing
the project file name as well as any other command line options with
which you want to run AIMMS, *but without the name of the AIMMS
executable*. If the project is not in the current working directory, the
directory in which the project is contained must be appended to the
project file name. On success, you obtain a project handle which must be
used to close the project. Because a single AIMMS instance can only run
a single project, the function fails if a project is already running in
this AIMMS instance.

.. rubric:: Opening a server project

When you are running an AIMMS project as a server application, you do
not want windows or message boxes to appear on the server desktop under
any circumstances. Although you can open an AIMMS project in a minimized
or hidden fashion through commandline arguments passed to the
``AimmsProjectOpen`` function, AIMMS can still present some message
boxes, e.g. to report licensing problems during startup. With the
function ``AimmsServerProjectOpen`` you can open an AIMMS project
absolutely without any windowing support. If AIMMS encounters any
problems during startup, the function will fail and you can retrieve the
error message through the function ``AimmsAPILastError``.

.. rubric:: License required

When you open an AIMMS project from within your own application through
the AIMMS API, the normal AIMMS licensing arrangements apply. When no
valid AIMMS license is available on the host computer, a call to either
``AimmsProjectOpen`` or ``AimmsServerProjectOpen`` will fail.

.. rubric:: Closing a project

With the function ``AimmsProjectClose`` you can request AIMMS to close
the current project, and, subsequently, to terminate itself. With the
``interactive`` argument you can indicate whether the project must be
closed in an interactive manner (i.e. whether the user must be able to
answer any additional dialog box that may appear), or that the default
response is assumed. The request will fail if the project handle is not
equal to the project handle returned by the function
``AimmsProjectOpen``, thus disallowing you to close a project that was
not opened by yourself.

.. rubric:: ... and MainTermination();

.. rubric:: Obtaining the AIMMS window

Through the function ``AimmsProjectWindow`` you can obtain the ``Win32``
window handle associated with the current AIMMS project. You can use the
window handle in any ``Win32`` function call inside your DLL that
requires the AIMMS window handle to function properly.