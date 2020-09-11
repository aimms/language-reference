.. _chap:units:

Units of Measurement
====================

This chapter describes how to incorporate dimensional analysis into an
AIMMS application. As will be explained, you can define quantities and
their corresponding units, and associate these units with identifiers in
your model. AIMMS automatically checks for unit consistency in all the
constraints and assignment statements. In addition, AIMMS allows you to
specify unit conventions. With this facility it is possible for
end-users around the world to select their preferred convention, and
view the model data in the units associated with that convention.

.. toctree::
   :maxdepth: 1

   introduction
   the-quantity-declaration
   associating-units-with-model-identifiers
   unit-analysis
   unit-based-scaling
   unit-expressions
   locally-overriding-units
   globally-overriding-units-through-conventions
   unit-valued-parameters