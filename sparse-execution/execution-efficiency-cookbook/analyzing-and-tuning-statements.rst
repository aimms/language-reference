.. _section:eff.tuning-stmts:

Analyzing and Tuning Statements
===============================

.. rubric:: Analyzing and tuning statements

As illustrated in the previous section, carefully reviewing the number
of elements in active subsets and the index domain conditions may lead
to significant reductions in execution time. Additional reductions can
be obtained by analyzing and rewriting specific time-consuming
statements and constraints. In this section we will discuss a procedure
which you can follow to identify and resolve potential inefficiencies in
your model.

.. rubric:: Suggested approach

You can use the AIMMS profiler to identify computational bottlenecks in
your model. If you have found a particular bottleneck, you may want to
use the checklist below to quickly find relevant information for the
problem at hand. For each question that you answer with a yes you may
want to follow the suggested option.

-  Is the bottleneck a repeated expression where the combined execution
   of all instances takes up a lot of time? If so, you can either

   -  manually replace the expression by a new parameter containing the
      repeated expression as a definition. Do not forget to check the
      ``NoSave`` property if you do not want that newly defined
      parameter to be stored in cases.

   -  or let AIMMS do it for you, by setting the option
      ``subst low dim expr class`` to an appropriate value for your
      application. See also the help associated with that option.

   For a worked example, see also
   :ref:`subsection:eff.tuning-stmts.compl-expr`

-  Is the bottleneck due to debugging/obsolete code? If so, delete it,
   move it to the ``Comment`` attribute, or enclose the time-consuming
   debugging code in something like an ``IF ( DebugMode ) THEN`` and
   ``ENDIF`` pair.

-  Are you using dense operators such ``/``, ``=``, ``^``, or dense
   functions such as :any:`Log`, :any:`Exp`, :any:`Cos` in which a zero argument
   has a non-zero result? An overview of the efficiency of such
   functions and operators can be found in
   :ref:`section:sparse.dense-ops`. Could you add index domain
   conditions to make the execution of the time-consuming expressions
   more sparse, without changing the final result?

-  Is the bottleneck part of a ``FOR`` statement? If so, is that ``FOR``
   statement really necessary? For a detailed discussion about the need
   for and alternatives to ``FOR`` statements, see
   :ref:`subsection:eff.tuning-stmts.for-stmt`.

-  Is the bottleneck the condition of the ``FOR`` statement that takes
   up most of the time? This is shown in the profiler by a large net
   time for the ``FOR`` statement.
   :ref:`subsection:eff.tuning-stmts.for-condition` discusses why the
   conditions of ``FOR`` statements may absorb a lot of computational
   time and discusses alternatives.

-  Does the body of a ``FOR``, ``WHILE``, or ``REPEAT`` statement
   contain a ``SOLVE`` statement, and is AIMMS spending a lot of time
   regenerating constraints (as shown in the profiling times of the
   constraints)? If so, consider modifying the generated mathematical
   programs directly using the GMP library as discussed in
   :ref:`chap:gmp`.

-  Does your model contain a defined parameter over an index, say ``t``,
   and do you use this parameter inside a ``FOR`` loop that runs over
   that same index ``t``? Inefficient use of this construct is indicated
   by the AIMMS profiler through a high hitcount for that defined
   parameter. See :ref:`subsection:eff.tuning-stmts.defs-for-loop` for
   an example and an alternative formulation.

-  Is the bottleneck an expression with several running indices?
   Contains this expression non-trivial sub-expressions with fewer
   running indices? If the answer is yes, consult
   :ref:`subsection:eff.tuning-stmts.compl-expr` for a detailed analysis
   of two examples.

-  Does the expression involve a parameter or a variable that is bound
   with a non-zero default? :ref:`subsection:eff.tuning-stmts.nz-defval`
   discusses the possible adverse timing effects of using non-zero
   defaults in expressions, and how to overcome these.

-  Would you expect a time-consuming assignment to take less time given
   the sparsity of the identifiers involved? This may be one of those
   rare occasions in which the specific order of running indices has an
   effect on the execution speed. Although tackling this type of
   bottleneck may be very challenging,
   :ref:`subsection:eff.tuning-stmts.index-ordering` hopefully offers
   sufficient clues through an illustrative example.

-  Are you using ordered sets? Reordering the elements in a set can slow
   execution significantly as detailed in :ref:`sec:eff.set.ordering`.

If you want hands on experience with such examples, please check out the last chapter of 
the `AIMMS Academy <https://academy.aimms.com>`_ course "Execution Efficiency".  
In this course, concrete AIMMS 4.79 projects are offered to experiment with.


