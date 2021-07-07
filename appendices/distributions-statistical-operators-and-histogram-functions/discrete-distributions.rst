.. _app:distribution.discrete:

Discrete Distributions
======================

.. rubric:: Discrete distributions

We start our discussion with the discrete distributions available in
AIMMS. They are

-  the :any:`Binomial` distribution,

-  the :any:`HyperGeometric` distribution,

-  the :any:`Poisson` distribution,

-  the :any:`NegativeBinomial` distribution, and

-  the :any:`Geometric` distribution.

.. rubric:: Discrete distributions describing successes

The :any:`Binomial`, :any:`HyperGeometric` and :any:`Poisson` distributions
describe the number of times that a particular outcome (referred to as
"success") occurs. In the :any:`Binomial` distribution, the underlying
assumption is a fixed number of trials and a constant likelihood of
success. In the :any:`HyperGeometric` distribution, the underlying
assumption is "sampling without replacement": A fixed number of trials
are taken from a population. Each element of this population denotes a
success or failure and cannot occur more than once. In the :any:`Poisson`
distribution the number of trials is not fixed. Instead we assume that
successes occur independently of each other and with equal chance for
all intervals with the same duration.

.. rubric:: Distributions describing trials

The :any:`NegativeBinomial` distribution describes the number of failures
before a specified number of successes have occurred. It assumes a
constant chance of success for each trial, so it is linked to the
:any:`Binomial` distribution. Similarly, the distribution linked to
:any:`Poisson` distribution that describes the amount of time until a
certain number of successes have occurred is known as the :any:`Gamma`
distribution and is discussed in :ref:`app:distribution.cont`. The
:any:`NegativeBinomial` distribution is a special case of the :any:`Geometric`
distribution and describes the number of failures before the first
success occurs. Similarly, the :any:`Exponential` distribution is a special
case of the :any:`Gamma` distribution and describes the amount of time
until the first occurrence.

.. rubric:: Discrete distributions overview

:ref:`this table <table:app.discr_distributions>` shows the relation between the
discrete distributions. The continuous :any:`Exponential` and :any:`Gamma`
distribution naturally fit in this table as they represent the
distribution of the time it takes before the first/:math:`n`-th
occurrence (given the average time between two consecutive occurrences).

.. _table:app.discr_distributions:

.. _tb:app.discr_distributions:

.. table:: Overview of discrete distributions in AIMMS

   +--------------------------------------------------------------------------+-------------------------+------------------------+-------------------------------------------+
   |                                                                          | with replacement        | without replacement    | independent occurrences at random moments |
   +==========================================================================+=========================+========================+===========================================+
   | example                                                                  | throwing dice           | drawing cards          | serving customers                         |
   +--------------------------------------------------------------------------+-------------------------+------------------------+-------------------------------------------+
   | # trials until first success / time until first occurrence               | :any:`Geometric`        | not supported in AIMMS | :any:`Exponential` (continuous)           |
   +--------------------------------------------------------------------------+-------------------------+------------------------+-------------------------------------------+
   | # trials until :math:`n`-th success / time until :math:`n`-th occurrence | :any:`NegativeBinomial` | not supported in AIMMS | :any:`Gamma` (continuous)                 |
   +--------------------------------------------------------------------------+-------------------------+------------------------+-------------------------------------------+
   | # successes in fixed # trials / # successes in fixed time                | :any:`Binomial`         | :any:`HyperGeometric`  | :any:`Poisson`                            |
   +--------------------------------------------------------------------------+-------------------------+------------------------+-------------------------------------------+

.. rubric:: :any:`Binomial` distribution

.. figure:: discrete-distributions-pspic1.svg

.. _binomial-LR:

The :any:`Binomial`\ :math:`(p,n)` distribution:

