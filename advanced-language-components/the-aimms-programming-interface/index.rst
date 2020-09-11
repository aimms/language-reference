.. _chap:api:

The AIMMS Programming Interface
===============================

.. rubric:: This chapter
   :name: api

In addition to the capability to call external procedures and functions
from within an AIMMS application, AIMMS also provides a generic
Application Programming Interface (API). This chapter describes the
semantics of the complete AIMMS API, and provides an extended example to
familiarize you with its use. In addition, it discusses the concurrency
aspects when multiple external applications are controlling a single
AIMMS session. Note that this chapter assumes that you have some basic
knowledge of the ``C`` programming language.

.. toctree::
   :maxdepth: 1

   introduction
   obtaining-identifier-attributes
   managing-identifier-handles
   communicating-individual-identifier-values
   accessing-sets-and-set-elements
   executing-aimms-procedures
   passing-errors-and-messages
   raising-and-handling-errors
   opening-and-closing-a-project
   thread-synchronization
   interrupts
   model-edit-functions