.. _subsection:eff.tuning-stmts.for-stmt:

Consider the Use of ``FOR`` Statements
--------------------------------------

.. rubric:: Why avoid the ``FOR`` statement?

The AIMMS execution system is designed for efficient bulk execution of
assignment statements, plus set and parameter definitions and
constraints. A consequence of this design choice is that computation
time is spent, just before the execution of such an executable object,
analyzing and initializing that object. This is usually worthwhile
except when only one element is computed at a time. Consider the
following two fragments of AIMMS code that have the same final result.
The first fragment uses a ``FOR`` statement:

.. code-block:: aimms

	for ( (i,j) | B(i,j) ) do ! Only when B(i,j) exists we want to
	    A(i,j) := B(i,j);     ! overwrite A(i,j) with it.
	endfor ;

The second fragment avoids the ``FOR`` statement:

.. code-block:: aimms

	A((i,j) | B(i,j)) := B(i,j); ! Overwrite A(i,j) only when B(i,j) exists

In the first fragment, the initialization and analysis is performed for
every iteration of the ``FOR`` loop. In the second fragment the
initialization and analysis is performed only once. Using the ``$``
sparsity modifier on the assignment operator ``:=`` (see also
:ref:`sec:sparse.modify`), the statement can be formulated even more
compactly and efficiently as:

.. code-block:: aimms

	A(i,j) :=$ B(i,j); ! Merge B(i,j) in A(i,j)

In the above example, the ``FOR`` statement is used only to restrict the
domain of execution of a single assignment. While using the ``FOR``
statement in this manner may seem normal to programmers, the execution
engine of AIMMS can deal with conditions on assignment statements much
more efficiently. As such, the use of the ``FOR`` statement is
superfluous and time consuming.

.. rubric:: When *not* to remove the ``FOR`` statement

Now that the ``FOR`` statement has been made to look inefficient, you
are probably wondering why has it been introduced in the AIMMS language
in the first place? Well, simply because sometimes it is needed. And it
is only inefficient if used unnecessarilly. So when is the ``FOR``
statement applicable? Two typical examples are:

-  generating a text report file, and

-  in algorithmic code inside the core model.

We will discuss these examples in the next two paragraphs.

.. rubric:: Generating text reports

The AIMMS ``DISPLAY`` statement is a high level command that outputs an
identifier in tabular, list, or composite list format with a limited
amount of control. In addition, the output of the ``DISPLAY`` statement
can always be read back by AIMMS, and, to enable that requirement, the
name of the identifier is always included in the output. Thus, the AIMMS
``DISPLAY`` statement usually fails to meet the specific formatting
requirements of your application domain, and you end up needing control
over the position of the output on an element-by-element basis. This
requires the use of ``FOR`` statements. However, depending on the
purpose of your text report file, there might be very good alternatives
available:

-  When this reporting is for printing purposes only, you may want to
   consider the AIMMS print pages as explained in AIMMS The `User's Guide <https://documentation.aimms.com/_downloads/AIMMS_user.pdf>`__
   Chapter 14. These print pages look far better than text
   reports.

-  When the report file is for communication with other programs, you
   may want to consider whether communication using relational databases
   (see :ref:`chap:db`), or through XML (see :ref:`chap:xml`) form
   better alternatives. For communication with EXCEL or OpenOffice Calc,
   a library of dedicated functions is built in AIMMS (see
   :ref:`chap:spreadsheet`).

.. rubric:: Algorithmic code inside the core model

A ``FOR`` statement is needed whenever your model contains two
statements where:

-  the computation of the last statement depends on the computation of
   the first statement, and

-  the computation of the first statement depends on the results of the
   last statement obtained during a previous iteration.

.. rubric:: Iterating unneccesarily

``FOR`` statements may be especially inefficient, if the condition of a
``FOR`` statement allows elements for which none of the statements
inside the ``FOR`` loop modify the data in your model or generate
output. This is illustrated in the following example.

.. rubric:: Transposing a distance matrix

Consider a distance matrix, ``D(i,j)``, with only a few entries per row
in its lower left half containing the distances to near neighbors. You
also want it to contain the reverse distances. One, inefficient, but
valid, way to formulate that in AIMMS is as follows:

.. code-block:: aimms

	for ( (i,j) | i > j ) do ! The condition 'i > j' ensures we only
	    D(i,j) := D(j,i) ;   ! write to the upper right of D.
	endfor ;

.. rubric:: Why inefficient?

There are two reasons why the above is inefficient:

-  Although there is a condition on the ``FOR`` loop, this condition
   permits many combinations of ``(i,j)`` that do not invoke execution
   as ``D(i,j)`` was sparse to begin with. A tempting improvement would
   be to add ``D(j,i)`` to the condition on the ``FOR`` loop. However,
   this will lead to other problems, however, as will be explained in
   the next section.

-  As explained in :ref:`subsec:sparse.basic.reordered-views`, AIMMS
   maintains reordered views. For each non-zero value computed and
   assigned to the identifier ``D(i,j)``, AIMMS will need to adapt the
   reordered view for ``D(j,i)``, and re-initialize searching in that
   reordered view.

.. rubric:: Suggested modification

In the example at hand we can move the condition on the ``FOR`` loop to
the assignment itself and simply remove the ``FOR`` statement altogether
(but not its contents). The example then reads:

.. code-block:: aimms

	D((i,j) | i > j) := D(j,i) ; ! The condition 'i > j' ensures we only
	                             ! write to the upper right of D.

.. rubric:: Using application domain knowledge

We can improve the assignment further by noting that we are actually
merging the transposed lower half in the identifier itself, and that
there is no conflict in the elements. This can be achieved by a ``$``
sparsity modifier on the assignment operator. The ``$`` sparsity
modifier and the opportunity it offers are introduced in
:ref:`sec:sparse.modify`. The example can then be written as:

.. code-block:: aimms

	D(i,j) :=$ D(j,i); ! Merge the transpose of the lower half in the identifier itself.

.. _sec:eff.set.for:

.. _subsection:eff.tuning-stmts.for-condition:

Ordered Sets and the Condition of a ``FOR`` Statement
-----------------------------------------------------

.. rubric:: Modifying the ``FOR`` condition

The condition placed on a ``FOR`` statement is like any other expression
evaluated one element at a time. However, during that evaluation, the
identifiers referenced in the condition may have been modified by the
statements inside the ``FOR`` loop. In general, this is not a problem,
except when the range of the running index of the ``FOR`` statement is
an *ordered* set. In that situation, the evaluation of the condition
itself becomes time consuming as the tuples satisfying the condition
have to be repeatedly computed and sorted, as illustrated below.

.. rubric:: Continued example

Let us again consider the example of the previous section with the
parameter ``D`` now added to the ``FOR`` loop condition, and the set
``S`` ordered lexicographically. As an efficient formulation has already
been presented in the previous section, it looks somewhat artificial,
but similar structures may appear in real-life models.

.. code-block:: aimms

	Set S {
	    Index      : i,j;
	    OrderBy    : i ! lexicographic ordering.;
	    Body       : {
	        for ( (i,j) | ( i > j ) AND D(j,i) ) do ! Only execute the statements in the
	            D(i,j) := D(j,i) ;                  ! loop when this is essential.
	        endfor
	    }
	}

.. rubric:: What does AIMMS do in this example?

First note that the ``FOR`` statement respects the ordering of the set
``S``. Because of this ordering, AIMMS will first evaluate the entire
collection of tuples satisfying the condition ``( i > j ) AND D(j,i)``,
and subsequently order this collection according to the ordering of the
set ``S``. Next, the body of the ``FOR`` statement is executed for every
tuple in the ordered tuple collection. However, when an identifier, such
as ``D`` in this example, is modified inside the body of the ``FOR``
loop AIMMS will need to recompute the ordered tuple collection, and
continue where it left off. This not only sounds time consuming, it is.

.. rubric:: ``FOR`` as a bottleneck

If the following three conditions are met, the condition of a ``FOR``
statement becomes time consuming:

-  the indices of a ``FOR`` statement have a specified element order,

-  the condition of the ``FOR`` statement is changed by the statements
   inside the loop, and

-  the product of the cardinality of the sets associated with the
   running indices of the ``FOR`` statement is very large.

if these three conditions are met, AIMMS will issue a warning when the
number of re-evaluations reaches a certain threshold.

.. rubric:: Improving efficiency

There are several ways to improve the efficiency of inefficient ``FOR``
statements. To understand this, it is necessary to explain a little more
about the execution strategies available to AIMMS when evaluating
``FOR`` statements, as each strategy has its own merits and drawbacks.
Therefore, consider the ``FOR`` statement:

.. code-block:: aimms

	for ( (i,j,k) | Expression(i,j,k) ) do
	   ! statements ...
	endfor;

where ``i``, ``j`` and ``k`` are indices of some sets, each with a
specified ordering, and ``Expression(i,j,k)`` is some expression over
the indices ``i``, ``j`` and ``k``.

.. rubric:: The sparse strategy