.. table:: 

	+------------------+--------------------------------------------------------------------------+
	| Input parameters | Probability of success :math:`p` and number of trials :math:`n`          |
	+------------------+--------------------------------------------------------------------------+
	| Input check      | :math:`\mbox{integer} \; n > 0 \; \mbox{and} \; 0 < p < 1`               |
	+------------------+--------------------------------------------------------------------------+
	| Permitted values | :math:`\{i \; | \; i = 0, 1, \ldots, n \}`                               |
	+------------------+--------------------------------------------------------------------------+
	| Formula          | :math:`P(X=i) = \binom{n}{i} p^i (1-p)^{n-i}`                            |
	+------------------+--------------------------------------------------------------------------+
	| Mean             | :math:`np`                                                               |
	+------------------+--------------------------------------------------------------------------+
	| Variance         | :math:`np(1-p)`                                                          |
	+------------------+--------------------------------------------------------------------------+
	| Remarks          | :any:`Binomial`:math:`(p,n)` = :any:`HyperGeometric`:math:`(p,n,\infty)` |
	+------------------+--------------------------------------------------------------------------+
	
A typical example for this distribution is the number of defectives in a
batch of manufactured products where a fixed percentage was found to be
defective in previously produced batches. Another example is the number
of persons in a group voting yes instead of no, where the probability of
yes has been determined on the basis of a sample.

.. rubric:: :any:`HyperGeometric` distribution

.. figure:: discrete-distributions-pspic2.svg

.. _hypergeometric-LR:

The :any:`HyperGeometric`\ :math:`(p,n,N)` distribution:

.. table:: 

	+------------------+----------------------------------------------------------------------------------------------------------------------+
	| Input parameters | Known initial probability of success :math:`p`, number of trials :math:`n` and population size :math:`N`             |
	+------------------+----------------------------------------------------------------------------------------------------------------------+
	| Input check      | :math:`\mbox{integer} \; n,N: 0 < n \leq N, \; \mbox{and $p \in \frac{1}{N}, \frac{2}{N}, \ldots, \frac{N - 1}{N}$}` |
	+------------------+----------------------------------------------------------------------------------------------------------------------+
	| Permitted values | :math:`\{ i \; | \; i = 0, 1, \ldots, n \}`                                                                          |
	+------------------+----------------------------------------------------------------------------------------------------------------------+
	| Formula          | :math:`P(X = i) = \frac{ \binom{N p}{i} \binom{N (1-p)}{n - i} }{ \binom{N}{n} }`                                    |
	+------------------+----------------------------------------------------------------------------------------------------------------------+
	| Mean             | :math:`np`                                                                                                           |
	+------------------+----------------------------------------------------------------------------------------------------------------------+
	| Variance         | :math:`np(1-p)\mbox{$\frac{N-n}{N-1}$}`                                                                              |
	+------------------+----------------------------------------------------------------------------------------------------------------------+

As an example of this distribution, consider a set of 1000 books of
which 30 are faulty When considering an order containing 50 books from
this set, the :any:`HyperGeometric`\ (0.03,50,1000) distribution shows the
probability of observing :math:`i \; (i = 0, 1, \ldots,n)` faulty books
in this subset.

.. rubric:: :any:`Poisson` distribution

.. figure:: discrete-distributions-pspic3.svg

.. _poisson-LR:

The :any:`Poisson`\ :math:`(\lambda)` distribution:

.. table:: 

	+------------------+--------------------------------------------------------------------------------------------+
	| Input parameters | Average number of occurrences :math:`\lambda`                                              |
	+------------------+--------------------------------------------------------------------------------------------+
	| Input check      | :math:`\lambda > 0`                                                                        |
	+------------------+--------------------------------------------------------------------------------------------+
	| Permitted values | :math:`\{ i \; | \; i = 0, 1, \ldots \}`                                                   |
	+------------------+--------------------------------------------------------------------------------------------+
	| Formula          | :math:`P(X = i) = \frac{\lambda^i}{i!} e^{-\lambda}`                                       |
	+------------------+--------------------------------------------------------------------------------------------+
	| Mean             | :math:`\lambda`                                                                            |
	+------------------+--------------------------------------------------------------------------------------------+
	| Variance         | :math:`\lambda`                                                                            |
	+------------------+--------------------------------------------------------------------------------------------+
	| Remarks          | :any:`Poisson`:math:`(\lambda)= \lim_{p \downarrow 0}`:any:`Binomial`:math:`(p,\lambda/p)` |
	+------------------+--------------------------------------------------------------------------------------------+
	
