.. _sec:gui.histogram:

Creating Histograms
===================

.. rubric:: Histogram

The term histogram typically refers to a picture of a number of
observations. The observations are divided over equal-length intervals,
and the number of observed values in each interval is counted. Each
count is referred to as a frequency, and the corresponding interval is
called a frequency interval. The picture of a number of observations is
then constructed by drawing, for each frequency interval, the
corresponding frequency as a bar. A histogram can thus be viewed as a
bar chart of frequencies.

.. rubric:: Histogram support

The procedures and functions discussed in this section allow you to
create histograms based on a large number of trials in an experiment
conducted from within your model. You can set up such an experiment by
making use of random data for each trial drawn from one or more of the
distributions discussed in the AIMMS Language Reference. The histogram
frequencies, created through the functions and procedures discussed in
this section, can be displayed graphically using the standard AIMMS bar
chart object.

.. rubric:: Histogram functions and procedures

AIMMS provides the following procedure and functions for creating and
computing histograms.

-  :any:`HistogramCreate`\ (*histogram-id*\ [,\ *integer-histogram*][,\ *sample-buffer-size*])

-  :any:`HistogramDelete`\ (*histogram-id*)

-  :any:`HistogramSetDomain`\ (*histogram-id*,\ *intervals*\ [,\ *left*,\ *width*][,\ *left-tail*][,\ *right-tail*])

-  :any:`HistogramAddObservation`\ (*histogram-id*,\ *value*)

-  :any:`HistogramAddObservations`\ (*histogram-id*,\ *values-parameter*)

-  :any:`HistogramGetFrequencies`\ (*histogram-id*,\ *frequency-parameter*)

-  :any:`HistogramGetBounds`\ (*histogram-id*,\ *left-bound*,\ *right-bound*)

-  :any:`HistogramGetObservationCount`\ (*histogram-id*)

-  :any:`HistogramGetAverage`\ (*histogram-id*)

-  :any:`HistogramGetDeviation`\ (*histogram-id*)

-  :any:`HistogramGetSkewness`\ (*histogram-id*)

-  :any:`HistogramGetKurtosis`\ (*histogram-id*)

The *histogram-id* argument assumes an integer value. The arguments
*frequency-parameter*, *left-bound* and *right-bound* must be one-
dimensional parameters (defined over a set of intervals declared in your
model). The optional arguments *integer-histogram* (default 0),
*left-tail* (default 1) and *right-tail* (default 1) must be either 0 or
1. The optional argument *sample-buffer-size* must be a positive
integer, and defaults to 512.

.. rubric:: Creating and deleting histograms

Through the procedures :any:`HistogramCreate` and :any:`HistogramDelete` you
can create and delete the internal data structures associated with each
individual histogram in your experiment. Upon success, the procedure
:any:`HistogramCreate` passes back a unique integer number, the
*histogram-id*. This reference is required in the remaining procedures
and functions to identify the histogram at hand. The observations
corresponding to a histogram can be either continuous or integer-valued.
AIMMS assumes continuous observations by default. Through the optional
*integer-histogram* argument you can indicate that the observations
corresponding to a histogram are integer-valued.

.. rubric:: Sample buffer size

For every histogram, AIMMS will allocate a certain amount of memory for
storing observations. By default, AIMMS allocates space to store samples
of 512 observations at most. Using the optional *sample-buffer-size*
argument, you can override the default maximum sample size. As long as
the number of observations is still smaller than the sample buffer size,
all observations will be stored individually. As soon as the actual
number of observations exceeds the sample buffer size, AIMMS will no
longer store the individual observations. Instead, all observations are
then used to determine the frequencies of frequency intervals. These
intervals are determined on the basis of the sample collected so far,
unless you have specified interval ranges through the procedure
:any:`HistogramSetDomain`.

.. rubric:: Setting the interval domain

You can use the function :any:`HistogramSetDomain` to define frequency
intervals manually. You do so by specifying

-  the number of fixed-width *intervals*,

-  the lower bound of the *left*-most interval (not including a
   left-tail interval) together with the (fixed) *width* of intervals to
   be created (optional),

-  whether a *left-tail* interval must be created (optional), and

-  whether a *right-tail* interval must be created (optional).

