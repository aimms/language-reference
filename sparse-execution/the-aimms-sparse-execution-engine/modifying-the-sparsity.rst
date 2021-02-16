.. _sec:sparse.modify:

.. _sec:sparse.modifier.binary:

Modifying the Sparsity
======================

.. rubric:: Questions

Now that we've glanced at the execution engine's inner workings, you may
be wondering about the following questions.

-  Does sparse execution influence the results of a model?

-  Does AIMMS have sparse versions of operators that are dense by
   nature?

.. rubric:: Sparse execution is correct

Sparse execution never changes the results of your model. AIMMS only
applies sparse intersection or sparse union when it is applicable. It
does not in any way influence the results of your model compared to
simply considering all the possible combinations of the running indices,
but only the efficiency with which these results are obtained.

.. rubric:: Sparsity modifiers

AIMMS does support sparse versions of some dense operators, but this
time the sparse versions will in general lead to different results.
Adding ``$`` characters to dense operators modify these operators to
sparse ones. That is why we call the ``$`` characters added to these
operators *sparsity modifiers*.

.. rubric:: Left and right operands

Sparsity modifiers may be added to the left-hand side of a dense
operator, to the right-hand side, or to both. It causes the operator
only to return a non-zero result if the associated operand(s) are
non-zero. Such a change to an operator may, however, change its results
in a way you may, or may not, want.

.. rubric:: A first example: the ``/$`` operator

Let us now consider a few examples where such a modification is
applicable. The first example of using a sparsity modifier is in the
efficient guarding against division by zero errors. Without the use of
sparsity modifiers, we can accomplish this as follows.

.. code-block:: aimms

	! Leave A(i,j) zero when C(i,j)+D(i,j) is zero in order to
	! avoid division by zero errors.
	! This is accomplished by repeating the denominator in the condition.
	A(i,j) := ( B(i,j) / (C(i,j)+D(i,j)) ) $ (C(i,j)+D(i,j)) ;

In the example, we only divide by ``C(i)+D(i)`` if this sum is non-zero.
Note that this subexpression is actually computed twice. AIMMS provides
a notational convenience in the form of ``$`` sparsity modifiers as
follows.

.. code-block:: aimms

	! Leave A(i,j) zero when C(i,j)+D(i,j) is zero in order to
	! avoid division by zero errors.
	! This is accomplished by using the /$ division operator
	! which sparsely skips 0.0's.
	A(i,j) := B(i,j) /$ (C(i,j)+D(i,j)) ;

The ``/$`` operator is defined as the ``/`` operator except when the
right hand side is 0.0. In that case, the ``$`` sparsity modifier
defines it as 0.0. An added advantage is that the sub-expression
``C(i)+D(i)`` is only computed once.

.. rubric:: The merge operator ``:=$``

A second example is in the merging of new results in a set of existing
results. Without the use of a sparsity modifier you can accomplish this
as follows.

.. code-block:: aimms

	! Only overwrite elements of E(i,j) when the result
	! F(i,j) + G(i,j) is non-zero.
	! This is accomplished by repeating the RHS of the
	! assignment as a domain condition.
	E((i,j) | F(i,j)+G(i,j)) := F(i,j)+G(i,j) ;

Using the ``$`` sparsity modifier this can be equivalently obtained as
follows.

.. code-block:: aimms

	! Only overwrite elements of E(i,j) when the result
	! F(i,j) + G(i,j) is non-zero.
	! This is accomplished by using the $ sparsity
	! modifier on the assignment operator:
	E(i,j) :=$ F(i,j)+G(i,j) ;

.. rubric:: Where allowed?

:ref:`this table <table:sparse.binary-sparsity>` summarizes the operators to which
the ``$`` sparsity modifier can be applied, and whether it can be
applied to the left-hand side operand, to the right-hand side operand,
or to both.

.. _table:sparse.binary-sparsity:

