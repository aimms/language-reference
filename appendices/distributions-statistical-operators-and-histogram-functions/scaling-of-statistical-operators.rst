.. _app:scaleoperator.stat:

Scaling of Statistical Operators
================================

.. rubric:: Transforming distributions

Shifting and scaling distribution has an effect on the distribution
operators, and on sample operators when the samples are from a specified
distribution. Location and scale parameters find their origin in a
common transformation

.. math:: x \mapsto \frac{x-l}{s}

to shift and stretch a given distribution. By choosing :math:`l=0` and
:math:`s=1` one obtains the standard form of a given distribution, and
the relation of operators working on the general and standard form of
distributions is as follows:

.. math::

   \begin{align}
   X(l,s) &= l + sX(0,1)\\
       \mathtt{DistributionDensity}(x;l,s) &= \frac{1}{s} \mathtt{DistributionDensity}(\frac{x-l}{s};0,1)\\
       \mathtt{DistributionInversDensity}(\alpha;l,s) &= s \cdot \mathtt{DistributionInversDensity}(\alpha;0,1)\\
       \mathtt{DistributionCumulative}(x;l,s) &= \mathtt{DistributionCumulative($\frac{x-l}{s};0,1$)}\\
       \mathtt{DistributionInverseCumulative}(\alpha;l,s) &= l + s \cdot \mathtt{DistributionInverseCumulative}(\alpha;0,1)\\
       \mathtt{Mean}(X(l,s)) &= l + s \cdot \mathtt{Mean}(X(0,1))\\
       \mathtt{Median}(X(l,s)) &= l + s \cdot \mathtt{Median}(X(0,1))\\
       \mathtt{Deviation}(X(l,s)) &= s \cdot \mathtt{Deviation}(X(0,1))\\
       \mathtt{DistributionVariance}(X(l,s)) &= s^2 \cdot \mathtt{DistributionVariance}(X(0,1))\\
       \mathtt{Skewness}(X(l,s)) &= \mathtt{Skewness}(X(0,1))\\
       \mathtt{Kurtosis}(X(l,s)) &= \mathtt{Kurtosis}(X(0,1))\\
       \mathtt{(Rank)Correlation}(X(l,s),Y) &= \mathtt{(Rank)Correlation}(X(0,1),Y)
   \end{align}

.. rubric:: Transformation of the mean

The transformation formula for the ``Mean`` holds for both the
:any:`DistributionMean` and the ``Mean`` of a sample. However, for the
``GeometricMean``, the ``HarmonicMean`` and the ``RootMeanSquare``, only
the scale factor can be propagated easily during the transformation.
Thus, for a sample taken from a distribution :math:`X` and a any mean
operator :math:`M` from the ``GeometricMean``, ``HarmonicMean`` or
``RootMeanSquare``, it holds that

.. math:: M(X(l,s)) = s \cdot M(X(l,1))

but in general

.. math:: M(X(l,s)) \pmb{\neq} l+ M(X(0,s))

.. rubric:: Transformation of the other moments

The transformation formula for the deviation is valid for the
:any:`DistributionDeviation`, the ``SampleDeviation`` and
``PopulationDeviation``, while the transformation formulae for the
``Skewness`` and ``Kurtosis`` hold for both the distribution and sample
operators.