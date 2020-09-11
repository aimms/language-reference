.. _sec:nlp.multistart:

The AIMMS Multistart Algorithm
==============================

.. rubric:: The multistart algorithm

A multistart algorithm calls an NLP solver from multiple starting
points, keeps track of (all) feasible solutions found by the NLP solver,
and reports back the best of these as its final solution.

.. rubric:: Why use multistart?

A multistart algorithm can improve the reliability of any NLP solver, by
calling it with many starting points. A single call to a NLP solver can
fail (return a status of infeasible), but multiple calls from the widely
spaced starting points provided by a multistart algorithm have a much
better chance of success.

.. rubric:: Basic techniques

In a pure multistart algorithm many local searches will converge to the
same local minimum. Computational effort can be reduced if the
minimizations leading to the same local minimum point can be identified
and combined at early stages. An improvement is to use cluster analysis
techniques to identify regions of points that will lead to the same
local minimum.

.. rubric:: Algorithm used by AIMMS

AIMMS uses a multistart algorithm that does not use advanced cluster
analysis techniques, but instead tries to identify areas of points that
will lead to the same local solution. These areas are updated (and
become larger) whenever a starting point is found that leads to a local
solution that has already been found before. An more detailed
description of a multistart algorithm similar to the one used by AIMMS
can be found in :cite:`bib:RKT87`.

.. rubric:: Definitions

The following terminology is used for the multistart algorithm

-  Sample points: a set of points that were randomly sampled.

-  Cluster point: a point that defines the center of a cluster, i.e., a
   cluster is a circle/ball with a cluster point as its center.

-  Starting point: a point used as an initial solution ("hotstart") for
   solving the NLP.

-  Local solution: a solution found by the NLP solver (by using a
   starting point). A local solution belongs to exactly one cluster
   point. A local solution can be infeasible.

.. rubric:: Two algorithms

The multistart module implements two algorithms, namely a basic
algorithm and a dynamic algorithm in which the number of iterations is
changed dynamically. The inputs for both algorithms are:

-  a GMP associated with an NLP,

-  ``NumberOfSamplePoints``, and

-  ``NumberOfSelectedSamplePoints``.

.. rubric:: The basic algorithm

The basic algorithm employs the following steps:

0. Set ``IterationCount`` equal to 1.

1. Generate ``NumberOfSamplePoints`` sample points from the uniform
   distribution. Calculate the penalized objective for all sample points
   and select the best ``NumberOfSelectedSamplePoints`` sample points.

2. For all sample points (``NumberOfSelectedSamplePoints`` in total) do:

   -  For all clusters, calculate the distance between the sample point
      and the center of the cluster. If the distance is smaller than the
      radius of the cluster (i.e., the sample point belongs to the
      cluster) then delete the sample point.

3. For all (remaining) sample points do:

   -  Solve the NLP by using the sample point as its starting point to
      obtain a candidate local solution.

   -  For all clusters do:

      -  Calculate the distance between the candidate local solution and
         the local solution belonging to the cluster.

      -  If the distance equals 0 (which implies that the candidate
         local solution is the same as the local solution belonging to
         the cluster) then update the center and radius of the cluster
         by using the sample point.

      -  Else, construct a new cluster by using the mean of the sample
         point and the candidate local solution as its center with
         radius equal to half the distance between these two points.
         Assign the candidate local solution as the local solution
         belonging to the cluster.

   -  For all remaining sample points, calculate the distance between
      the sample point and the center of the updated or the new cluster.
      If the distance is smaller than the radius of the cluster then
      delete the sample point.

4. Increment ``IterationCount``. If the number of iterations exceeds the
   ``IterationLimit``, then go to step (5). Else go to step (1).

5. Order the local solutions and store the ``NumberOfBestSolutions``
   solutions in the solution repository.

By default, the algorithm uses the initial variable values as the first
"sample" point in the first iteration.

.. rubric:: The dynamic algorithm: first phase

