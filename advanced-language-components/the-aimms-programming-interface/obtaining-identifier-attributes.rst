.. _sec:api.attribute:

Obtaining Identifier Attributes
===============================

.. rubric:: Obtaining attributes

For every identifier handle passed to (or created from within) an
external function, AIMMS can provide additional attributes that are
either related to the declaration of the identifier associated with the
handle, or to the particular identifier slice that was passed as an
argument in the external function call. :numref:`table:api.info` lists
all AIMMS API functions which can be used to obtain these additional
attributes.

.. _table:api.info:

.. table:: AIMMS API functions for obtaining handle attributes

   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeName(int handle, AimmsString *name)``               |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeType(int handle, int *type)``                       |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeStorage(int handle, int *storage)``                 |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeDefault(int handle, AimmsValue *value)``            |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeSetUnit(int handle, char *unit, char *convention)`` |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeGetUnit(int handle, AimmsString *unitName)``        |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeDimension(int handle, int *full, int *slice)``      |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeRootDomain(int handle, int *domain)``               |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeDeclarationDomain(int handle, int *domain)``        |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeCallDomain(int handle, int *domain)``               |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeRestriction(int handle, int *domainhandle)``        |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeSlicing(int handle, int *slicing)``                 |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributePermutation(int handle, int *permutation)``         |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeFlagsSet(int handle, int flags)``                   |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeFlagsGet(int handle, int *flags)``                  |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeFlags(int handle, int *flags)``                     |
   +-------------------------------------------------------------------------+
   | ``int AimmsAttributeElementRange(int handle, int *sethandle)``          |
   +-------------------------------------------------------------------------+

.. rubric:: Identifier name and type

With the functions ``AimmsAttributeName`` and ``AimmsAttributeType`` you
can request the name and identifier type of the identifier associated
with a handle. AIMMS passes the name of an identifier through an
``AimmsString`` structure (explained below). AIMMS only allows handles
for identifier types with which data can be associated. More
specifically, AIMMS distinguishes the following identifier types:

-  simple root set,

-  simple subset,

-  relation,

-  indexed set,

-  numeric parameter,

-  element parameter,

-  string parameter,

-  unit parameter,

-  variable,

-  element variable.

When the handle refers to a suffix of an identifier, the suffix type is
appended to the identifier name separated by a dot.

.. rubric:: Storage type

In addition to the identifier type, AIMMS also associates a storage type
with each handle. It is the data type in which AIMMS expects the data
values associated with the handle to be communicated. The function
``AimmsAttributeStorage`` returns the storage type. The possible storage
types are:

-  double (``double``),

-  integer (``int``),

-  binary (``int``, but only assuming 0-1 values),

-  string (``char *``).

The complete list of identifier and storage type values returned by
these functions can be found in the header file ``aimmsapi.h``.

.. rubric:: Default value

With the function ``AimmsAttributeDefault`` you can obtain the default
value of the identifier associated with a handle. The default value can
either be a double, integer or string value, depending on the storage
type associated with the handle. Below you will find the convention used
by AIMMS to pass such storage type dependent values back and forth.

.. rubric:: Setting and getting units

Through the functions ``AimmsAttributeGetUnit`` and
``AimmsAttributeSetUnit`` you can get and set the units of measurement
(see also :ref:`chap:units`) that will be used when passing data from
and to AIMMS. When setting the unit to be used, you can specify both a
unit and a convention. AIMMS will parse the given unit expression and
use the specified convention to compute the appriopriate multiplication
factors between the internal and external representation of the data of
the identifier at hand.

.. rubric:: Passing integer, double or string values
   :name: expl:extern.passing-values

All transfer of integer, double or string values takes place through the
record structures ``AimmsString`` and ``AimmsValue`` defined as follows.

.. code-block:: c

	typedef struct AimmsStringRecord {
	  int   Length;
	  char *String;
	} AimmsString;

.. code-block:: c

	typedef union AimmsValueRecord {
	  double      Double;
	  int         Int;
	  struct {
	    int       Length;
	    char     *String;
	  }
	} AimmsValue;

