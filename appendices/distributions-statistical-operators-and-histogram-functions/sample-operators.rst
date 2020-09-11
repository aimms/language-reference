.. _app:sample.stat:

Sample Operators
================

.. rubric:: Sample operators

The statistical sample operators discussed in this section can help you
to analyze the results of an experiment. The following operators are
available in AIMMS:

-  the ``Mean`` operator,

-  the ``GeometricMean`` operator,

-  the ``HarmonicMean`` operator,

-  the ``RootMeanSquare`` operator,

-  the ``Median`` operator,

-  the ``SampleDeviation`` operator,

-  the ``PopulationDeviation`` operator,

-  the ``Skewness`` operator,

-  the ``Kurtosis`` operator,

-  the ``Correlation`` operator, and

-  the ``RankCorrelation`` operator.

.. rubric:: Associated units

The results of the ``Skewness``, ``Kurtosis``, ``Correlation`` and
``RankCorrelation`` operator are unitless. The results of the other
sample operators listed above should have the same unit of measurement
as the expression on which the statistical computation is performed.
Whenever your model contains one or more ``QUANTITY`` declarations,
AIMMS will perform a unit consistency check on arguments of the
statistical operators and their result.

.. _mean:

.. _geometricmean:

.. _harmonicmean:

.. _rootmeansquare:

.. rubric:: Mean

The following mean computation methods are supported: (arithmetic) mean
or average, geometric mean, harmonic mean and root mean square (RMS).
The first method is well known and has the property that it is an
unbiased estimate of the expectation of a distribution. The geometric
mean is defined as the :math:`N`-th root of the product of :math:`N`
values. The harmonic mean is the reciprocal of the arithmetic mean of
the reciprocals. The root mean square is defined as the square root of
the arithmetic mean of the squares. It is mostly used for averaging the
measurements of a physical process.

.. table:: 

	============ ======================================
	**Operator** ``Mean``\ (*domain*,\ *expression*)
	**Formula**  :math:`\frac{1}{n} \sum_{i=1}^{n} x_i`
	============ ======================================
	
.. table:: 

	============ =====================================================
	**Operator** ``GeometricMean``\ (*domain*,\ *expression*)
	**Formula**  :math:`\sqrt[{\displaystyle n}]{\prod_{i=1}^{n} x_i}`
	============ =====================================================
	
.. table:: 

	+--------------+--------------------------------------------------------------------------------+
	| **Operator** | ``HarmonicMean``\ (*domain*,\ *expression*)                                    |
	+--------------+--------------------------------------------------------------------------------+
	| **Formula**  | :math:`\frac{{\displaystyle n}}{{\displaystyle \sum_{i=1}^{n} \frac{1}{x_i}}}` |
	+--------------+--------------------------------------------------------------------------------+
	
.. table:: 

	============ ===================================================
	**Operator** ``RootMeanSquare``\ (*domain*,\ *expression*)
	**Formula**  :math:`\sqrt{\frac{1}{n} \sum_{i=1}^{n} x_{i}^{2}}`
	============ ===================================================
	
.. _median:

.. rubric:: Median

The median is the middle value of a sorted group of values. In case of
an odd number of values the median is equal to the middle value. If the
number of values is even, the median is the mean of the two middle
values.

.. table:: 

	+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| **Operator** | ``Median``\ (*domain*,\ *expression*)                                                                                                                                                                                                    |
	+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`{median} = \left\{ \begin{array}{ll} x_{\frac{N + 1}{2}} & \; \; \mbox{if} \; N \; \mbox{is odd} \\ \frac{1}{2} \left( x_{\frac{N}{2}} + x_{\frac{N + 2}{2}} \right)& \;\; \mbox{if} \; N \; \mbox{is even} \end{array} \right\}` |
	+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	
.. _sampledeviation:

.. _populationdeviation:

.. rubric:: Standard deviation

The standard deviation is a measure of dispersion about the mean. It is
defined as the root mean square of the distance of a set of values from
the mean. There are two kinds of standard deviation: the standard
deviation of a sample of a population, also known as
:math:`\sigma_{n-1}` or :math:`s`, and the standard deviation of a
population, which is denoted by :math:`\sigma_n`. The relation between
these two standard deviations is that the first kind is an unbiased
estimate of the second kind. This implies that for large :math:`n`
:math:`\sigma_{n-1} \approx \sigma_n`. The standard deviation of an
sample of a population can be computed by means of

.. table:: 

	+--------------+---------------------------------------------------------------------------------------------------------------------------+
	| **Operator** | ``SampleDeviation``\ (*domain*,\ *expression*)                                                                            |
	+--------------+---------------------------------------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`\sqrt{ \frac{1}{n-1} \left( \sum_{i=1}^{n} x_{i}^{2} - \frac{1}{n} {\left( \sum_{i=1}^{n} x_i \right)}^2 \right)}` |
	+--------------+---------------------------------------------------------------------------------------------------------------------------+
	
whereas the standard deviation of a population can be determined by

