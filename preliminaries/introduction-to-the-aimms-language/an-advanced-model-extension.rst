.. _sec:intro.proc:

An Advanced Model Extension
===========================

.. rubric:: This section

In this section a single procedure is developed to illustrate the use of
execution control structures in AIMMS. It demonstrates a customized
solution approach to solve the depot location problem subject to
fluctuations in demand. Understanding the precise algorithm described in
this section requires more mathematical background than was required for
the previous sections. However, even without this background the
examples in this section may provide you with a basic understanding of
the capabilities of AIMMS to manipulate its data and control the flow of
execution.

.. rubric:: Finding a robust solution

The mathematical program developed in :ref:`sec:intro.decl` does not
take into consideration any fluctuations in customer demand. Selecting
the depots on the basis of a single demand scenario may result in
insufficient capacity under changing demand requirements. While there
are several techniques to determine a solution that remains robust under
fluctuations in demand, we will consider here a customized solution
approach for illustrative purposes.

.. rubric:: Algorithm in words

The overall structure of the algorithm can be captured as follows.

-  During each major iteration, the algorithm adds a single new depot to
   a set of already permanently selected depots.

-  To determine a new depot, the algorithm solves the depot location
   model for a fixed number of scenarios sampled from normal demand
   distributions. During these runs, the variable ``DepotSelected(d)``
   is fixed to 1 for each depot ``d`` in the set of already permanently
   selected depots.

-  The (nonpermanent) depot for which the highest selection frequency
   was observed in the previous step is added to the set of permanently
   selected depots.

-  The algorithm terminates when there are no more depots to be selected
   or when the total capacity of all permanently selected depots first
   exceeds the average total demand incremented with the observed
   standard deviation in the randomly selected total demand.

.. rubric:: Additional identifiers

In addition to all previously declared identifiers the following
algorithmic identifiers will also be needed:

-  the set ``SelectedDepots``, a subset of the set ``Depots``, holding
   the already permanently selected depots, as well as

-  the parameters ``AverageDemand(c)``, ``DemandDeviation(c)``,
   ``TotalAverageDemand``, ``NrOfTrials``, ``DepotSelectionCount(d)``,
   ``CapacityOfSelectedDepots``, ``TotalSquaredDemandDifference`` and
   ``TotalDemandDeviation``.

The meaning of these identifiers is either self-explanatory or will
become clear when you study the further specification of the algorithm.

.. rubric:: Outline of algorithm

At the highest level you may view the algorithm described above as a
single initialization block followed by a ``WHILE`` statement containing
a reference to two additional execution blocks. The corresponding
outline is as follows.

.. code-block:: aimms

	<<Initialize algorithmic parameters>>

	while ( Card(SelectedDepots) < Card(Depots) and
	        CapacityOfSelectedDepots < TotalAverageDemand + TotalDemandDeviation ) do
	    <<Determine depot frequencies prior to selecting a new depot>>
	    <<Select a new depot and update algorithmic parameters>>
	endwhile;

The AIMMS function :any:`Card` determines the cardinality of a set, that is
the number of elements in the set.

.. rubric:: Initializing model parameters

The initialization blocks consists of assignment statements to give each
relevant set and parameter its initial value. Note that the assignments
indexed with ``d`` will be executed for every depot in the ``Depots``,
and no explicit ``FOR`` statement is required.

.. code-block:: aimms

	TotalAverageDemand           := Sum[ c, AverageDemand(c) ];

	SelectedDepots               := { };
	DepotSelectionCount(d)       := 0;
	CapacityOfSelectedDepots     := 0;

	TotalDemandDeviation         := 0;
	TotalSquaredDemandDifference := 0;

	DepotSelected.NonVar(d)      := 0;

.. rubric:: Explanation

With the exception of ``TotalAverageDemand``, all identifiers are
assigned their default value 0 or empty. This is superfluous the first
time the algorithm is called during a session, but is required for each
subsequent call. The value of global identifiers such as ``NrOfTrials``,
``AverageDemand(c)`` and ``DemandDeviation(c)`` must be set prior to
calling the algorithm.

.. rubric:: The ``.NonVar`` suffix

The suffix ``.NonVar`` indicates a nonvariable status. Whenever the
suffix ``DepotSelected.NonVar(d)`` is nonzero for a particular ``d``,
the corresponding variable ``DepotSelected(d)`` is considered to be a
parameter (and thus fixed inside a mathematical program).

.. rubric:: Determining depot frequencies

The AIMMS program that determines the depot frequencies prior to
selecting a new depot consists of just five statements.

.. code-block:: aimms

	while ( LoopCount <= NrOfTrials ) do
	    CustomerDemand(c) := Normal(AverageDemand(c), DemandDeviation(c));

	    Solve DepotLocationDetermination;

	    DepotSelectionCount(d | DepotSelected(d)) += 1;

	    TotalSquaredDemandDifference += Sum[ c, (CustomerDemand(c) - AverageDemand(c))^2 ];
	endwhile;

.. rubric:: Explanation

Inside the ``WHILE`` statement the following steps are executed.

-  Determine a demand scenario.

-  Solve the corresponding mathematical program.

-  Increment the depot selection frequency accordingly.

-  Register squared deviations from the average for total demand.

.. rubric:: Functions used

The operator ``LoopCount`` is predefined in AIMMS, and counts the number
of the current iteration in any of AIMMS' loop statements. Its initial
value is 1. The function :any:`Normal` is also predefined, and generates a
number from the normal distribution with known mean (the first argument)
and known standard deviation (the second argument). The operator ``+=``
increments the identifier on the left of it with the amount on the
right. The operator ``^`` represents exponentiation.

.. rubric:: Selecting a new depot

The AIMMS program to select a new depot and update the relevant
algorithmic parameters also consists of just five statements.

.. code-block:: aimms

	SelectedDepots           += ArgMax[ d | not d in SelectedDepots,
	                                    DepotSelectionCount(d) ];
	CapacityOfSelectedDepots := Sum[ d in SelectedDepots, DepotCapacity(d) ];

	TotalDemandDeviation     := Sqrt( TotalSquaredDemandDifference ) /
	                            (Card(SelectedDepots)*NrOfTrials) ;

	DepotSelected(d in SelectedDepots)        := 1;
	DepotSelected.NonVar(d in SelectedDepots) := 1;

.. rubric:: Explanation

In the above AIMMS program the following steps are executed.

-  Determine the not already permanently selected depot with the highest
   frequency, and increment the set of permanently selected depots
   accordingly.

-  Register the new current total capacity as the sum of all capacities
   of depots that have been permanently selected.

-  Register the new value of the estimated standard deviation in total
   demand.

-  Assign 1 to all permanently selected depots, and fix their
   nonvariable status accordingly.

.. rubric:: Functions used

The iterative operator ``ArgMax`` considers all relevant depots from its
first argument, and takes as its value that depot for which the
corresponding second arguments is maximal. The AIMMS function :any:`Sqrt`
denotes the well-known square root operation.