The first strategy, called the *sparse* strategy, fully evaluates
``Expression(i,j,k)``, and stores the result in temporary storage before
executing the ``FOR`` statement. Subsequently, for each tuple
``(i,j,k)`` for which a non-zero value is stored, the statements within
the ``FOR`` loop are executed. If an identifier is modified during the
execution of these statements, then the condition ``Expression(i,j,k)``
has to be fully re-evaluated.

.. rubric:: The dense strategy

The second strategy, called the *dense* strategy, evaluates
``Expression(i,j,k)`` for all possible combinations of indices
``(i,j,k)``. As soon as a non-zero result is found the statements are
executed. Re-evaluation is avoided, but at the price of considering
every ``(i,j,k)`` combination.

.. rubric:: The unordered strategy

The third strategy, called the *unordered* strategy, uses the normal
sparse execution engine of AIMMS but ignores the specified order of the
indices. This may, however, give different results, especially when the
``FOR`` loop contains one or more ``DISPLAY``/``PUT`` statements or uses
lag and lead operators in conjunction with one or more of the ordered
indices.

.. rubric:: Selecting a strategy

By prefixing the ``FOR`` statement with one of the keywords ``SPARSE``,
``ORDERED``, or ``UNORDERED`` (as explained in
:ref:`sec:exec.flow.for`), you can force AIMMS to adopt a particular
strategy. If you do not explicitly specify a strategy, AIMMS uses the
sparse strategy by default, and only issues a warning if an identifier
referenced inside the ``FOR`` loop is modified and the second evaluation
of ``Expression(i,j,k)`` gives a non-empty result.

.. rubric:: Improving efficiency

Given the above, you have the following options for improving the
efficiency of the ``FOR`` statement.

-  Rewrite the ``FOR`` statement such that the condition does not change
   during each iteration.

-  Prefix the ``FOR`` statement with the keyword ``UNORDERED`` such that
   the unordered strategy will be set. You can safely choose this
   strategy if the element order is not relevant for the ``FOR``
   statement. In all other cases, the semantics of the ``FOR`` statement
   will be changed.

-  Prefix the ``FOR`` statement with the keyword ``ORDERED`` such that
   the dense strategy is selected. You can safely choose this strategy
   if the condition on the running indices evaluates to true for a
   significant number of all possible combinations of the tuples
   ``(i,j,k)``.

-  Prefix the ``FOR`` statement with the keyword ``SPARSE`` to adopt the
   sparse strategy. However, all warnings will be suppressed relating to
   the condition on the running indices needing to be evaluated multiple
   times. You can choose this strategy if the condition needs to be
   re-evaluated in only a few iterations.

.. _subsection:eff.tuning-stmts.defs-for-loop:

Combining Definitions and ``FOR`` Loops
---------------------------------------

.. _sec:eff.definition:

.. rubric:: Dependency is symbolic

As explained in :ref:`sec:nonproc.dep`, the dependency structure between
set and parameter definitions is based only on symbol references. AIMMS'
evaluation scheme recomputes a defined parameter *in its entirety* even
if only a single element in its inputs has changed. This negatively
affects performance when such a defined parameter is used inside a
``FOR`` loop and its input is changed inside that same ``FOR`` loop.

.. rubric:: A simulation example

A typical example occurs when using definitions in simulations over
time. In simulations, computations are often performed period by period,
referring back to data from previous period(s). The relation used to
computate the stock of a particular product ``p`` in period ``t`` can
easily be expressed by the following definition and then used inside the
body of a procedure.

.. code-block:: aimms

	Parameter ProductStock {
	    IndexDomain  :  (p,t);
	    Definition   :  ProductStock(p,t-1) + Production(p,t) - Sales(p,t);
	}    
	Procedure ComputeProduction {
	    Body         : {
	        for ( t ) do
	            ! Compute Production(p,t) partly based on the stock for period (t-1)
	            Production(p,t) := Max( ProductionCapacity(p),
	                                    MaxStock(p) - ProductStock(p,t-1) + Sales(p,t) );
	        endfor ;
	    }
	}

During every iteration, the production in period ``t`` is computed on
the basis of the stock in the previous period and the maximum production
capacity. However, because of the dependency of ``ProductStock`` with
respect to ``Production``, AIMMS will re-evaluate the definition of
``ProductStock`` in its entirety for *each* period before executing the
assignment for the next period. Although the ``FOR`` loop is not really
necessary here, it is used for illustrative purposes.

.. rubric:: Improved formulation

In this example, execution times can be reduced by moving the definition
of ``ProductStock`` to an explicit assignment in the ``FOR`` loop.

