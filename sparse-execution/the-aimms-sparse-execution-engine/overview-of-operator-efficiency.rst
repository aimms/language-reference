.. _section:sparse.dense-ops:

Overview of Operator Efficiency
===============================

.. rubric:: Operator efficiency

In this section you will find an overview of the efficiency of all
unary, binary and iterative operators in AIMMS.

.. rubric:: Unary operators and functions

The unary operators and functions presented in
:ref:`this table <table:sparseness.unary>` are divided in two groups: sparse and
dense.

-  *sparse*: Here, when the argument is 0.0, the result is 0.0. The
   result needs to be computed only for those tuples for which the
   argument has a non-zero value.

-  *dense*: Here, when the argument is 0.0, the result is not equal to
   0.0. The results of all possible tuples need to be computed.

.. _table:sparseness.unary:

.. table:: Sparsen and dense unary operators and functions

	+-------------------------------+-------------------------------+
	| **sparse**                    | **dense**                     |
	+===============+===============+===============+===============+
	| ``-``         | ``Sinh``      | ``NOT``       | ``Cos``       |
	+---------------+---------------+---------------+---------------+
	| ``Sin``       | ``Tanh``      | ``Cos``       | ``Cosh``      |
	+---------------+---------------+---------------+---------------+
	| ``Tan``       | ``ArcSin``    | ``Exp``       | ``ArcCos``    |
	+---------------+---------------+---------------+---------------+
	| ``Round``     | ``ArcTan``    | ``Log``       | ``ArcCosh``   |
	+---------------+---------------+---------------+---------------+
	| ``Floor``     | ``ArcSinh``   | ``Log10``     | ``Factorial`` |
	+---------------+---------------+---------------+---------------+
	| ``Ceil``      | ``ArcTanh``   |               |               |
	+---------------+---------------+---------------+---------------+
	| ``Trunc``     | ``Sqr``       |               |               |
	+---------------+---------------+---------------+---------------+
	| ``Sqrt``      |               |               |               |
	+---------------+---------------+---------------+---------------+
	
.. rubric:: Binary operators

The binary operators presented in :ref:`this table <table:sparseness.binary>` can
be divided in three groups:

-  *intersection sparse*: Here, when either of the arguments is 0.0, the
   result is 0.0. The result of only those tuples need to be computed
   where both arguments are not equal to 0.0. This corresponds to taking
   the intersection of the set of tuples for which the arguments are
   defined.

-  *union sparse*: Here, when both arguments are 0.0, the result is 0.0.
   The result of only those tuples need to be computed where at least
   one of the arguments is not equal to 0.0. This corresponds to taking
   the union of the set of tuples for which the arguments are defined.

-  *dense*: Here, when both arguments are 0.0, the result is not equal
   to 0.0. In this case, the expression needs to be evaluated for all
   possible combinations of values of the indices, unless these
   combinations are limited by a sparse operator elsewhere in the same
   expression. This corresponds to taking the Cartesian product of the
   ranges of the indices.

.. _table:sparseness.binary:

.. table:: Sparseness of binary operators

   ============ ======= ==================
   intersection union   dense
   ============ ======= ==================
   ``*``        ``+``   ``^``
   ``$``        ``-``   ``/``
   ``ONLYIF``   ``<>``  ``=``
   ``AND``      ``<``   ``<=``
                ``>``   ``>=``
                ``OR``  :any:`Permutation`
                ``XOR`` :any:`Combination`
   ============ ======= ==================

.. rubric:: Iterative operators

The iterative operators presented in
:ref:`this table <table:sparseness.iterative>` are divided in three groups as
follows:

-  *sparse* A value 0.0 of an argument does not influence the result and
   can safely be ignored. The iterative operator only considers existing
   entries of its argument.

-  *almost sparse* A second 0.0 in the argument does not influence the
   result. The execution starts in a dense meaning that the iterative
   operator considers all possible tuples. However, after a first 0.0
   has been encountered, execution continues in a sparse manner.

-  *dense* A value 0.0 in the argument influences the result. The
   iterative operator considers all possible combinations.

.. _table:sparseness.iterative:

.. table:: Sparseness of iterative operators

   ========== ================= ================== =======================
   **sparse** **almost sparse** **dense**             
   ========== ================= ================== =======================
   ``Sum``    :any:`Max`        ``Mean``           ``SampleDeviation``
   ``Prod``   :any:`Min`        ``GeometricMean``  ``PopulationDeviation``
   ``Exists`` ``ArgMax``        ``HarmonicMean``   ``Skewness``
   ``Forall`` ``ArgMin``        ``RootMeanSquare`` ``Kurtosis``
   ``Count``                    ``Median``         ``RankCorrelation``
   ========== ================= ================== =======================