The dynamic algorithm contains two phases. The first phase is similar to
the basic algorithm but with some differences. The dynamic algorithm
starts by determining the best sampling box for the creation of the
random points (in step 0). For the first sample point, which can be an
initial point provided by the user or the first randomly generated
point, a method is applied to compute an approximately feasible solution
(see :cite:`bib:Ch04`) to increase the chance that this first sample point
will lead to a feasible solution. Finally, if the dynamic algorithm did
not find any feasible solution during the first iterations, and all
local solutions found contain large infeasibilities, then a heuristic
will be used to update the variable bounds (in step 4).

.. rubric:: The dynamic algorithm: second phase

The second phase of the dynamic algorithm is only conducted if no
feasible solution was found in the first phase, or if the objective
values of the feasible solutions found in the first phase vary. The
second phase differs for both situations. If no feasible solution was
found in the first phase then the algorithm will continue with steps 1
to 4 until a feasible solution is found or the time limit is hit. In
each iteration, the algorithm will now use the method for computing an
approximately feasible solution for the first randomly generated point.
In the other case, in which the objective values of the feasible
solutions found in the first phase vary, the second phase will continue
with steps 1 to 4 until enough feasible solutions are found to satisfy a
Bayesian estimate for the number of local feasible solutions (or if the
time limit is hit).

.. rubric:: Using the AIMMS multistart algorithm

The AIMMS multistart algorithm is implemented as a system module, with
the name ``Multi Start``, that you can add to your project. You can
install this module using the **Install System Module** command in the
AIMMS **Settings** menu. The algorithm outlined above is implemented in
the AIMMS language. Some supporting functions that are computationally
difficult, or hard to express in the AIMMS language, have been added to
the GMP library in support of the AIMMS multistart algorithm.

.. rubric:: Calling the multistart algorithm

The main procedure to start the multistart algorithm is the procedure
``DoMultiStart``. The only mandotory input is a generated mathematical
program obtained by calling the :any:`GMP::Instance::Generate` function of
the GMP library discussed in :ref:`sec:gmp.instance`. Therefore the
multistart algorithm can be called by using for example:

.. code-block:: aimms

	MulStart::DoMultiStart( myGMP );

Here ``MulStart`` is the prefix of the multistart module. The behavior
of the multistart algorithm is influenced by several control parameters,
which are discussed in :ref:`sec:multistart.control.par`.

.. rubric:: Optional arguments

The procedure ``DoMultiStart`` contains two optional arguments (with a
default value of 0) which can be used to specify the number of sample
points and the number of selected sample points (as outlined above). If
both arguments are not specified (like in the example of the previous
paragraph) or are equal to 0, then the multistart algorithm will use the
dynamic algorithm, and otherwise the basic algorithm. For example, if

.. code-block:: aimms

	MulStart::DoMultiStart( myGMP, 20, 10 );

is used then the basic algorithm will be used with 20 sample points and
10 selected sample points. If the dynamic algorithm is used then the
multistart algorithm will automatically select values for the number of
sample points and the number of selected sample points. It is possible
to use the dynamic algorithm and specify the number of sample points and
the number of selected sample points yourself by calling the procedure
``DoMultiStartDynamic``.

.. rubric:: Supporting GMP functions

The GMP library contains the following functions to support the
multistart algorithm:

-  :any:`GMP::Solution::RandomlyGenerate` (used in step (1))

-  :any:`GMP::Solution::GetPenalizedObjective` (used in step (1))

-  :any:`GMP::Solution::GetDistance` (used in steps (2) and (4))

-  :any:`GMP::Solution::ConstructMean` (used in step (4))

-  :any:`GMP::Solution::UpdatePenaltyWeights` (used during initialization)

Optionally it is possible to (approximately) project each sample point
to the feasible region by using the procedure
:any:`GMP::Instance::FindApproximatelyFeasibleSolution`.

.. rubric:: Modifying the algorithm

Because the multistart algorithm is written in the AIMMS language, you
have complete freedom to modify the algorithm in order to tune it for
your nonlinear programs.