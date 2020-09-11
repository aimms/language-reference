.. _sec:intro.tips:

General Modeling Tips
=====================

.. rubric:: From beginner to advanced

The previous sections introduced you to optimization modeling in AIMMS.
In such a small application, the model structure is quite transparent
and the formulation in AIMMS is straightforward. This section discusses
issues to consider when your model is larger and more complex.

.. rubric:: Separation of model and data

The AIMMS language is geared to strictly separate between model
formulation and the supply of its data. While this may seem unnatural at
first (when your models are still small), there are several major
advantages in using this approach.

-  By formulating the definitions and assignments associated with your
   problem in a completely symbolic form (i.e. without any reference to
   numbers or particular set elements) the intention of the expressions
   present in your model is more apparent. This is especially true when
   you have chosen clear and descriptive names for all the identifiers
   in your model.

-  With the separation of model and data it becomes possible to run your
   model with several data sets. Such data sets may describe completely
   different problem topologies, all of which is perfectly fine as long
   as your model formulation has been set up transparently.

-  Keeping your model free from explicit references to numbers or
   particular set elements improves maintainability considerably.
   Explicit data references inside assignment statements and constraints
   are essentially undocumented, and therefore subsequent changes in
   values are error-prone.

.. rubric:: Intellectual challenge

Translating a real-life problem into a working modeling application is
not always an easy task. In fact, finding a formulation or implementing
a solution method that works in all cases is quite often a demanding
(but also a very satisfying) intellectual challenge.

.. rubric:: Levels of abstraction

Setting up a transparent model involves incorporating an appropriate
level of abstraction. For example, when modeling a specific plant with
two production units and two products, you might be tempted to introduce
just four dedicated identifiers to store the individual production
values. Instead, it is better to introduce a single generic identifier
for storing production values for all units and all products. By doing
so, you incorporate genericity in your application and it will be
possible to re-use the application at a later date for a different plant
with minimum reformulation.

.. rubric:: Finding the proper level

Finding the proper level of abstraction is not always obvious but it
becomes easier as your modeling experience increases. In general, it is
a good strategy to re-think the consequences-with an eye on the
extensibility of your application-before implementing the most
straightforward data structures. In most cases the time spent finding a
more generic structure is paid back, because the better structure helps
you to formulate and extend the model in a clear and structured way.

.. rubric:: From small to large-scale

Transforming a small working demo application into a large scale
real-life application may result in problems if care is not taken to
specify variables and constraints in an accurate manner. In a small
model, there is usually no runtime penalty to poorly specified
mathematical programs. In contrast, when working with large
multidimensional data sets, a poor formulation of a mathematical program
can easily cause that

-  the available memory resources are exhausted, or

-  runtime requirements are not met.

Under these conditions, the physical constraints should be reassessed
and appropriate domains, parameter definitions and constraints added as
outlined below.

.. rubric:: Formulating proper domains of definition

For large applications you should always ask the following questions.

-  Have you adequately constrained the domains of high-dimensional
   identifiers? Often by reassessing the physical situation the domain
   range can be further reduced. Usually such domain restrictions can be
   expressed through logical conditions referring to other (input)
   identifiers.

-  Can you predict, for whatever reason, that some index combinations
   are very unlikely to appear in the solution of a mathematical
   program, even though they should be allowed formally? If so, you
   might experiment with omitting such combinations from their
   respective domains of definition, and see how this domain reduction
   reduces the size of the mathematical program and affects its
   solution.

As a result of carefully re-designing index domains you may find that
your model no longer exhausts available memory resources and runs in an
acceptable amount of time.

.. rubric:: Example

In the depot location problem discussed in this chapter, the domain of
the variable ``Transport`` has already restricted to the set of allowed
``PermittedRoutes``, as computed on :ref:`examp:tutor.routes`. Thus, the
mathematical program will never consider transports on a route that is
not desirable. Without this restriction, the mathematical program would
consider the transports from *every* depot ``d`` to *every* customer
``c``. The latter may cause the mathematical program size to explode,
when the number of depots and customers become large.

.. rubric:: Reformulation of algorithm

Finally, you may run into mathematical programs where the runtime of a
solution method does not scale well even after careful domain
definition. In this case, it may be necessary to reformulate the problem
entirely. One approach may be to decompose the original mathematical
program into subprograms, and use these together with a customized
sequential solution method to obtain acceptable solutions. You can find
pointers to many of such decomposition methods in the AIMMS Modeling
Guide.