.. code-block:: aimms

	Parameter ProductStock {
	    IndexDomain  :  (p,t);
	    ! Definition attribute is empty.
	}    
	Procedure ComputeProduction {
	    Body         : {
	        for ( t ) do
	            ! Compute Production(p,t) partly based on the stock for period (t-1)
	            Production(p,t) := Max( ProductionCapacity(p),
	                                    MaxStock(p) - ProductStock(p,t-1) + Sales(p,t) );

	            ! Then compute stocks for current period t
	            ProductStock(p,t) := ProductStock(p,t-1) + Production(p,t) - Sales(p,t);
	        endfor ;
	    }
	}

In this formulation, only one slice of the ``ProductStock`` parameter is
computed per period. A drawback of this formulation is that it will have
to be restated at various places in your model if the inputs of the
definition are assigned at several places in your model.

.. rubric:: Use of macros

As an alternative, you might consider the use of a ``Macro`` (see also
:ref:`sec:expr.macro`) to localize the defining expression of
``ProductStock`` at a single node in the model tree. The disadvantage of
macros is that they cannot be used in ``DISPLAY`` statements, or saved
to cases.

.. rubric:: When to avoid definitions

As illustrated above, it is best to avoid definitions, if, within a
``FOR`` loop, you only need a slice of that definition to modify the
inputs for another slice of that same definition. AIMMS is not designed
to recognize this situation and will repeatly evaluate the entire
definition. The AIMMS profiler will expose such definitions by their
high hitcount.

.. _subsection:eff.tuning-stmts.compl-expr:

Identifying Lower-Dimensional Subexpressions
--------------------------------------------

.. rubric:: Lower-dimensional subexpressions

Repeatedly performing the same computation is obviously a waste of time.
In this section, we will discuss a special, but not uncommon, instance
of such behavior, namely lower-dimensional sub-expressions. A lengthy
expression, that runs over several indices, can have distinct
subexpressions that depend on fewer indices. Let us illustrate this with
two examples, the first being an artificial example to explain the
principle, and the second a larger example that has actually been
encountered in practice and permits the discussion of related issues.

.. rubric:: Artificial example

Consider the following artificial example:

.. code-block:: aimms

	F(i,k) := G(i,k) * Sum[j | A(i,j) = B(i,j), H(j)] ;

For every value of ``i``, the sub-expression
``Sum[j | A(i,j) = B(i,j), H(j)]`` results in the same value for each
``k``. Currently, the AIMMS execution engine will repeatedly compute
this value. It is more efficient to rewrite the example as follows.

.. code-block:: aimms

	FP(i) := Sum[j | A(i,j) = B(i,j), H(j)] ;
	F(i,k) := G(i,k) * FP(i) ;

The principle of introducing an identifier for a specific sub-expression
often leads to dramatic performance improvements, as illustrated in the
following real-life example.

.. rubric:: A complicated assignment

Consider the following 4-dimensional assignment involving
region-terminal-terminal-region transports. Here, ``sr`` and ``dr``
(source region and destination region) are indices in a set of
``Regions`` with ``m`` elements and ``st`` and ``dt`` (source terminal
and destination terminal) are indices in a set of ``Terminals`` with
``n`` elements.

.. code-block:: aimms

	Transport( (sr,st,dt,dr) |          TRDistance(sr,st) <= MaxTRDistance(st) AND
	                                    TRDistance(dr,dt) <= MaxTRDistance(dt) AND
	   sr <> dr AND MinTransDistance <= RRDistance(sr,dr) <= MaxTransDistance  AND
	   st <> dt AND MinTransDistance <= TTDistance(st,dt) <= MaxTransDistance
	         ) := Demand(sr,dr);

The domain condition states that region-terminal-terminal-region
transport should only be assigned if the various distances between
regions and/or terminals satisfy the given bounds.

.. rubric:: Efficiency analysis

The ``<=`` operator is dense and be evaluated for all possible values of
the indices. The subexpression
``TRDistance(sr,st) <= MaxTRDistance(st)``, for example, will be
evaluated for every possible value of ``dr`` and ``dt``, even though it
only depends on ``sr`` and ``st``. In other words, we're computing the
same thing over and over again.

.. rubric:: Effect of the ``AND`` operator

