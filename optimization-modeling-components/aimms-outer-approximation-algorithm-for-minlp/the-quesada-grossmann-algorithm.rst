The Quesada-Grossmann Algorithm
===============================

.. rubric:: One MIP problem

Quesada and Grossmann (:cite:`bib:QG92`) noticed that the classic outer
approximation algorithm often spends a large amount of time in solving
the MIP problems in which a significant amount of rework is done. They
proposed an algorithm in which only one MIP problem is solved. The
algorithm implemented in AIMMS uses a callback procedure for lazy
constraints which is supported by modern MIP solvers like CPLEX and
GUROBI.

.. rubric:: Convex models

The Quesada-Grossmann algorithm is designed to solve convex MINLP
models. The basic outer approximation algorithm can also be used to
solve convex models by using the parameter ``IsConvex``, but the
Quesada-Grossmann algorithm is often more efficient. The
Quesada-Grossmann algorithm is also available in the
``GMP Outer Approximation`` module.

.. rubric:: Calling procedure

The procedure ``DoConvexOuterApproximation`` inside the module
implements the Quesada-Grossmann algorithm. This procedure is called in
the same way as the ``DoOuterApproximation`` procedure of
:ref:`sec:aoa.using.algorithm`, which implements the basic algorithm.
The following control parameters in :ref:`this table <table:aoa.controlparam>` can
be used to influence the Quesada-Grossmann algorithm: ``TimeLimit``,
``CreateStatusFile``, ``UsePresolver`` and
``RelativeOptimalityTolerance``.