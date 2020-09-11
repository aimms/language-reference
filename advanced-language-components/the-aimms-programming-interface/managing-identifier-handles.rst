.. _sec:api.identifier:

Managing Identifier Handles
===========================

.. rubric:: Creation and data control

AIMMS offers the capability to dynamically create and delete handles to
any desired identifier slice over any desired local subdomain from
within a DLL. In addition, a subset of the AIMMS data control operators
(as discussed in :ref:`sec:data.control`) can be called from within
external DLLs. :numref:`table:api.identifier` lists all available AIMMS
API functions for creating handles and performing data control
operations.

.. _table:api.identifier:

.. table:: AIMMS API functions for handle management

   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierHandleCreate(char *name, int *domain, int *slicing, int flags, int *handle)``                           |
   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierHandleCreatePermuted(char *name, int *domain, int *slicing, int *permutation, int flags, int *handle)`` |
   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierHandleDelete(int handle)``                                                                              |
   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierEmpty(int handle)``                                                                                     |
   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierCleanup(int handle)``                                                                                   |
   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierUpdate(int handle)``                                                                                    |
   +------------------------------------------------------------------------------------------------------------------------------+
   | ``int AimmsIdentifierDataVersion(int handle, int *version)``                                                                 |
   +------------------------------------------------------------------------------------------------------------------------------+

.. rubric:: Creating a handle

You can use the function ``AimmsIdentifierHandleCreate`` to dynamically
create a handle to (a slice of) an AIMMS identifier or a suffix thereof
within an external function or procedure. You can restrict the scope of
a handle by

-  specifying a *call* domain to which you want to restrict the handle,
   or

-  by *slicing* one or more dimensions of the identifier.

.. rubric:: Obtaining a suffix

If you want a handle to an identifier itself, the name passed to
``AimmsIdentifierHandleCreate`` should just be the identifier name. If
you want a handle to a suffix of an identifier, you should pass the name
of the identifier followed by a dot and the suffix name. Thus, for
instance, you should pass the name ``"Transport.ReducedCost"`` if you
want a handle to the reduced costs of the variable ``Transport``.

.. rubric:: Specifying a call domain

When you want to create a handle over the full root domain, you can
simply pass a null pointer for the ``domain`` argument. If you want to
specify an additional call domain, you must pass an integer array of
length equal to the identifier's full dimension, each element containing
a handle to the set to which you want to restrict the domain. If the raw
flag is not set, passing a null pointer for the domain handle will
effectively restrict the declaration domain of the identifier at hand,
because of the semantics of the raw flag (see also
:ref:`sec:api.attribute` and :ref:`sec:api.value`).

.. rubric:: Specifying a slice

When you want to create a handle over the full dimension of an
identifier, you can simply pass a null pointer for the ``slicing``
argument. If you want to create a handle to a slice, you must pass an
integer array of length equal to the identifier's full dimension, each
element containing either a null element for all the domains that you do
not want to slice, or the element number of the element to which you
want to slice.

.. rubric:: Modification flags

With the ``flags`` argument in a call to ``AimmsIdentifierHandleCreate``
you can specify which modification flags should be set for the handle to
be created. The format of the ``flags`` argument is the same as in the
function ``AimmsAttributeFlags`` discussed in the previous section.

.. rubric:: Creating a permuted handle

With the function ``AimmsIdentifierHandleCreatePermuted`` you can obtain
a handle to a multidimensional identifier, for which the order in which
element tuples are returned is permuted. Handles created by
``AimmsIdentifierHandle CreatePermuted`` are always read-only,
i.e. cannot be used in the functions ``AimmsValueAssign`` and
``AimmsValueAssignMulti``. The ``permutation`` argument must be
specified according to the rules explained for the function
``AimmsAttributePermutation``.

.. rubric:: Example

Consider an identifier ``p(i,j,k,l)`` for which you want to retrieve the
values as if the identifier were defined as ``p(k,i,l,j)``. To retrieve
all values of ``p`` in this order, the ``permutation`` array must be
specified as ``[2,4,1,3]``.

.. rubric:: Deleting handles

With the function ``AimmsIdentifierHandleDelete`` you can delete a
dynamically created handle that is no longer needed. The function fails
when you try to delete a handle that was passed as an argument to the
DLL. After deletion the handle can no longer be used in conjunction with
any AIMMS API function.

.. rubric:: Empty, cleanup and update handles

The AIMMS API functions

-  ``AimmsIdentifierEmpty``,

-  ``AimmsIdentifierCleanup``, and

-  ``AimmsIdentifierUpdate``

can be called to perform the identical actions on a set or identifier
(slice) from within an external DLL as can be accomplished by the data
control operators ``EMPTY``, ``CLEANUP`` and ``UPDATE`` from within
AIMMS, respectively. The function ``AimmsIdentifierEmpty`` will empty
the particular slice and subdomain of the identifier associated with the
handle. The other two functions will cleanup or update the *entire* data
set of the identifier associated with the handle, regardless of the
specified slicing and local domain.

.. rubric:: Data version

For every identifier within your model AIMMS maintains a version number
of the data associated with the identifier. This number is incremented
each time a data value of the identifier has been changed. You can use
the function ``AimmsIdentifierDataVersion`` to retrieve this version
number, for instance, to verify whether the data has changed relative to
the last time you retrieved it.

.. rubric:: Checking for global data changes

When you apply the function ``AimmsIdentifierDataVersion`` to the
predefined handle value ``AIMMSAPI_MODEL_HANDLE``, AIMMS will return a
data version number based on the cases and datasets currently active
within the model. AIMMS will update this number as soon as the combined
configuration of the active case and/or datasets within the model has
changed, as well as after a call to the ``CLEANDEPENDENTS`` operator. A
change in this global data version number is a good indication that the
contents of all or a number of domain sets may have changed, and must be
retrieved again.