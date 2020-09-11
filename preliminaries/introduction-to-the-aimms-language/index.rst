.. _chap:intro:

Introduction to the AIMMS Language
==================================

.. rubric:: Example makes a good starting point

This chapter discusses a simple but complete modeling example containing
the most common components of a typical AIMMS application. The aim is to
give a quick feel for the language, and to assist you to form a mental
picture of its functionality.

.. rubric:: Familiarity with algebraic notation

It is assumed that you are familiar with some basic algebraic notation.
It is important that you understand the notions of "summation,"
"simultaneous equations in many variables (unknowns)," and "minimizing
or maximizing an objective function, subject to constraints." If you are
not acquainted with these notions, refer to the book *AIMMS-Optimization
Modeling*.

.. rubric:: What to expect in this chapter

This chapter uses a simple depot location problem to introduce the basic
AIMMS concepts necessary to formulate and solve the model. The task
consists of the following steps.

-  :ref:`sec:intro.decl` describes the depot location problem,
   introduces the set notation, and illustrates how sets can be used to
   declare multidimensional identifiers useful for modeling the problem
   in AIMMS.

-  :ref:`sec:intro.model` discusses the formulation of a mathematical
   program that can be used to compute the optimal solution of the
   problem.

-  :ref:`sec:intro.expressions` briefly discusses data initialization,
   and explains how data can be entered.

-  :ref:`sec:intro.proc` illustrates how you can use flow control
   statements in AIMMS to formulate an algorithm for solving your
   problems in advanced ways.

-  :ref:`sec:intro.tips` discusses issues to consider when working with
   more complex models.

.. toctree::
   :maxdepth: 1

   the-depot-location-problem
   formulation-of-the-mathematical-program
   data-initialization
   an-advanced-model-extension
   general-modeling-tips