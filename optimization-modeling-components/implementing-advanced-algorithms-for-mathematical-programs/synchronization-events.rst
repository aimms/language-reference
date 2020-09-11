.. _sec:gmp.event:

Synchronization Events
======================

.. rubric:: Events for synchronization

To allow for more advanced thread synchronization during parallel
solves, AIMMS offers synchronization objects called *events*, which can
be manipulated using the function listed in :numref:`table:gmp.event`.

.. _GMP::Event::Reset-LR:

.. _GMP::Event::Set-LR:

.. _GMP::Event::Delete-LR:

.. _GMP::Event::Create-LR:

.. _table:gmp.event:

.. table:: 

	+----------------------------------------------------+
	| ``Create``\ (*name*) →         :any:`AllGMPEvents` |
	+----------------------------------------------------+
	| ``Delete``\ (*event*)                              |
	+----------------------------------------------------+
	| ``Set``\ (*event*)                                 |
	+----------------------------------------------------+
	| ``Reset``\ (*event*)                               |
	+----------------------------------------------------+
	
.. rubric:: Creating events

Through the function :any:`GMP::Event::Create` you can create a new event,
while the function :any:`GMP::Event::Delete` deletes existing events. Using
the function :any:`GMP::Event::Set` you can notify AIMMS that an event has
occurred. The function :any:`GMP::Event::Reset` resets the event.

.. rubric:: Waiting for events

Events are elements of the predefined set :any:`AllGMPEvents`, which, along
with the set :any:`AllSolverSessions`, is a subset of the predefined set
:any:`AllSolverSessionCompletionObjects`. As both the functions

-  :any:`GMP::SolverSession::WaitForCompletion`, and

-  :any:`GMP::SolverSession::WaitForSingleCompletion`

expect a subset of the set :any:`AllSolverSessionCompletionObjects` as
their arguments, these functions can be used to wait for both solver
session completion and the occurrence of events.

.. rubric:: Using events

You can use events, for example, to notify the main thread of execution
in your model that you want a new mathematical program instance to be
generated and solved asynchronously based on input data provided by a
solver callback. AIMMS does not allow asynchronous solves to be started
from within a callback itself.