There are multiple ``AND`` operators in this example. The ``AND``
operator is sparse, and oten, sparse operators make execution quick.
However, they fail to do just that in this particular example. Bear with
us. Although the ``AND`` operator is a sparse binary operator, its
effectiveness depends on how effectively the intersection is taken. What
are we taking the intersection of? If we consider a particular argument
of the ``AND`` operators: ``TRDistance(sr,st) <= MaxTRDistance(st)``, as
the operator ``<=`` is dense and this argument will be computed for all
tuples ``{(sr,st,dt,dr)}`` even though the results will be mostly 0.0's.
The domain of evaluation for this argument is thus the full Cartesian
product of four sets. The evaluation domain of the other arguments of
the ``AND`` operators will be the same. So, in this example, we are
repeatedly taking the intersection of a Cartesian product with itself,
resulting in that same Cartesian product. Thus, the ``AND`` operator
will be evaluated for all tuples in ``{(sr,st,dt,dr)}`` even though this
operator is sparse.

.. rubric:: Example reformulation

In the formulation below, we've named the following sub-expressions.

.. code-block:: aimms

	ConnectableRegionalTerminal( (sr,st) | TRDistance(sr,st) <= MaxTRDistance(st) ) := 1;

	ConnectableRegions( (sr,dr) | sr <> dr AND
	        MinTransDistance <= RRDistance(sr,dr) <= MaxTransDistance )  := 1;

	ConnectableTerminals( (st,dt) | st <> dt AND
	        MinTransDistance <= TTDistance(st,dt) <= MaxTransDistance )  := 1;

In each of these three assignments, each condition depends fully on the
running indices and thus its evaluation is not unnecessarily repeated.
By substituting the three newly introduced identifiers in the condition
the original assignment becomes:

.. code-block:: aimms

	Transport( (sr,st,dt,dr) |
	           ConnectableRegionalTerminal(sr,st)     AND
	           ConnectableRegionalTerminal(dr,dt)     AND
	           ConnectableRegions(sr,dr)              AND
	           ConnectableTerminals(st,dt) )
	         := Demand(sr,dr);

The newly created identifiers are all sparse, and the sparse operator
``AND`` can effectively use this created sparsity in its arguments.

.. rubric:: Effect of reformulation

A modified version of the above example was sent to us by a customer.
While the original formulation took several minutes to execute for a
given large dataset, the reformulation only took a few seconds.

.. rubric:: A bit of general advice

Perhaps a modeling style which avoids the need for substitutions is
best. The easy way is to let AIMMS identify the places in which such
substitutions can be made by switching the options in the option
category ``Aimms`` - ``Tuning`` -
``Substitute Lower Dimension Expressions`` to appropriate settings. The
disadvantage of this easy method is that some opportunities are missed
as AIMMS cannot guarantee the equivalence of the formulations, and some
replacements are missed. For instance, in the above example, AIMMS will
create an identifier for both ``TRDistance(sr,st) <= MaxTRDistance(st)``
and ``TRDistance(dr,dt) <= MaxTRDistance(dt)``, even though only one
suffices. You can avoid substitutions by keeping your expressions brief
relating only a few identifiers at a time. This will also help to keep
your model readable.

.. _subsection:eff.tuning-stmts.nz-defval:

Parameters with Non-Zero Defaults
---------------------------------

.. rubric:: Sparse execution expects 0.0's

Sparse execution is based on the effect of the number 0.0 on addition
and multiplication. When other numbers are used as a default, all
possible elements of these parameters need to be considered rather than
only the stored ones. The advice is not to use such parameters in
intensive computations. In the example below, the summation operator
will need to consider every possible element of ``P`` rather than only
its non-zeros.

.. code-block:: aimms

	Parameter P {
	    IndexDomain  :  (i,j);
	    Default      :  1;
	    Body         : {
	        CountP := Sum( (i,j), P(i,j) )
	    }
	}

.. rubric:: Appropriate use of default

Identifiers with a non-zero default, may be convenient, however, in the
interface of your application as the GUI of AIMMS can display
non-default elements only.

.. rubric:: The ``NonDefault`` function

For parameters with a non-zero default, you still may want to execute
only for its non-default values. For this purpose, the function
``NonDefault`` has been introduced. This function allows one to limit
execution to the data actually stored in such a parameter. Consider the
following example where the non defaults of ``P`` are summed:

.. code-block:: aimms

	CountP := Sum( (i,j)| NonDefault(P(i,j)), P(i,j) );

In the above example the summation is limited to only those entries in
``P(i,j)`` that are stored. If you would rather use familiar algebraic
notation, instead of the dedicated function ``NonDefault``, you can
change the above example to:

.. code-block:: aimms

	CountP := Sum( (i,j) | P(i,j) <> 1, P(i,j) );

