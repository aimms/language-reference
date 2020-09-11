.. _sec:nonproc.dep:

Dependency Structure of Definitions
===================================

.. rubric:: Dependency graph

The definitions inside the declarations of global sets and parameters
together form a system of interrelated functional relationships. AIMMS
automatically determines the dependency between the defined identifiers
and the inputs that are used inside these relationships. Such
dependencies can be depicted in the form of a directed graph, called the
*dependency graph*. From this dependency graph, AIMMS determines the
minimal set of identifiers that must be recomputed-and in which order-to
get the total system of functional relationships up-to-date.

.. rubric:: Example

Consider the system of definitions

.. math::

   \begin{align}
   d_1 & \equiv e_1 + e_2 \\
      d_2 & \equiv d_1 + d_3 \\
      d_3 & \equiv e_2 + e_3 \\
      d_4 & \equiv e_1 + d_2.
   \end{align}

Its dependency graph, with identifiers as nodes and dependencies as
directed arcs, looks as follows.

.. figure:: dependency-structure-of-definitions-pspic1.svg

Note that a change to the input parameter :math:`e_3`, for instance,
requires the re-computation of the defined parameters
:math:`d_2,\dots,d_4`-but not of :math:`d_1`-to update the entire
system.

.. rubric:: Dependencies must be a-cyclic

The dependency graph associated with the set and parameter definitions
must be a-cyclic, i.e. must not contain circular references. In this
case, every change to one or more input parameters of defined sets or
parameters will result in a *finite* sequence of assignments to update
the system. If the dependency graph is cyclic, a simultaneous system of
relations will result. Such a system may not have a (unique) solution,
and can only be solved by a specialized solver. Simultaneous systems of
relations are handled inside AIMMS through the use of constraints and
mathematical programs.

.. rubric:: Example

An illegal set of dependencies results if the definition of :math:`d_1`
in the last example is changed as follows.

.. math:: d_1 \equiv d_4 + e_1 + e_2.

This results in the following cyclic dependency graph.

.. figure:: dependency-structure-of-definitions-pspic2.svg

Now, a change to any of the input parameters :math:`e_1,\dots,e_3` will
result in a simultaneous system for the parameters :math:`d_1`,
:math:`d_2` and :math:`d_4`.

.. rubric:: AIMMS will check

AIMMS computes the dependency structure between the parameter and set
definitions while compiling your model. If AIMMS detects a cyclic
dependency, an error will result, because AIMMS can, in general, not
deal with cyclic dependencies without relying on specialized numerical
solvers. In that case you need to remove the cyclic dependencies before
you can execute the model without further modifications. If you are
unable to remove the cyclic dependencies, you have essentially two
alternatives. You can either formulate a mathematical program, or define
your own solution method inside a procedure.

.. rubric:: Variables for simultaneous systems

The cyclic system can be turned into a mathematical program by changing
the parameters with cyclic definitions into variables. This results in a
simultaneous system of equalities which can be solved through a
``SOLVE`` statement. The declaration of mathematical programs is
discussed in :ref:`chap:mp`.

.. rubric:: Feedback loops

The alternative is to implement a customized solution procedure by
breaking the simultaneous system into a simulation with a feedback loop
linking inputs and outputs. To accomplish this, you must first remove
the cyclic definitions from the declarations, and then add a procedure
that implements the feedback loop. If you have sufficient knowledge of
the process you are describing, this route may result in fast
convergence behavior.

.. rubric:: Dependency is global only

AIMMS only allows a definition for globally declared sets and
parameters. Consequently, a single global dependency graph suffices to
express the functional relationships between all defined sets and
parameters.

.. rubric:: Dependency is symbolic

In addition, the dependency structure between set and parameter
definitions is purely based on symbol references. As a result, AIMMS'
automatic evaluation scheme will always recompute an indexed (output)
parameter depending on an indexed (input) parameter *in its entirety*,
even when only a single input value has changed.

.. rubric:: Inefficiency may occur

This evaluation behavior may lead to severe inefficiencies when you use
a high-dimensional defined parameter that is re-evaluated repeatedly
during the execution of a loop in your model. In such cases it is
advisable to refrain from using a definition for such a parameter, but
replace it by one or more assignments at the appropriate places in your
model. This issue is discussed in full detail in
:ref:`sec:eff.definition`.