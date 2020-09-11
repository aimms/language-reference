.. _chap:stoch:

Stochastic Programming
======================

.. rubric:: Deterministic vs. stochastic models

The mathematical programming types discussed so far have a common
assumption that all the input data used in the formulation of the
mathematical program is known with certainty. This is known as "decision
making under certainty," and the corresponding models are called
*deterministic* models. Models that account for uncertainty in the input
data are called *stochastic* models, and the theory and techniques used
to solve stochastic models is commonly referred to as stochastic
programming. You can find an introduction to stochastic programming in
Chapters 16 and 17 of the AIMMS `Modeling Guide <https://documentation.aimms.com/_downloads/AIMMS_modeling.pdf>`__. 
A more in-depth discussion of stochastic programming and
its solution methods can be found, for instance, in :cite:`bib:BL97` and
:cite:`bib:KM05`.

.. rubric:: Stochastic programming in AIMMS

In this chapter, you will find a description of the facilities built
into AIMMS for creating and solving stochastic models. From any existing
deterministic linear (LP) or mixed-integer (MIP) model, AIMMS is able to
automatically create a stochastic model as well, *without the need for
you to reformulate any of the constraint definitions*. The only steps
necessary to create a stochastic model are

-  to indicate which parameters and variables in your deterministic
   model are to become stochastic in a declarative manner, and

-  to provide the scenario tree and the stochastic input data.

.. rubric:: Single formulation

Being able to generate both a deterministic and stochastic model from an
identical symbolic formulation allows for any changes you make in the
deterministic formulation to automatically propagate to the stochastic
model. This significantly reduces the effort involved with maintaining a
stochastic model associated with a given deterministic model.

.. rubric:: This chapter

:ref:`sec:stoch.concepts` discusses a number of basic concepts in
stochastic programming. These provide a common understanding necessary
for the introduction of the stochastic programming facilities of AIMMS
discussed in :ref:`sec:stoch.stoch`. :ref:`sec:stoch.tree` describes the
facilities available in AIMMS for the generation of a scenario tree,
while :ref:`sec:stoch.solve` discusses the steps necessary to solve a
stochastic model in AIMMS.

.. toctree::
   :maxdepth: 1

   basic-concepts
   stochastic-parameters-and-variables
   scenario-generation
   solving-stochastic-models