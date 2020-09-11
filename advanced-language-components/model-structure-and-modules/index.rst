.. _chap:module:

Model Structure and Modules
===========================

.. rubric:: Model and sections

This chapter discusses the common structuring components of a model,
namely the *main model* and model *sections*. With the use of sections,
you can provide depth to the model tree in the AIMMS **Model Explorer**,
which allows you to structure your model in any logical manner that
makes sense to you. Imposing a clear and logical structure to your model
will strongly add to the overall maintainability of your modeling
application.

.. rubric:: Modules

The next concept introduced in this chapter is that of a *module*, which
is basically a model section with its own, separate, namespace. Modules
allow you to share sections of model source between multiple models,
without the risk of running into name clashes. AIMMS uses modules to
implement those parts of its functionality that can be best expressed in
the AIMMS language itself. The available AIMMS system modules include

-  a (customizable) implementation of the outer approximation algorithm,

-  a scenario generation module for stochastic programming, and

-  sets of constants used in the graphical 2D- and 3D-chart objects.

.. rubric:: Library modules

Finally, this chapter discusses the concept of a *library module*, which
is the source module associated with a library project (see
Section 3.1 of the `User's Guide <https://documentation.aimms.com/_downloads/AIMMS_user.pdf>`__). Library
modules can only be added to an AIMMS model through the **Library
Manager**, and are always displayed as a separate root in the model
tree.

.. toctree::
   :maxdepth: 1

   introduction
   model-declaration-and-attributes
   section-declaration-and-attributes
   module-declaration-and-attributes
   librarymodule-declaration-and-attributes
   runtime-libraries-and-the-model-edit-functions