This statement also sums only the non-default values of ``P``. AIMMS
recognizes this special use of the ``<>`` operator as actually using the
``NonDefault`` function; the summation operator will only consider the
tuples ``(i,j)`` that are actually stored for ``P``.

.. rubric:: Suffices of variables

Note that the suffices :ref:`.Lower` and :ref:`.Upper` of variables are like
parameters with a non-zero default. For example in a free variable the
default of the ``.lower`` suffix is ``-inf`` and the default of the
suffix ``.upper`` is ``inf``.

.. _subsection:eff.tuning-stmts.index-ordering:

Index Ordering
--------------

.. rubric:: Index ordering

In rare cases, the particular order of indices in a statement may have
an adverse effect on its performance. The efficiency aspects of index
ordering, when they occur, are inarguably the most difficult to
understand and recognize. Again, this inefficiency is best explained
using an example.

.. rubric:: An artificial example

Consider the following assignment statement:

.. code-block:: aimms

	FS(i,k) := Sum( j, A(i,j) * B(j,k) );

If ``A(i,j)`` and ``B(j,k)`` are binary parameters, where

-  for any given ``i``, the parameter ``A(i,j)`` maps to a single ``j``,
   and,

-  for any given ``j``, the parameter ``B(j,k)`` maps to a single ``k``,

one would intuitively expect that the assignment could be executed
rather efficiently. When actually executing the statement, it may
therefore come as an unpleasant surprise that it takes a seemingly
unexplainable amount of time.

.. rubric:: An analysis

In the qualitative analysis above, implicitly the index order ``i``
selects ``j``, and ``j`` selects a few ``k``\ 's, or, in AIMMS
terminology, a running index order ``[i,j,k]``. The actual running index
order of AIMMS is, however, first the indices ``[i,k]`` from the
assignment operator, followed by the index ``[j]`` from the summation
operator: ``[i,k,j]``. The effect of the actual index order is that, for
a given value of index ``i``, the relevant values of index ``k`` cannot
be restricted using the parameter chain ``A(i,j)``-``B(j,k)`` without
the aid of an intermediate running index ``j``. Consequently, AIMMS has
to try every combination of ``(i,k)``.

.. rubric:: Reformulation

Given the above analysis, the preferred index ordering ``[i,j,k]`` can
be accomplished by introducing an intermediate identifier
``FSH(i,j,k)``, and replacing the original assignment by the following
statements.

.. code-block:: aimms

	FSH(i,j,k) := A(i,j) * B(j,k);
	FS(i,k) := Sum( j, FSH(i,j,k) );

With a real-life example, where the range of the indices ``i``, ``j``
and ``k`` contained over 10000 elements, the observed improvement was
more than a factor 50.

.. rubric:: Not for ``+``

A similar improvement could be obtained for the following example:

.. code-block:: aimms

	FSP(i,k) := Sum( j, A(i,j) + B(j,k) );

Here a value is computed for each ``(i,k)`` of ``FSP``, because, for
every ``i``, there is a non-zero ``A(i,j)``, and for every ``k``, there
is a non-zero ``B(j,k)``.

.. _sec:eff.set.ordering:

Set Element Ordering
--------------------

.. rubric:: Data entry order
   :name: eff.set.ordering

By default, all elements in a root set are numbered internally by AIMMS
in a consecutive manner according to their *data entry order*, i.e. the
order in which the elements have been added to the set. Such additions
can be either explicit or implicit, and may take place, for example when
the model text contains references to explicit elements in the root set,
or by reading the set from files, databases, or cases.

.. rubric:: Multidimensional storage

The storage of multidimensional data defined over a root set is always
based on this internal and consecutive numbering of root set elements.
More explicitly, all tuple-value pairs associated with a
multidimensional identifier are stored according to a strict
right-to-left ordering based on the respective root set numberings.

.. rubric:: Indexed execution

By default, all indexed execution taking place in AIMMS, either through
implied loops induced by indexed assignments or through explicit ``FOR``
loops, employs the same strict right-to-left ordering of root set
elements. Thus, there is a perfect match between the execution order and
the order in which identifiers referenced in such loops are stored
internally. As a consequence, it is very easy for AIMMS to synchronize
the tuple for which execution is currently due with an ordered route
through all the non-zero tuples in the identifiers involved in the
statement. This principle is the basis of the sparse execution engine
underlying AIMMS.

.. rubric:: Execution over ordered sets

