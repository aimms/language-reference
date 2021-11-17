.. _chap:eff:

Execution Efficiency Cookbook
=============================

.. rubric:: This chapter

Typically, when you start running your model with realistic, large-scale
data sets, execution performance becomes an important issue. In this
chapter, we discuss various techniques that you can use to improve the
execution efficiency of your model.

.. rubric:: Dividing the time spent

The running time of AIMMS applications can be divided in the time spent
by AIMMS itself and the time spent by the solution algorithms
(i.e. solvers) used by AIMMS.

.. rubric:: Time spent by solvers

The time used by the solvers mostly depends, apart from the quality of
the solver, on the specific formulation of the mathematical program to
be solved. Finding a formulation that can be efficiently solved is often
a challenging task and is beyond the scope of this chapter. For a
detailed discussion, you are referred to the extensive literature that
exists on this subject.

.. rubric:: Time spent by AIMMS

AIMMS itself typically spends most of its time on the execution of
assignment statements and the generation of constraints. This time
depends on several factors. A few of these factors are:

-  the size of the sets and the data set size used in your model,

-  the efficiency of the AIMMS execution engine, and

-  the language constructs used to formulate the execution statements
   and constraints.

.. rubric:: Understanding AIMMS execution

At AIMMS we are committed to continuously improving the efficiency of
the AIMMS execution engine and the AIMMS matrix generator. The
efficiency of your application, however, does not only depend on the
efficiency of AIMMS, but also on the specific formulation of your model
and the language constructs that you have used. A global understanding
of the AIMMS execution engine, as presented in :ref:`chap:sparse`, may
provide a good background on which to start reconsidering particular
formulations that lead to bottlenecks in execution performance in your
application.

.. rubric:: Analysis tools

In addition, AIMMS provides you with two tools for analyzing execution
bottlenecks, namely the **Identifier Cardinalities** and **Profiler**
tools. The use of both tools is described in :doc:`creating-and-managing-a-model/debugging-and-profiling-an-aimms-model/index`.

.. rubric:: Analyzing cardinalities

The **Identifier Cardinalities** tool can help you to discover
identifiers with a large number of elements. Such identifiers, when used
in statements and constraints, may lead to efficiency bottlenecks
throughout your model. Whenever you are able to reduce the number of
elements associated with such identifiers, by leaving out irrelevant
elements, the execution efficiency of your model will improve at several
places. Naturally, such reductions are not possible when all the
elements are relevant to the computation of the solution. In
:ref:`section:eff.reduc-elements`, we discuss two frequently observed
and effective approaches to reducing the number of elements in both
one-dimensional sets and multidimensional identifiers.

.. rubric:: Analyzing statements

With the AIMMS **Profiler** tool you can identify the individual
statements and constraints on which the AIMMS execution engine spends
most of its time. Even if the inefficiencies are not the result of
superfluous identifier cardinalities, it may still be possible to review
and rewrite such statements and constraints in order to improve the
execution efficiency of your application. In
:ref:`section:eff.tuning-stmts` we discuss potential bottlenecks and
alternative formulations for particular statements and constraints.

.. rubric:: Simple precautions

Before you begin tuning your application, you may want to set aside a
copy of the application and inputs with known results. You can then set
up a script that executes each of these tests using the AIMMS command
line option ``--run-only`` (see also :doc:`miscellaneous/calling-aimms/index`). 
In addition, you may wish to regularly commit your
sources to a version control system in order to track the changes you
make over time.

.. toctree::
   :maxdepth: 1

   reducing-the-number-of-elements
   analyzing-and-tuning-statements
   summary