The :any:`Poisson` distribution should be used when there is an constant
chance of a 'success' over time or (as an approximation) when there are
many occurrences with a very small individual chance of 'success'.
Typical examples are the number of visitors in a day, the number of
errors in a document, the number of defects in a large batch, the number
of telephone calls in a minute, etc.

.. rubric:: :any:`NegativeBinomial` distribution

.. figure:: discrete-distributions-pspic4.svg

.. _negativebinomial-LR:

The :any:`NegativeBinomial`\ :math:`(p,r)` distribution:

.. table:: 

	+------------------+-----------------------------------------------------------------+
	| Input parameters | Success probability :math:`p` and number of successes :math:`r` |
	+------------------+-----------------------------------------------------------------+
	| Input check      | :math:`0 < p < 1 \; \mbox{and} \; r = 1, 2, \ldots`             |
	+------------------+-----------------------------------------------------------------+
	| Permitted values | :math:`\{ i \; | \; i = 0, 1, \ldots \}`                        |
	+------------------+-----------------------------------------------------------------+
	| Formula          | :math:`P(X = i) = \binom{r + i - 1}{i} p^r (1-p)^i`             |
	+------------------+-----------------------------------------------------------------+
	| Mean             | :math:`r/p-r`                                                   |
	+------------------+-----------------------------------------------------------------+
	| Variance         | :math:`r(1-p)/p^2`                                              |
	+------------------+-----------------------------------------------------------------+

Whenever there is a repetition of the same activity, and you are
interested in observing the :math:`r`-th occurrence of a particular
outcome, then the :any:`NegativeBinomial` distribution might be applicable.
A typical situation is going from door-to-door until you have made
:math:`r` sales, where the probability of making a sale has been
determined on the basis of previous experience. Note that the
:any:`NegativeBinomial` distribution describes the number of *failures*
before the :math:`r`-th success. The distribution of the number of
*trials* :math:`i` before the :math:`r`-th success is given by
:math:`P_{\texttt{NegativeBinomial(p,r)}}(X=i-r)`.

.. rubric:: :any:`Geometric` distribution

.. figure:: discrete-distributions-pspic5.svg

.. _geometric-LR:

The :any:`Geometric`\ :math:`(p)` distribution:

.. table:: 

	+------------------+--------------------------------------------------------------------+
	| Input parameters | Probability of success :math:`p`                                   |
	+------------------+--------------------------------------------------------------------+
	| Input check      | :math:`0 < p < 1`                                                  |
	+------------------+--------------------------------------------------------------------+
	| Permitted values | :math:`\{i \; | \; i = 0, 1, \ldots \}`                            |
	+------------------+--------------------------------------------------------------------+
	| Formula          | :math:`P(X = i) = (1 - p)^i p`                                     |
	+------------------+--------------------------------------------------------------------+
	| Mean             | :math:`1/p-1`                                                      |
	+------------------+--------------------------------------------------------------------+
	| Variance         | :math:`(1-p)/p^2`                                                  |
	+------------------+--------------------------------------------------------------------+
	| Remarks          | :any:`Geometric`:math:`(p)` = :any:`NegativeBinomial`:math:`(p,1)` |
	+------------------+--------------------------------------------------------------------+
	
The :any:`Geometric` distribution is a special case of the
:any:`NegativeBinomial` distribution. So it can be used for the same type
of problems (the number of visited doors before the first sale). Another
example is an oil company drilling wells until a producing well is
found, where the probability of success is based on measurements around
the site and comparing them with measurements from other similar sites.
