.. _sec:time.rolling:

Implementing a Model with a Rolling Horizon
===========================================

.. rubric:: Rolling horizons

The term *rolling horizon* is used to indicate that a time-dependent
model is solved repeatedly, and in which the planning interval is moved
forward in time during each solution step. With the facilities
introduced in the previous sections setting up such a model is
relatively easy. This section outlines the steps that are required to
implement a model with a rolling horizon, without going into detail
regarding the contents of the underlying model.

.. rubric:: Two strategies

In this section you will find two strategies for implementing a rolling
horizon. One is a simple strategy that will only work with certain
restrictions. It requires just a single aggregation step and a single
disaggregation step. The other is a generic strategy that will work in
all cases. This strategy, however, requires that aggregation and
disaggregation steps be performed between every two subsequent ``SOLVE``
statements.

.. rubric:: Simple strategy

The simple strategy will work provided that

-  all periods in the horizon are of equal length, and

-  the horizon rolls from period boundary to period boundary.

It is then sufficient to make the horizon sufficiently large so as to
cover the whole time range of interest.

.. rubric:: Algorithm outline

The algorithm to implement the rolling horizon can be outlined as
follows.

#. Select the current time slot and period, and create the global
   timetable.

#. Aggregate all calendar-based data into horizon-based data.

#. Solve the optimization model for a planning interval that is a subset
   of the complete horizon.

#. Move the current period to the next period boundary of interest, and
   repeat from steps until the time range of interest has passed.

#. Disaggregate the horizon-based solution into a calendar-based
   solution.

.. rubric:: Assumptions

The examples below that illustrate both the simple and generic strategy
make the following assumptions.

-  The model contains the daily calendar ``DailyCalendar``, the horizon
   ``ModelPeriods`` and the timetable ``TimeTable`` declared in
   :ref:`sec:time.calendar`, :ref:`sec:time.horizon` and
   :ref:`sec:time.timetable`, respectively.

-  The model contains a time-dependent mathematical program
   ``TimeDependentModel``, which produces a plan over the planning
   interval associated with ``ModelPeriods``.

-  The planning horizon, for which the model is to be solved, rolls
   along from ``FirstWeekBegin`` to ``LastWeekBegin`` in steps of one
   week. Both identifiers are element parameters in ``DailyCalendar``.

.. rubric:: Code outline

The outline of the simple strategy can be implemented as follows.

.. code-block:: aimms

	CurrentDay := FirstWeekBegin;
	CreateTimeTable( TimeTable   , CurrentDay     , IntervalStart,
	                 PeriodLength, LengthDominates,
	                 InactiveDays, DelimiterDays  );

	Aggregate( DailyDemand, Demand, TimeTable, 'summation' );
	! ... along with any other aggregation required

	repeat
	    solve TimeDependentModel;

	    CurrentDay    += 7;
	    IntervalStart += 1;

	    break when (not CurrentDay) or (CurrentDay > LastWeekBegin);
	endrepeat;

	Disaggregate( Stock     , DailyStock     , TimeTable, 'interpolation', locus: 1 );
	Disaggregate( Production, DailyProduction, TimeTable, 'summation' );
	! ... along with any other disaggregation required

.. rubric:: Generic strategy

The simple strategy will not work

-  whenever the lengths of periods in the horizon (expressed in time
   slots of the calendar) vary, or

-  when the start of a new planning interval does not align with a
   future model period.

In both cases, the horizon-based solution obtained from a previous solve
will not be accurate when you move the planning interval. Thus, you
should follow a generic strategy which adds an additional disaggregation
and aggregation step to every iteration.

.. rubric:: Algorithm outline

The generic strategy for implementing a rolling horizon is outlined as
follows.

#. Select the initial current time slot and period, and create the
   initial timetable.

#. Aggregate all calendar-based data into horizon-based data.

#. Solve the mathematical program.

#. Disaggregate all horizon-based variables to calendar-based
   identifiers.

#. Move the current time slot forward in time, and recreate the
   timetable.

#. Aggregate all identifiers disaggregated in step 4 back to the horizon
   using the updated timetable.

#. Repeat from step 2 until the time range of interest has passed.

.. rubric:: Code outline

The outline of the generic strategy can be implemented as follows.

.. code-block:: aimms

	CurrentDay := FirstWeekBegin;
	CreateTimeTable( TimeTable   , CurrentDay     , IntervalStart,
	                 PeriodLength, LengthDominates,
	                 InactiveDays, DelimiterDays  );

	repeat
	    Aggregate( DailyDemand, Demand, TimeTable, 'summation' );
	    ! ... along with any other aggregation required

	    solve TimeDependentModel;

	    Disaggregate( Stock     , DailyStock     , TimeTable, 'interpolation', locus: 1 );
	    Disaggregate( Production, DailyProduction, TimeTable, 'summation' );
	    ! ... along with any other disaggregation required

	    CurrentDay += 7;
	    break when (not CurrentDay) or (CurrentDay > LastWeekBegin);
	    CreateTimeTable( TimeTable   , CurrentDay     , IntervalStart,
	                     PeriodLength, LengthDominates,
	                     InactiveDays, DelimiterDays  );

	    Aggregate( DailyStock     , Stock     , TimeTable, 'interpolation', locus: 1 );
	    Aggregate( DailyProduction, Production, TimeTable, 'summation' );
	    ! ... along with any other aggregation required
	endrepeat;