When ``value`` is such a structure, you can obtain an integer, double or
string value through ``value.Int``, ``value.Double`` or
``value.String``, respectively.

.. rubric:: Passing string lengths

For strings, you must set ``value.Length`` to the length of the string
buffer passed through ``value.String`` before calling the API function.
When AIMMS fills the ``value.String`` buffer, the actual length of the
string passed back is assigned to ``value.Length``. When the actual
string length exceeds the buffer size, AIMMS truncates the string passed
back through ``value`` to the indicated buffer size, and assigns the
length of the actual string to ``value.Length``.

.. rubric:: Identifier dimensions

For each handle you can obtain the dimension of the associated
identifier by calling the function ``AimmsAttributeDimension``. The
function returns:

-  the *full* dimension of the identifier as given in its declaration,
   and

-  the *slice* dimension, i.e. the resulting dimension of the actual
   identifier slice associated with the handle.

AIMMS uses tuples of length equal to the full dimension whenever
information is communicated regarding the index domain of a handle or
its slicing. When explicit data values associated with a handle are
passed using the AIMMS API functions discussed in :ref:`sec:api.value`,
AIMMS communicates such values using tuples of length equal to the slice
dimension.

.. rubric:: Set dimensions

For all data communication with external DLLs AIMMS considers sets to be
represented by binary indicator parameters indexed over their respective
root sets. For all elements in these root sets, such an indicator
parameter assumes the value 1 if a root set element (or tuple of root
set elements) is contained in the set at hand, or 0 otherwise. Since the
default of these indicator parameters is 0, AIMMS only needs to
communicate the nonzero values, i.e. exactly the tuples that are
actually contained in the set. In connection with this representation,
AIMMS returns the following (full or slice) dimensions for sets:

-  the dimension of a *simple set* is 1,

-  the dimension of a *relation* is the dimension of the Cartesian
   product of which the relation is a subset,

-  the dimension of an *indexed set* is the dimension of the index
   domain of the set plus 1.

.. rubric:: Identifier domains

The functions ``AimmsAttributeRootDomain``,
``AimmsAttributeDeclarationDomain`` and ``AimmsAttributeCallDomain`` can
be used to obtain an integer array containing handles to domain sets for
every dimension of the identifier at hand. These domains play a
different role in the sparse data communication, as explained below.

.. rubric:: Root domain handles

The function ``AimmsAttributeRootDomain`` returns an array of handles to
the respective root sets associated with the index domain specified in
the identifier's declaration. You need these handles, for instance, to
obtain a string representation of the element numbers returned by the
data communication AIMMS API functions discussed in
:ref:`sec:api.value`.

.. rubric:: Declaration domain handles

The function ``AimmsAttributeDeclarationDomain`` returns an array of
handles to the respective domain sets specified in the identifier's
declaration. These domain sets can be equal to their corresponding root
sets, or to subsets thereof. AIMMS will only pass data values for
element tuples in the declaration domain, unless you have specified the
``raw`` translation modifier (see also :ref:`sec:extern.declaration`)
for a handle argument, or have created the handle yourself with the raw
flag set (see also :ref:`sec:api.identifier`).

.. rubric:: Call domain handles

The function ``AimmsAttributeCallDomain`` returns an array of handles to
the particular subsets of the root sets (as returned in the root domain
of the handle) to which data communication is restricted for this
handle. The call domain can be different from the global domain if an
actual external argument has been restricted to a subdomain of the root
set in an external call (see also :ref:`sec:intern.ref`), or if you have
created the handle with an explicit call domain yourself (see also
:ref:`sec:api.identifier`). AIMMS will only pass data values associated
with element tuples in just the call domain (raw flag set), or in the
intersection of the call and declaration domain (raw flag not set).

.. rubric:: Domain restriction

With the function ``AimmsAttributeRestriction`` you can obtain a handle
to the global domain restriction of an indexed identifier as specified
in its declaration and (dynamically) maintained by AIMMS as necessary.
You may want to use this handle in conjunction with raw handles
(explained in :ref:`sec:api.value`) to verify whether a particular
element satisfies its domain restriction.

