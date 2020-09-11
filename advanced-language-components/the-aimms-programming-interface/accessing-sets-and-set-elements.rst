.. _sec:api.set:

Accessing Sets and Set Elements
===============================

.. rubric:: Accessing sets

The AIMMS API functions discussed in the previous section allow you to
retrieve and assign individual values of (slices of) indexed identifiers
associated with tuples of set element numbers used by AIMMS internally.
The AIMMS API functions discussed in this section allow you to add
elements to simple sets, and let you convert element numbers into
ordinal numbers and element names, or vice versa.
:numref:`table:api.set` presents all set related API functions.

.. _table:api.set:

.. table:: AIMMS API functions for passing set data

   +----------------------------------------------------------------------------------+
   | ``int AimmsSetAddElement(int handle, char *name, int *element)``                 |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetAddElementMulti(int handle, int n, int *elementNumbers)``          |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetAddElementRecursive(int handle, char *name, int *element)``        |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetRenameElement(int handle, int element, char *name)``               |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetDeleteElement(int handle, int element)``                           |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetElementNumber(int handle, char *name, int allowCreate,``           |
   +----------------------------------------------------------------------------------+
   | ``int *elementNumber, int *isCreated)``                                          |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetAddElementMulti(int handle, int n, int *elementNumbers)``          |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetAddElementRecursiveMulti(int handle, int n, int *elementNumbers)`` |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetElementToOrdinal(int handle, int element, int *ordinal)``          |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetElementToName(int handle, int element, AimmsString *name)``        |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetOrdinalToElement(int handle, int ordinal, int *element)``          |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetOrdinalToName(int handle, int ordinal, AimmsString *name)``        |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetNameToElement(int handle, char *name, int *element)``              |
   +----------------------------------------------------------------------------------+
   | ``int AimmsSetNameToOrdinal(int handle, char *name, int *ordinal)``              |
   +----------------------------------------------------------------------------------+

.. rubric:: Adding elements to simple sets

The function ``AimmsSetAddElement`` allows you to add new element names
to a simple set. AIMMS will return with the internal element number
assigned to the element, which you can use for further references to the
element. The function fails if an element with the specified name
already exists, but still sets ``element`` to the corresponding element
number.

.. rubric:: Adding element to subsets

If the set is a subset, AIMMS will add the element to that subset only.
Thus, the function will fail and return no element number if the
corresponding element does not already exist in the associated root set.
If the element is present in the root set, but not in the domain of the
subset, the functions will fail but still return the element number
corresponding to the presented string. With the function
``AimmsSetAddElementRecursive`` you can add an element to a subset
itself as well as to all its supersets, up to the associated root set.

.. rubric:: Renaming set elements

Through the function ``AimmsSetRenameElement`` you can provide a new
name for an element number associated with an existing element in a set.
The change in name does not imply any change in the data previously
defined over the element. However, the element will be displayed
according to its new name in the graphical user interface, or in data
exchange with external data sources.

.. rubric:: Deleting set elements

With the function ``AimmsSetDeleteElement`` you can delete the element
with the given element number from a simple set. If the set is a *root*
set, any remaining data defined over the element in subsets parameters
and variables will become inactive. To remove such inactive references
to the deleted element, you can use the API function
``AimmsIdentifierCleanup`` (see also :ref:`sec:api.identifier`).

.. rubric:: Modifying subset contents

Alternatively to applying the functions ``AimmsSetAddElement`` and
``AimmsSetDeleteElement`` to subsets, you can also use the function
``AimmsValueAssign`` to modify the contents of a subset. In that case,
you should assign the value 1 to the tuple that should be added to the
subset, or 0 to a tuple that should be removed (as discussed in the
previous section). The function ``AimmsValueAssign`` will also work on
indexed sets and relations.

.. rubric:: Adding multiple set elements to a simple set...

When, as part of a large data transfer from an external data source to
AIMMS, you have to add a large amount of (non-existing) set elements to
a simple AIMMS set, the use of the functions ``AimmsSetElement`` and
``AimmsSetElementRecursive`` may become a performance bottleneck
compared to any bulk data transfer of multidimensional data defined over
these set elements. The reason for this is that the function
``AimmsSetElementAdd`` adds elements one at a time, and may need to
extend the internal data structures used to store set data many times,
which is a relatively expensive action.

.. rubric:: ... in an efficient manner

As an alternative, AIMMS offers a different set of functions that
combined allow you to add multiple set elements much more efficiently,
at the expense of a slightly more complex sequence of actions. The
functions are:

-  the function ``AimmsSetElementNumber``, which retrieves an existing,
   or creates a new, set element number for a given element name, *but
   does not add it yet to any set*, and

-  the functions ``AimmsSetAddElementMulti`` and
   ``AimmsSetAddElementRecursiveMulti``, which add multiple elements to
   a set or a hierarchy of sets simultaneously by passing an array of
   set element numbers created through the function
   ``AimmsSetElementNumber``.

.. rubric:: Set element representations

The functions

-  ``AimmsSetElementToOrdinal``,

-  ``AimmsSetElementToName``,

-  ``AimmsSetOrdinalToElement``,

-  ``AimmsSetOrdinalToName``,

-  ``AimmsSetNameToElement``, and

-  ``AimmsSetNameToOrdinal``

allow you to convert AIMMS' element numbers into ordinal numbers within
a particular subset, and element names and vice versa. The functions
will fail when the input representation does not correspond to an
existing element.

.. rubric:: Ordinal numbers may change

In working with ordinal numbers, you should be aware that ordinal
numbers are not invariant under changes to a set. When an element is
added to or deleted from a set, or when the ordering of the set has
changed, the ordinal numbers of some or all of its elements may have
changed. In contrast, the element numbers and names of elements remain
constant as long as the case used by the AIMMS model has not changed, or
when the ``CLEANDEPENDENTS`` operator has not been applied to one or
more root sets. You can verify the latter condition with a call to the
function ``AimmsIdentifierDataVersion`` (see also
:ref:`sec:api.identifier`).