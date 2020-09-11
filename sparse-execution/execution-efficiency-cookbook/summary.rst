Summary
=======

.. rubric:: The recipe boils down to three steps

This chapter consists of a recipe for fine tuning an existing AIMMS
application such that AIMMS more efficiently executes the definitions
and statements and efficiently generates the constraints. The recipe
consists of the following three steps:

-  First, construct active subsets by removing all elements for which
   the variables are fixed in advance. These active subsets should then
   be used throughout your core model. This reduces the work each time,
   even in the evaluation of the index domain conditions to be
   constructed next.

-  Second, construct index domain conditions for the parameters,
   variables, and constraints of the core model. This will make several
   dense expressions seemingly execute more sparse, because only a
   limited number of elements are evaluated. Especially with variables
   and constraints this avoids the generation of columns for fixed
   variables and empty constraints. Thus the number of bottlenecks in
   your application is further reduced.

-  Finally, use the AIMMS profiler to pinpoint those assignment
   statements, ``FOR`` loops, and constraints that still absorb a
   considerable amount of computation time, and analyze and possible
   modify them. A checklist that can be used for this analysis has been
   presented in :ref:`section:eff.tuning-stmts`.