Inefficiency is introduced if the elements in a set over which a loop
takes place have been ordered differently from the data entry order,
either because of an ordering principle specified in the ``OrderBy``
attribute of the set declaration or through an explicit ``Sort``
operation. Consequently, there will no lomger be a direct match between
the execution order of the loop and the storage order of the non-zero
identifier values. Depending on the precise type of statement, this may
result in no, slight or serious increase in the execution time of the
statement, as AIMMS may have to perform randomly-placed lookups for
particular tuples. These random lookups are much more time consuming
than running over the data only once in an ordered fashion.

.. rubric:: Effect on ``FOR`` loops

In particular, you should avoid using ``FOR`` statements in which the
running index is an index in a set with a nondefault ordering whenever
possible. If not, AIMMS is forced to execute such ``FOR`` statements
using the imposed nondefault ordering and, as a result, *all* identifier
lookups within the ``FOR`` loop are random. In such a situation, you
should carefully consider whether ordered execution is really essential.
If not, it is advisable to leave the original set unordered, and create
an ordered *subset* (containing all the elements of the original set)
for use when the nondefault element ordering is required.

.. rubric:: Effect on assignments

In most situations, the efficiency of indexed assignments is not
affected by the use of indices in sets with a nondefault ordering. AIMMS
has only to rely on the nondefault ordering if an assignment contains
special order-dependent constructs such as lag and lead operators. In
all other cases, AIMMS can use the default data entry order.

.. rubric:: Complete reordering

If a nondefault ordering of some sets in your model causes a serious
increase in execution times, you may want to apply the
``CLEANDEPENDENTS`` statement (see also :ref:`sec:data.control`) to
those roots sets that are the cause of the increase of execution times.
The ``CLEANDEPENDENTS`` statement will fully renumber the elements in
the root set according to their current ordering, and rebuild all data
defined over it according to this new numbering.

.. rubric:: Use sparingly

As all identifiers defined over the root set have to be completely
rebuilt, ``CLEANDEPENDENTS`` is an inherently expensive operation. You
should, therefore, only use it when really necessary.

.. _subsection:eff.tuning-stmts.diagnostics:

Using AIMMS' Advanced Diagnostics
---------------------------------

.. rubric:: Using diagnostic warnings

In order to help you create correct and efficient applications, AIMMS is
regularly extended with diagnostics that incorporate the recognition of
new types of problematic situations. These diagnostics may help you
detect model formulations that lead to sub-optimal performance and/or
ambiguous results. These diagnostics can be controled through various
options in the **Warning** category.

.. rubric:: Apply diagnostics regularly

As the list of diagnostic options is regularly extended, and some of the
formulation problems depend on the model data and, thus, can only be
detected at runtime, you are advised to apply the diagnostics provided
by AIMMS on a regular basis during your application tests.
:ref:`sec:exec.error.warning` describes a way in which you can switch on
all the diagnostic options by just changing the value of the two options
``strict_warning_default`` and ``common_warning_default``.

.. rubric:: Diagnostic options

Below we provide a list of performance-related diagnostics that may help
you tune the performance of your model:

``Warning_repeated_iterative_evaluation``
   If the arguments of an iterative operator do not depend on some of
   the indices, the iterative operator is repeatedly evaluated with the
   same result. Consider the assignment ``a(i) := sum(j,b(j));`` in
   which the sum does not depend on the index ``i`` and so the same
   value is computed for every value of ``i``. See also
   :ref:`subsection:eff.tuning-stmts.compl-expr`.

``Warning_unused_index``
   If an index is not used inside the argument(s) or index domain
   condition of an iterative iterator, this leads to inefficient
   execution. In the assignment ``a(i) := sum((j,k),b(i,j));``, the
   index ``k`` is not used in the summation. Further, when an index in
   the index domain of a constraint is not used inside the definition of
   that constraint this is likely to lead to the generation of duplicate
   rows.

``Warning_duplicate_row``
   At the end of generating a mathematical program it is verified that
   there are no duplicate rows inside that mathematical program. This
   might be caused by two constraints having the same definition.
   Besides consuming more memory, duplicate rows cause the problem to
   become degenerate and may cause the problem to become more difficult
   to solve. This warning is not supported for mathematical programs of
   type MCP or MPCC because, for these types the row col mapping is also
   relevant and duplicate rows cannot be simply eliminated.

``Warning_duplicate_column``
   At the end of generating a mathematical progrram it is verified that
   there are no duplicate columns inside that mathematical program.
   Besides consuming more memory, duplicate columns result in the
   generated mathematical program having non-unique solutions.

``Warning_trivial_row``
   Generating and eliminating trivial rows such as :math:`0 <= 1` takes
   time.

The help for the option category ``AIMMS`` -
``Progress, errors & warnings`` - ``warnings`` provides more information
on these options.