The default for the *left* argument is ``-INF``. *Note that the left
argument is ignored unless the width argument is strictly greater than
0*. Note that the selection of one or both of the tail intervals causes
a corresponding increase in the number of frequency intervals to be
created.

.. rubric:: Use of tail intervals

Whenever an observed value is smaller than the lower bound of the
left-most fixed-width interval, AIMMS will update the frequency count of
the left-tail interval. If the left-tail interval is not present, then
the observed value is lost and the procedure :any:`HistogramAddObservation`
and :any:`HistogramAddObservations` (to be discussed below) will have a
return value of 0. Similarly, AIMMS will update the frequency count of
the right-tail interval, when an observation lies beyond the right-most
fixed-width interval.

.. rubric:: Adjusting the interval domain

Whenever, during the course of an experiment, the number of added
observations is still below the sample buffer size, you are allowed to
modify the interval ranges. As soon as the number of observations
exceeds the sample buffer size, AIMMS will have fixed the settings for
the interval ranges, and the function :any:`HistogramSetDomain` will fail.
This function will also fail when previous observations cannot be placed
in accordance with the specified interval ranges.

.. rubric:: Adding observations

You can use the procedure :any:`HistogramAddObservation` to add a new
observed value (or :any:`HistogramAddObservations` to add a set of values)
to a histogram. Non-integer observations for integer-valued histograms
will be rounded to the nearest integer value. The procedure will fail,
if the observed value cannot be placed in accordance with the specified
interval ranges.

.. rubric:: Obtaining frequencies

With the procedure :any:`HistogramGetFrequencies`, you can request AIMMS to
fill a one-dimensional parameter (slice) in your model with the observed
frequencies. The cardinality of the index domain of the frequency
parameter must be at least as large as the total number of frequency
intervals (including the tail interval(s) if created). The first element
of the domain set is associated with the left-tail interval, if created,
or else the left-most fixed-width interval.

.. rubric:: Interval determination

If you have provided the number of intervals through the procedure
:any:`HistogramSetDomain`, AIMMS will create this number of frequency
intervals plus at most two tail intervals. Without a custom-specified
number of intervals, AIMMS will create 16 fixed-width intervals plus two
tail intervals. If you have not provided interval ranges, AIMMS will
determine these on the basis of the collected observations. As long as
the sample buffer size of the histogram has not yet been reached, you
are still allowed to modify the number of intervals prior to any
subsequent call to the procedure :any:`HistogramGetFrequencies`.

.. rubric:: Obtaining interval bounds

Through the procedure :any:`HistogramGetBounds` you can obtain the left and
right bound of each frequency interval. The bound parameters must be
one-dimensional, and the cardinality of the corresponding domain set
must be at least the number of intervals (including possible left- and
right-tail intervals). The lower bound of a left-tail interval will be
``-INF``, the upper bound of a right-tail interval will be ``INF``.

.. rubric:: Obtaining statistical information

The following functions provided statistical information:

-  :any:`HistogramGetObservationCount` The total number of observations,

-  :any:`HistogramGetAverage` the arithmetic mean,

-  :any:`HistogramGetDeviation` standard deviation,

-  :any:`HistogramGetSkewness` skewness, and

-  :any:`HistogramGetKurtosis` kurtosis coefficient.

.. rubric:: Example

In the following example, a number of observable outputs ``o`` of a
mathematical program are obtained as the result of changes in a single
uniformly distributed input parameter ``InputRate``. The interval range
of every histogram is set to the interval [0,100] in 10 steps, and it is
assumed that the set associated with index ``i`` has at least 12
elements.

.. code-block:: aimms

	for (o) do
	    HistogramCreate( HistogramID(o) );
	    HistogramSetDomain( HistogramID(o), intervals: 10, left: 0.0, width: 10.0 );
	endfor;

	while ( LoopCount <= TrialSize ) do
	    InputRate := Uniform(0,1);
	    solve MathematicalProgram;
	    for (o) do
	        HistogramAddObservation( HistogramID(o), ObservableOutput(o) );
	    endfor;
	endwhile;

.. code-block:: aimms

	for (o) do
	    HistogramGetFrequencies( HistogramID(o), Frequencies(o,i) );
	    HistogramGetBounds( HistogramID(o), LeftBound(o,i), RightBound(o,i) );
	    HistogramDelete( HistogramID(o) );
	endfor;