.. table:: 

	+--------------+-------------------------------------------------------------------------------------------------------------------------+
	| **Operator** | ``PopulationDeviation``\ (*domain*,\ *expression*)                                                                      |
	+--------------+-------------------------------------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`\sqrt{ \frac{1}{n} \left( \sum_{i=1}^{n} x_{i}^{2} - \frac{1}{n} {\left( \sum_{i=1}^{n} x_i \right)}^2 \right)}` |
	+--------------+-------------------------------------------------------------------------------------------------------------------------+
	
.. _skewness:

.. rubric:: Skewness

The skewness is a measure of the symmetry of a distribution. Two kinds
of skewness are distinguished: positive and negative. A positive
skewness means that the tail of the distribution curve on the right side
of the central maximum is longer than the tail on the left side (skewed
"to the right"). A distribution is said to have a negative skewness if
the tail on the left side of the central maximum is longer than the tail
on the right side (skewed "to the left").

In general one can say that a skewness value greater than :math:`1` of
less than :math:`-1` indicates a highly skewed distribution. Whenever
the value is between :math:`0.5` and :math:`1` or :math:`-0.5` and
:math:`-1`, the distribution is considered to be moderately skewed. A
value between :math:`-0.5` and :math:`0.5` indicates that the
distribution is fairly symmetrical.

.. table:: 

	+--------------+----------------------------------------------------------------------------------------------+
	| **Operator** | ``Skewness``\ (*domain*,\ *expression*)                                                      |
	+--------------+----------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`\frac{{\displaystyle \sum_{i=1}^{n} (x_i - \mu)^3}} {{\displaystyle \sigma_{n-1}^3}}` |
	+--------------+----------------------------------------------------------------------------------------------+
	
where :math:`\mu` denotes the mean and :math:`\sigma_{n-1}` denotes the
standard deviation.

.. _kurtosis:

.. rubric:: Kurtosis

The kurtosis coefficient is a measure for the peakedness of a
distribution. If a distribution is fairly peaked, it will have a high
kurtosis coefficient. On the other hand, a low kurtosis coefficient
indicates that a distribution has a flat peak. It is common practice to
use the kurtosis coefficient of the standard Normal distribution, equal
to 3, as a standard of reference. Distributions which have a kurtosis
coefficient less than 3 are considered to be platykurtic (meaning flat),
whereas distributions with a kurtosis coefficient greater than 3 are
leptokurtic (meaning peaked). Be aware that in literature also an
alternative definition of kurtosis is used in which 3 is subtracted from
the formula used here.

.. table:: 

	+--------------+----------------------------------------------------------------------------------------------+
	| **Operator** | ``Kurtosis``\ (*domain*,\ *expression*)                                                      |
	+--------------+----------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`\frac{{\displaystyle \sum_{i=1}^{n} (x_i - \mu)^4}} {{\displaystyle \sigma_{n-1}^4}}` |
	+--------------+----------------------------------------------------------------------------------------------+
	
where :math:`\mu` denotes the mean and :math:`\sigma_{n-1}` denotes the
standard deviation.

.. _correlation:

.. rubric:: Correlation coefficient

The correlation coefficient is a measurement for the relationship
between two variables. Two variables are positive correlated with each
other when the correlation coefficient lies between 0 and 1. If the
correlation coefficient lies between :math:`-1` and 0, the variables are
negative correlated. In case the correlation coefficient is 0, the
variables are considered to be unrelated to one another.

Positive correlation means that if one variable increases, the other
variable increases also. Negative correlation means that if one variable
increases, the other variable decreases.

.. table:: 

	+--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| **Operator** | ``Correlation``\ (*domain*,\ *x_expression*, *y_expression*)                                                                                                                                                                                                                                          |
	+--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`\frac{ { \displaystyle n \sum_{i=1}^{n} x_i y_i - \sum_{i=1}^{n} x_i \sum_{i=1}^{n} y_i } } { { \displaystyle \sqrt{ \left( n \sum_{i=1}^{n} x_{i}^{2} - {\left( \sum_{i=1}^{n} x_i \right)}^2 \right) \left( n \sum_{i=1}^{n} y_{i}^{2} - {\left( \sum_{i=1}^{n} y_i \right)}^2 \right)} } }` |
	+--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
	
.. _rankcorrelation:

.. rubric:: Rank correlation

If one wants to determine the relationship between two variables, but
their distributions are not equal or the precision of the data is not
trusted, one can use the rank correlation coefficient to determine their
relationship. In order to compute the rank correlation coefficient the
data is ranked by their value using the numbers :math:`1,2,\ldots,n`.
These rank numbers are used to compute the rank correlation coefficient.

.. table:: 

	+--------------+------------------------------------------------------------------------------------------------------------------------------------------+
	| **Operator** | ``RankCorrelation``\ (*domain*,\ *x_expression*, *y_expression*)                                                                         |
	+--------------+------------------------------------------------------------------------------------------------------------------------------------------+
	| **Formula**  | :math:`1 - \frac{{\displaystyle 6 \sum_{i=1}^{n} {\left( \mbox{Rank}(x_i) - \mbox{Rank}(y_i) \right)}^2 }} {{\displaystyle n(n^2 - 1)}}` |
	+--------------+------------------------------------------------------------------------------------------------------------------------------------------+