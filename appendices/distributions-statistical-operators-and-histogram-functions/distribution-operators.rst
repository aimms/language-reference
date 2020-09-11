.. _app:distribution.stat:

Distribution Operators
======================

.. rubric:: Distribution operators

The distribution operators discussed in this section can help you to
analyze the results of an experiment. For example, it is expected that
the sample mean of a sequence of observations gets closer to the mean of
the distribution that was used during the observations as the number of
observations increases. To compute statistics over a sample, you can use
the sample operators discussed in :ref:`app:sample.stat` or you can use
the histogram functions that are explained in :ref:`sec:gui.histogram`
of the Language Reference. The following distribution operators are
available in AIMMS:

-  the ``DistributionCumulative(distr,x)`` operator,

-  the ``DistributionInverseCumulative(distr,\alpha)`` operator,

-  the ``DistributionDensity(distr,x)`` operator,

-  the ``DistributionInverseDensity(distr,\alpha)`` operator,

-  the ``DistributionMean(distr)`` operator,

-  the ``DistributionDeviation(distr)`` operator,

-  the ``DistributionVariance(distr)`` operator,

-  the ``DistributionSkewness(distr)`` operator, and

-  the ``DistributionKurtosis(distr)`` operator.

.. rubric:: Cumulative distributions :math:`\ldots`

``DistributionCumulative(distr,x)`` computes the probability that a
random variable :math:`X` drawn from the distribution *distr* is less or
equal than :math:`x`. Its inverse,
``DistributionInverseCumulative( distr,\alpha)``, computes the smallest
:math:`x` such that the probability that a variable :math:`X` is greater
than or equal to :math:`x` does not exceed :math:`\alpha`.

.. rubric:: :math:`\ldots` and their derivatives

The ``DistributionDensity(distr,x)`` expresses the expected density
around :math:`x` of sample points drawn from a *distr* distribution and
is in fact the derivative of ``DistributionCumulative( distr,x)``. The
``DistributionInverseDensity(distr,\alpha)`` is the derivative of
``DistributionInverseCumulative( distr,\alpha)``. Given a random
variable :math:`X`, the :any:`DistributionInverseDensity` can be used to
answer the question of how much a given value :math:`x` should be
increased such that the probability :math:`P(X \leq x)` is increased
with :math:`\alpha` (for small values of :math:`\alpha`).

.. rubric:: :math:`\ldots` for discrete distributions

For continuous distributions *distr*, :math:`\alpha \in [0,1]`, and
:math:`x = {$\texttt{DistributionInverseCumulative}$}(distr,\alpha)`, it
holds that

.. math::

   \begin{aligned}
       {\texttt{DistributionDensity}}(distr,x) & = \partial \alpha / \partial x \\
       {\texttt{DistributionInverseDensity}}(distr,\alpha) & = \partial x / \partial \alpha\end{aligned}

Note that the above two relations make it possible to express
:any:`DistributionInverseDensity` in terms of :any:`DistributionDensity`.
Through this relation the :any:`DistributionInverseDensity` is also defined
for discrete distributions.

.. rubric:: Distribution statistics

The operators :any:`DistributionMean`, :any:`DistributionDeviation`,
:any:`DistributionVariance`, :any:`DistributionSkewness` and
:any:`DistributionKurtosis` provide the mean, standard deviation, variance,
skewness and kurtosis of a given distribution. Note that the values
computed using the sample operators converges to the values computed
using the corresponding distribution operators as the size of the sample
increases (the law of large numbers).