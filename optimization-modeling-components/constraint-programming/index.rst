.. _chap:constraint.programming:

Constraint Programming
======================

.. rubric:: Introduction

Constraint Programming is a relatively new paradigm used to model and
solve combinatorial optimization problems. It is most effective on
highly combinatorial problem domains such as timetabling, sequencing,
and resource-constrained scheduling. Successful industrial applications
utilizing constraint programming technology include the gate allocation
system at Hong Kong airport, the yard planning system at the port of
Singapore, and the train timetable generation of Dutch Railways.

.. rubric:: Constraint Programming in AIMMS

This chapter discusses the special identifier types and language
constructs that AIMMS offers for formulating and solving constraint
programming problems. We will see that constraint programming offers a
much wider range of modeling constructs than, for example, integer
linear programming or nonlinear programming. Different variable types
can be used, while restrictions can be formed using arbitrary algebraic
and logical expressions or by the use of special constraint types, such
as alldifferent. In addition, AIMMS offers a specific syntax to express
scheduling problems in an intuitive way, taking advantage of the
algorithmic power that underlies constraint-based scheduling.

.. rubric:: This chapter

In this chapter, the basic constraint programming concepts are first
presented, including different variable types and restrictions in
:ref:`sec:constraint.programming.essentials`.
:ref:`sec:cp.scheduling.problems` discusses the AIMMS syntax for
modeling constraint-based scheduling problems. The final section of this
chapter discusses issues related to modeling and solving constraint
programs in AIMMS.

.. rubric:: Literature

An in-depth discussion on constraint programming is given in :cite:`bib:cp_handbook`
and more details on constraint-based scheduling can be found in
:cite:`bib:baptiste2001`.

.. rubric:: Online resources

First, the Association for Constraint Programming organizes an annual
summer school, the material for which is posted online. This material
can be accessed at ``http://4c.ucc.ie/a4cp/``. The CPAIOR conference
series organizes tutorials alongside each event, the materials of which
are posted online. The CPAIOR 2009 tutorial provides an introduction to
constraint programming and hybrid methods, and available online at
``http://www.tepper.cmu.edu/cpaior09``.

.. toctree::
   :maxdepth: 1

   constraint-programming-essentials
   scheduling-problems
   modeling-solving-and-searching