.. rubric:: Example

Consider the following set and parameter declarations.

.. code-block:: aimms

	Set S_0 {
	    Index        : i_0;
	}
	Set S_1 {
	    SubsetOf     : S_0;
	    Index        : i_1, j_1;
	}

.. code-block:: aimms

	Set S_2 {
	    SubsetOf     : S_1;
	    Index        : i_2;
	}
	Parameter p {
	    IndexDomain  : i_0;
	}
	Parameter q {
	    IndexDomain  : (i_1, j_1) | p(i_1);
	}

A handle to (in AIMMS notation) ``q(i_1, i_2)`` will return handles to

-  ``S_0`` and ``S_0`` for the respective root domains,

-  ``S_1`` and ``S_1`` for the respective declaration domains,

-  ``S_1`` and ``S_2`` for the respective call domains, and

-  ``p(i_1)`` for the domain restriction.

.. rubric:: Slicing

As discussed in :ref:`sec:intern.ref`, the actual arguments in a
procedure or function call can be slices of higher-dimensional
identifiers within your model. When the slice dimension of a handle in
an external call is less then its full dimension, you can use use the
function ``AimmsAttributeSlicing`` to find out which dimensions of the
associated AIMMS identifier have been sliced, and to which elements. The
function returns an integer array containing, for every dimension, the
element number (within the associated root set) to which the
corresponding domain has been sliced, or the number
``AIMMSAPI_NO_ELEMENT`` if no slicing took place.

.. rubric:: Domain permutations

Through the function ``AimmsAttributePermutation`` you can obtain the
permutation of a permuted handle created with the function
``AimmsAttributeHandleCreatePermuted``. The output ``permutation``
argument must be an integer array of length equal to the full dimension
of the identifier. AIMMS returns the following values:

-  if a dimension of the handle is sliced, the corresponding position in
   the ``permutation`` array will be 0,

-  if a dimension is not sliced, the corresponding position in the
   ``permutation`` array will contain the sliced position (starting at
   1, and numbered from 1 to the handle's slice dimension)

   -  in which AIMMS will store elements of the corresponding dimension
      in a ``tuple`` returned by the functions ``AimmsValueNext`` and
      ``Aimms ValueNextMulti``, or

   -  in which AIMMS expects such elements in calls to the functions
      ``AimmsValueSearch`` and ``AimmsValueRetrieve``.

.. rubric:: Getting ordered, special, raw and read-only flags

By specifying the input-output type and the ``ordered``,
``retainspecials``, ``elementsasordinals`` or ``raw`` translation
modifiers for arguments in an external call (see also
:ref:`sec:extern.declaration`), you can influence the manner in which
data is passed to an external function. With the AIMMS API function
``AimmsAttributeFlagsGet`` you obtain the active set of ``flags``
indicating whether

-  the data associated with a handle is passed ordered (``ordered``
   flag),

-  special values are passed unchanged or are translated
   (``retainspecials`` flag),

-  element tuples are passed by their element numbers
   (``elementsasordinals`` flag),

-  inactive data is passed (``raw`` flag), and

-  you can make assignments to the handle (input-output type).

The result is the *bitwise or* function of the individual flag values as
defined in the ``aimmsapi.h`` header file.

.. rubric:: Setting flags

Through the function ``AimmsAttributeFlagSet`` you can modify the flag
settings for an existing handle. Note that the result of calls to
``AimmsValueNext`` may become unpredictable after modifying the
``ordered`` flag. In such a case, you are advised to reset the handle
through the function ``AimmsHandleReset``.

.. rubric:: Element range

When a handle is associated with an element parameter within your
application, you can use the function ``AimmsAttributeElementRange`` to
obtain a handle to the set constituting the element range of the element
parameter. You need this handle, for instance, when you want to obtain a
string representation of the element numbers within the element range
communicated by AIMMS in the AIMMS API functions discussed
:ref:`sec:api.value`.