.. _sec:api.value:

Communicating Individual Identifier Values
==========================================

.. rubric:: Communicating identifier values

With every identifier handle AIMMS lets you retrieve all associated
nondefault data values on an element-by-element basis. In addition,
AIMMS lets you search whether a nondefault value exists for a particular
element tuple, and make assignments to individual element tuples.
:numref:`table:api.value` lists all the available AIMMS API functions
for this purpose.

.. _table:api.value:

.. table:: AIMMS API functions for sparse data communication

   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueCard(int handle, int *card)``                                     |
   +===================================================================================+
   | ``int AimmsValueResetHandle(int handle)``                                         |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueSearch(int handle, int *tuple, AimmsValue *value)``               |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueNext(int handle, int *tuple, AimmsValue *value)``                 |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueNextMulti(int handle, int *n, int *tuples, AimmsValue *values)``  |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueRetrieve(int handle, int *tuple, AimmsValue *value)``             |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueAssign(int handle, int *tuple, AimmsValue *value)``               |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueAssignMulti(int handle, int n, int *tuples, AimmsValue *values)`` |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueDoubleToMapval(double value, int *mapval)``                       |
   +-----------------------------------------------------------------------------------+
   | ``int AimmsValueMapvalToDouble(int mapval, double *value)``                       |
   +-----------------------------------------------------------------------------------+

.. rubric:: Cardinality

The function ``AimmsValueCard`` returns the cardinality of a handle,
i.e. the number of nondefault elements of the associated identifier
slice. You can call this function, for instance, when you need to
allocate memory for the data structures in your own code before actually
retrieving the data.

.. rubric:: Retrieving nondefault values

The functions ``AimmsValueResetHandle``, ``AimmsValueSearch`` and
``AimmsValueNext`` retrieve nondefault values associated with a handle
on an element-by-element basis.

-  The function ``AimmsValueResetHandle`` resets the handle to the
   position just before the first nondefault element.

-  The function ``AimmsValueSearch`` expects an input tuple of element
   numbers (in the slice domain), and returns the first tuple for which
   a nondefault value exists on or following the input tuple.

-  The function ``AimmsValueNext`` returns the first nondefault element
   directly following the element returned by the last call to
   ``AimmsValueNext`` or ``AimmsValueSearch``, or the first element if
   the function ``AimmsValueResetHandle`` was called last. The function
   fails when there is no such element.

By calling ``AimmsValueResetHandle`` and subsequently ``AimmsValueNext``
it is possible to retrieve *all* nondefault values. By calling the
function ``AimmsValueSearch`` you can directly skip to a particular
element tuple if you have found that the intermediate tuples are not
interesting anymore, and continue from there.

.. rubric:: No scalar handles

The functions ``AimmsValueResetHandle``, ``AimmsValueNext`` and
``AimmsValueSearch`` do not accept handles to scalar
(i.e. 0-dimensional) identifier slices. To retrieve and assign scalar
values you should use the functions ``AimmsValueRetrieve`` and
``AimmsValueAssign`` explained below.

.. rubric:: Unordered versus ordered retrieval

The particular element returned by the functions ``AimmsValueSearch``
and ``AimmsValueNext`` may differ depending on the setting of the
``ordered`` flag for the handle. If the handle has been created
unordered (default), the values returned successively are ordered by
increasing element number in a right-to- left tuple order. If the handle
has been created ordered, AIMMS will return values in accordance with
the ordering principles imposed on all *local* tuple domains.

.. rubric:: Raw data retrieval

By default, AIMMS will only pass values for element tuples that lie
within the *current* contents of the intersection of the call domain and
declaration domain of an identifier. Thus, the values that get passed
may depend on a dynamically changing domain restriction that is part of
the index domain in the declaration of an identifier. When the ``raw``
modification flag is set for a handle, AIMMS will pass *all* available
data values in the call domain, regardless of the domain restrictions.

.. rubric:: Return tuple and value

All data retrieval functions return a ``tuple`` and the associated
nondefault ``value``. The interpretation of the ``value`` argument for
all possible storage types was discussed on
:ref:`expl:extern.passing-values`. The ``tuple`` argument must be an
integer array of length equal to the *slice* dimension of the handle.
Upon success, the tuple contains the element numbers in the *global*
domain sets for every non-sliced dimension.

.. rubric:: Element or ordinal numbers

By setting the flag ``elementsasordinals`` during the creation of a
handle, you can modify the default tuple representation. If this flag is
set, the tuples returned by AIMMS will contain ordinal numbers
corresponding to the respective call domains associated with the handle.
Similarly, AIMMS expects tuples that are passed to it, to contain
ordinal numbers as well, when this flag is set.

