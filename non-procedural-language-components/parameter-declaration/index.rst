.. _chap:par:

Parameter Declaration
=====================

.. rubric:: Terminology

The word parameter does not have a uniform meaning in the scientific
community. When you are a statistician, you are likely to view a
parameter as an unknown quantity to be estimated from observed data. *In
AIMMS the word parameter denotes a known quantity that holds either
numeric or string-valued data.* In programming languages the term
variable is used for this purpose. However, this is not the convention
adopted in AIMMS, where, in the context of a mathematical program, the
word variable is reserved for an unknown quantity. Outside this context,
a variable behaves as if it were a parameter. The terminology in AIMMS
is consistent with the standard operations research terminology that
distinguishes between parameters and variables.

.. rubric:: Why use parameters

Rather than putting the explicit data values directly into your
expressions, it is a much better practice to group these values together
in parameters and to write all your expressions using these symbolic
parameters. Maintaining a model that contains explicit data is a
painstaking task and error prone, because the meaning of each separate
number is not clear. Maintaining a model in symbolic form, however, is
much easier and frequently boils down to simply adjusting the data of a
few clearly named parameters at a single point.

.. rubric:: Example

Consider the set ``Cities`` introduced in the previous chapter and a
parameter ``FixedTransport(i,j)``. Suppose that the cost of each unit of
transport between cities ``i`` and ``j`` is stored in the parameter
``UnitTransportCost(i,j)``. Then the definition of
``TotalTransportCost`` can be expressed as

.. code-block:: aimms

	TotalTransportCost := sum[(i,j), UnitTransportCost(i,j)*FixedTransport(i,j)];

Not only is this expression easy to understand, it also makes your model
extendible. For instance, an extra city can be added to your model by
simply adding an extra element to the set ``Cities`` as well as updating
the tables containing the data for the parameters ``UnitTransportCost``
and ``FixedTransport``. After these changes the above statement will
automatically compute ``TotalTransportCost`` based on the new settings
without any explicit change to the symbolic model formulation.

.. toctree::
   :maxdepth: 1

   parameter-declaration-and-attributes