.. table:: Sparsity modifiers of binary operators

   +--------------------------+---------------------------+
   | Operator                 | Sparsity modifier allowed |
   |                          +-------------+-------------+
   |                          | ``$`` left  | ``$`` right |
   +==========================+=============+=============+
   | ``^``                    | yes         | yes         |
   +--------------------------+-------------+-------------+
   | ``*``                    | no          | no          |
   +--------------------------+-------------+-------------+
   | ``/``                    | no          | yes         |
   +--------------------------+-------------+-------------+
   | ``+``, ``-``             | no          | no          |
   +--------------------------+-------------+-------------+
   | ``=``, ``<>``, ``<``,    | yes         | yes         |
   | ``<=``, ``>``, ``>=``    |             |             |
   +--------------------------+-------------+-------------+
   | ``:=``                   | yes         | yes         |
   +--------------------------+-------------+-------------+
   | ``+=``, ``-=``           | yes         | no          |
   +--------------------------+-------------+-------------+
   | ``*=``, ``/=``, ``=``    | yes         | yes         |
   +--------------------------+-------------+-------------+
   | ``$``, ``ONLYIF``,       | no          | no          |
   | ``AND``, ``OR``, ``XOR`` |             |             |
   +--------------------------+-------------+-------------+

.. rubric:: Modifying iterative operators

In addition to modifying the behavior of binary operators, the ``$``
sparsity modifier can also be applied to iterative operators. The effect
in this case is that the iterative operator in the presence of a ``$``
modifier will only be applied to tuples for which the expression yields
a non-zero value.

.. rubric:: Example: the ``Min$`` operator

The third and final example of the ``$`` sparsity modifier provided here
is on the :any:`Min` operator. Suppose you want to find the smallest
non-zero distance between a particular node and other nodes. This can be
modeled as follows:

.. code-block:: aimms

	! Find the smallest non-zero distance:
	MinimalDistance(i) := Min(j | Distance(i,j), Distance(i,j));

The 'non-zero' restriction is taken care of by repeating the argument of
the :any:`Min` operator in its domain condition. By using the ``$``
sparsity modifier we can shorten the above as follows:

.. code-block:: aimms

	! Find the smallest non-zero distance:
	MinimalDistance(i) := Min$(j, Distance(i,j));

.. rubric:: Where allowed?

:ref:`this table <table:sparse.iterative-sparsity>` summarizes the iterative
operators to which the ``$`` sparsity modifier can be applied.

.. _table:sparse.iterative-sparsity:

.. table:: Sparsity modifiers of iterative operators

   +------------------------------------------------------+---------------------------+
   | Iterative operator                                   | Sparsity modifier allowed |
   |                                                      +---------------------------+
   |                                                      | ``$`` added               |
   +======================================================+===========================+
   | ``Sort``, ``NBest``                                  | yes                       |
   +------------------------------------------------------+---------------------------+
   | ``Intersection``                                     | yes                       |
   +------------------------------------------------------+---------------------------+
   | :any:`First`, :any:`Last`, ``Nth``                   | no                        |
   +------------------------------------------------------+---------------------------+
   | ``ArgMin``, ``ArgMax``                               | yes                       |
   +------------------------------------------------------+---------------------------+
   | ``Sum``, ``Union``                                   | no                        |
   +------------------------------------------------------+---------------------------+
   | ``Prod``                                             | yes                       |
   +------------------------------------------------------+---------------------------+
   | :any:`Min`, :any:`Max`                               | yes                       |
   +------------------------------------------------------+---------------------------+
   | Statistical operators                                | yes                       |
   | (see also :ref:`this table <table:expr.stat-iter>`)  |                           |
   +------------------------------------------------------+---------------------------+
   | ``ForAll``                                           | no                        |
   +------------------------------------------------------+---------------------------+
   | Other logical operators                              | no                        |
   | (see also :ref:`this table <table:expr.logic-iter>`) |                           |
   +------------------------------------------------------+---------------------------+

.. rubric:: Usage of sparsity modifiers

To conclude, we can say that the ``$`` sparsity modifier is notationally
a convenience which you may or may not like. In the end it is up to you
whether you use it or not. You decide this by weighing its advantage and
disadvantages. Our view on this is discussed briefly below.

.. rubric:: Advantages

Using sparsity modifiers has the following advantages.

-  It enables a more compact notation. In the examples above, the domain
   condition is replaced by a strategically placed ``$`` sparsity
   modifier thereby reducing the overall expression. Many models have
   with multiple line subexpressions and with these the reduction is not
   insignificant.

-  It is more efficient. There are usually abundant zeros in a model.
   You want them ignored so that the corresponding entries do not appear
   in the results. In addition, you want them to be ignored as quickly
   as possible: so as not to waste any computation time on them.

.. rubric:: Disadvantages

As with any new notation it takes time to get used to it. This holds
both for you as a modeler and also for the people you want to
communicate your model to. In order to alleviate this disadvantage you
may want to add a few brief comments on the modified operators you use
such as
``:=$ operator used here to merge the result into the existing data``.