.. rubric:: Rationale

While at first sight the choice for representing tuples by their element
numbers in the global domain of a handle may seem less convenient than
ordinal numbers in its call domain, you must be aware that the latter
representation is not invariant under changes in the contents of the
call domain. Alternatively to setting the flag ``elementsasordinals``,
you can also convert the returned element numbers into these formats
using the AIMMS API functions discussed in :ref:`sec:api.set`.

.. rubric:: Value types

The expected storage type of the data values returned by the data
retrieve functions can be obtained using the function
``AimmsAttributeStorage``. The possible storage types for the various
identifier types are listed below:

-  numeric parameters and variables return double or integer values,

-  all set types return binary values,

-  element parameters return integer element numbers, and

-  string and unit parameters return string values.

.. rubric:: Element parameter values

The element numbers returned for element parameters are relative to the
set handle returned by the function ``AimmsAttributeElementRange``. You
can use the AIMMS API functions of :ref:`sec:api.set` to obtain the
associated ordinal numbers or string representations.

.. rubric:: Set values

For sets (either simple, relation or indexed), the data retrieval
functions return the binary value 1 for just those elements (or element
tuples) that are contained in the set. For indexed sets, AIMMS returns
tuples for which the last component is the element number of an element
contained in the set slice associated with all but the last tuple
components.

.. rubric:: Converting special numbers

When a handle to a numeric parameter or variable has been created with
the ``special`` flag set, the data retrieval functions will pass any
special number value associated with the handle as is (see also
:ref:`sec:extern.declaration` and :ref:`sec:api.attribute`). AIMMS
represents special numbers as double precision floating point numbers
outside AIMMS' ordinary range of computation. The function
``AimmsValueDoubleToMapval`` returns the :any:`MapVal` value associated
with any double value (see also :numref:`table:expr.arith-ext`), while
the function ``AimmsValueMapvalToDouble`` returns the double
representation associated with any type of special number.

.. rubric:: Retrieving specific values

The function ``AimmsValueRetrieve`` returns the value for a specific
element tuple in the slice domain. This value can be either the default
value or a nondefault value. The tuple must consist of element numbers
in the corresponding domain sets. When the ``raw`` flag is not set, the
function fails (but still returns the default value of the associated
identifier) for any tuple outside of the index domain of the handle.
When the ``raw`` flag is set, the function fails only when there is no
data for the tuple.

.. rubric:: Assigning values

The function ``AimmsValueAssign`` lets you assign a new value to a
particular element tuple in the slice domain. If you want to assign the
default value you can either pass a null pointer for ``value``, or a
pointer to the appropriate default value. The function fails if you try
to assign a value to an element tuple outside the contents of the call
domain of the handle. When the ``raw`` flag is not set, the function
will also fail if the assigned tuple lies outside of the current
(active) contents of the declaration domain.

.. rubric:: Exchanging multiple values

When a particular identifier handle requires the exchange of a large
amount of values, you are strongly encouraged to use the functions
``AimmsValueNextMulti`` and ``AimmsValueAssignMulti`` instead of the
functions ``AimmsValueNext`` and ``AimmsValueAssign``. In general, AIMMS
can perform the simultaneous exchange of multiple values much more
efficient than the equivalent sequence of single exchanges. For both
functions, the ``tuples`` array must be an integer array of length ``n``
times the *slice* dimension of the handle, while the ``values`` array
must be the corresponding ``AimmsValue`` array of length ``n``.

-  In the function ``AimmsValueNextMulti``, AIMMS will fill the
   ``tuples`` array with the respective tuples for which nondefault
   values are returned in the ``values`` array. Upon return, the ``n``
   argument will contain the actual number of values passed.

-  In the function ``AimmsValueAssignMulti``, the ``tuples`` array must
   be filled sequentially with the respective tuples to which the
   assignments take place via the ``values`` array.

When your data transfer involves the addition of a large amount of set
elements to an AIMMS set as well, you may also want to consider using
the function ``AimmsSetAddElementMulti`` (see :ref:`sec:api.set`).

.. rubric:: Communicating scalar values

When a handle corresponds to a 0-dimensional (i.e. scalar) identifier
slice, you can still use the ``AimmsValueRetrieve`` and
``AimmsValueAssign`` to retrieve its value or assign a value to it. In
this case, the ``tuple`` argument is ignored.

.. rubric:: Assigning set values

When you want to delete or add an existing element or element tuple to a
set, you must assign the value 0 or 1 to the associated tuple
respectively. If you want to add a tuple of nonexisting simple elements,
you must first add these elements to the corresponding global simple
domain sets using the function ``AimmsSetAddElement`` discussed below.