.. _app:distribution:

Distributions, Statistical Operators and Histogram Functions
============================================================

.. rubric:: This chapter
   :name: stat.func

This chapter provides a more elaborate description of the distributions
and distribution and sample operators listed in
:numref:`table:expr.distrib`, :numref:`table:expr.stat-iter` and
:numref:`table:expr.distrib-oper`. You can use this information when you
want to set up an experiment around your (optimization-based) AIMMS
model.

.. rubric:: Description of distributions

For each of the available distributions we describe

-  its parameters, mean and variance,

-  the unit relationship between its parameters and result,

-  its shape, and

-  its typical use in applications.

Such information may be useful in the selection and use of a
distribution to describe the particular statistical behavior of input
data of experiments that you want to perform on top of your model.
However, a general guideline for choosing the right might be in order
and is provided in the next paragraph.

.. rubric:: Choosing the right distribution

Whenever your experiment counts a number of occurrences, you should
first make a distinction between experiments with replacement
(i.e. throwing dice), experiments without replacement (i.e. drawing
cards from a deck), or experiments in which independent occurrences take
place at random moments (i.e. customers appearing at a desk). Having
made this distinction, :ref:`tb:app.discr_distributions` will help you
to select the right distribution for your experiment. In any other case
the :any:`Normal` distribution should be considered first. Although this
distribution is unbounded, it is declining so rapidly that it can often
be used even when the result should be bounded. If the :any:`Normal`
distribution does not suffice, the primary selection criterium is
existence of bounds: AIMMS provides the user with distributions with no
bounds, one (lower) bound and two (upper and lower) bounds. See
:ref:`app:distribution.cont` (continuous distributions) for details.

.. rubric:: Description of distribution operators

For each of the available distribution and sample operators we provide

-  the interpretation of its result, and

-  the formula for the computation of the operator.

Such information may be useful when you want to perform an analysis of
the results of your experiments.

.. rubric:: Option for backward compatibility

All distribution operators that are listed in
:ref:`app:distribution.stat` have been introduced in AIMMS 3.4, although
the :any:`DistributionCumulative` and :any:`DistributionInverseCumulative`
operator were already available under the names
``CumulativeDistribution`` and ``InverseCumulativeDistribution``,
respectively. Furthermore, in order to obtain a consistent set of
distribution functions the prototype for some of them has been slightly
adapted. :ref:`app:distribution.cont` discusses the function prototype
of the continuous distribution functions in full detail. Both the old
and the new function prototypes are discussed in the AIMMS Function
Reference. To make sure that models using distribution functions and
developed in an older version of AIMMS are working correctly, you should
set the option ``Distribution_compatibility`` to '``AIMMS 3.0``'.

.. toctree::
   :maxdepth: 1

   discrete-distributions
   continuous-distributions
   distribution-operators
   sample-operators
   scaling-of-statistical-operators
   creating-histograms