.. _sec:intro.decl:

The Depot Location Problem
==========================

.. rubric:: The modeling process

In translating any real-life problem into a valid AIMMS optimization
model (referred to as a mathematical program) several conceptual steps
are required. They are:

-  describe the input and output data using sets and indexed
   identifiers,

-  specify the mathematical program,

-  specify procedures for data pre- and post-processing,

-  initialize the input data from files and databases,

-  solve the mathematical program, and

-  display the results (or write them back to a database).

.. rubric:: Problem description

The example in this chapter is based on a simple depot location problem
which can be summarized as follows.

   Consider the distribution of a single product from one or more depots
   to multiple customers. The objective is to select depots from a
   predefined set of possible depots (each with a given capacity) such
   that

   -  the demand of each customer is met,

   -  the capacity of each selected depot is not exceeded, and

   -  the total cost for both depot rental and transport to the
      customers is minimized.

.. rubric:: Use of sets

In the above problem you can see that there are two entities that
determine the size of the problem: depots and customers. With these
entities a number of instances are associated, e.g. a particular
instance of a depot could be ``'Amsterdam'``. The precise collection of
instances, however, may differ from run to run. Therefore, when
translating the problem into a symbolic model it is customary and
desirable not to make any explicit reference to individual instances.
Such high-level model specification can be accomplished through the use
of *sets*, each with an associated *index* for referencing arbitrary
elements in that set.

.. rubric:: Initial set declarations

The following set declarations in AIMMS introduce the two sets
``Depots`` and ``Customers`` with indices ``d`` and ``c``, respectively.
AIMMS has a convenient graphical model editor to create your model. It
allows you to enter all model input using graphical forms. However, in
the interest of compactness we will use a textual representation for
declarations that closely resembles the contents of a graphical form
throughout this manual.

.. code-block:: aimms

	Set Depots {
	    Index :  d;
	}
	Set Customers{
	    Index :  c;
	}

.. rubric:: Parameters for input data

In most models there is input data that can be naturally associated with
a particular element or tuple of elements in a set. In AIMMS, such data
is stored in Parameters. A good example in the depot location problem is
the quantity ``Distance``, which can be defined as the distance between
depot ``d`` and customer ``c``. To define ``Distance`` a index tuple
(``d``,\ ``c``) is required and it is referred to as the associated
``IndexDomain`` of this quantity.

.. rubric:: Example

In AIMMS, the identifier ``Distance`` is viewed as a ``Parameter`` (a
known quantity), and can be declared as follows.

.. code-block:: aimms

	Parameter Distance {
	    Index :  (d,c);
	}

In this example the identifier ``Distance`` is referred to as an ndexed
identifier, because it has a nonempty index domain.

.. rubric:: Scalar data

Not all identifiers in a model need to be indexed. The following
declarations illustrate two scalar parameters which are used later.

.. code-block:: aimms

	Parameter MaxDeliveryDistance;
	Parameter UnitTransportRate;

.. rubric:: Restricting permitted routes

For real-life applications the collection of all possible routes
``(d,c)`` may be huge. In practice, routes ``(d,c)`` for which the
distance ``Distance(d,c)`` is big, will never become a part of the
solution. It, therefore, makes sense to exclude such routes ``(d,c)``
from the entire solution process altogether. We can do this by computing
a set of ``PermittedRoutes`` which we will use throughout the sequel of
the example.

.. _examp:tutor.routes:

.. rubric:: Example

In AIMMS, the relation ``PermittedRoutes`` can be declared as follows.

.. code-block:: aimms

	Set PermittedRoutes {
	    SubsetOf     :  (Depots, Customers);
	    Definition   :  {
	        { (d,c) | Distance(d,c) <= MaxDeliveryDistance }
	    }
	}

.. rubric:: Explanation

In the ``SubsetOf`` attribute of the above declaration it is indicated
that the set ``PermittedRoutes`` is a subset of the Cartesian product of
the simple sets ``Depots`` and ``Customers``. The ``Definition``
attribute globally defines the set ``PermittedRoutes`` as the set of
those tuples (``d``, ``c``) for which the associated ``Distance(d,c)``
does not exceed the value of the scalar parameter
``MaxDeliveryDistance``. AIMMS will assure that such a global
relationship is valid at any time during the execution of the model.
Note that the set notation in the ``Definition`` attribute resembles the
standard set notation found in mathematical literature.

.. rubric:: Applying domain restrictions

Now that we have restricted the collection of permitted routes, we can
use the relation ``PermittedRoutes`` throughout the model to restrict
the domain of identifiers declared over ``(d,c)`` to only hold data for
permitted routes ``(d,c)``.

.. rubric:: Example

In AIMMS, the parameter ``UnitTransportCost`` can be declared as
follows.

.. code-block:: aimms

	Parameter UnitTransportCost {
	    IndexDomain  :  (d,c) in PermittedRoutes;
	    Definition   :  UnitTransportRate * Distance(d,c);
	}

This parameter is defined through a simple formula. Once an identifier
has its own definition, AIMMS will not allow you to make an assignment
to this identifier anywhere else in your model text.

.. rubric:: Effects of domain restriction

As an effect of applying a domain restriction to the parameter
``UnitTransportCost``, any reference to ``UnitTransportCost(d,c)`` for
tuples (``d``,\ ``c``) outside the set ``PermittedRoutes`` is not
defined, and AIMMS will evaluate this quantity to 0. In addition, AIMMS
will use the domain restriction in its GUI, and will not allow you to
enter numerical values of ``UnitTransportCost(d,c)`` outside of its
domain.

.. rubric:: Additional parameter declarations

To further define the depot location problem the following parameters
are required:

-  the fixed rental charge for every depot ``d``,

-  the available capacity of every depot ``d``, and

-  the product demand of every customer ``c``.

The AIMMS declarations are as follows.

.. code-block:: aimms

	Parameter DepotRentalCost {
	    IndexDomain  :  d;
	}
	Parameter DepotCapacity {
	    IndexDomain  :  d;
	}
	Parameter CustomerDemand {
	    IndexDomain     :  c;
	}