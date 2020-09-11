.. _chap:robust:

Robust Optimization
===================

.. rubric:: Introduction

Robust optimization is a rather new modeling methodology for decision
making under uncertainty. Robust optimization is designed to meet some
major challenges associated with uncertainty-affected optimization
problems:

-  to operate under lack of full information on the nature of
   uncertainty,

-  to model the problem in a form that can be solved efficiently, and

-  to provide guarantees about the performance of the solution.

Robustness of decisions is defined in terms of the best performance in
the worst case possible state-of-the-world (min-max optimization). A
more in-depth discussion of robust optimization can be found, for
instance, in :cite:`bib:BGN09`.

.. rubric:: Robust optimization in AIMMS

In this chapter, you will find a description of the facilities built
into AIMMS for creating and solving robust optimization models. From any
existing deterministic linear program (LP) or mixed-integer program
(MIP), AIMMS is able to automatically create a robust optimization model
as well, *without the need for you to reformulate any of the constraint
definitions*. The only steps necessary to create a robust optimization
model are

-  to indicate which parameters in your deterministic model are to
   become uncertain in a declarative manner,

-  to indicate which variables in your deterministic model are to become
   adjustable to the uncertain parameters (if any), and

-  to specify possible realizations of the uncertain parameters.

.. rubric:: Single formulation

Being able to generate both a deterministic and robust optimization
model from an identical symbolic formulation allows for any changes you
make in the deterministic formulation to automatically propagate to the
robust optimization model. This significantly reduces the effort
involved with maintaining a robust optimization model associated with a
given deterministic model.

.. rubric:: Robust Optimization Add-On required

To be able to run an robust optimization model, you need to make sure
you have the *Robust Optimization Add-On* licensed. Without the RO
Add-On, you can still define your robust optimization models, but will
be unable to solve them (an execution error will occur).

.. rubric:: Acknowledge-ments

The Robust Optimization Add-On in AIMMS has been developed in close
cooperation with Professor Aharon Ben-Tal and Boris Bachelis of the
Technion, Israel Institute of Technology. We would like to express our
gratitude for our partnership in developing the Robust Optimization
Add-On in AIMMS and for their continuous support to get the details
right, which allowed us to make Robust Optimization a natural and
intuitive extension to our existing functionality.

.. rubric:: This chapter

:ref:`sec:robust.concepts` discusses a number of basic concepts in
robust optimization. These provide a common understanding necessary for
the introduction of the robust optimization features of AIMMS discussed
in the sections to follow. :ref:`sec:robust.uncertain` describes the
facilities available in AIMMS for specifying uncertain parameters, while
:ref:`sec:robust.chance` discusses chance constraints as another means
to introduce uncertainty into your robust optimization model.
:ref:`sec:robust.adjustable` discusses the facilities available to
declare variables to be adjustable to uncertain parameters.
:ref:`sec:robust.solve`, finally, describes the steps how to actually
solve a robust optimization model.

.. toctree::
   :maxdepth: 1

   basic-concepts
   uncertain-parameters-and-uncertainty-constraints
   chance-constraints
   adjustable-variables
   solving-robust-optimization-models