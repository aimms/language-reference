.. _sec:gmp.intro:

Introduction to the GMP Library
===============================

.. rubric:: Introduction

With every ``MathematicalProgram`` declared as part of your model, the
GMP library allows you to associate

-  one or more **G**\ enerated\ **M**\ ath\ **P**\ rogram
   instances (GMPs),

and with each GMP

-  a conceptual matrix of coefficients that can be manipulated,

-  a repository of initial, intermediate or final solutions, and

-  a pool of local or remote solver sessions.

:numref:`fig:gmp.concepts` illustrates the interrelationship between
symbolic mathematical programs and the concepts of the GMP library, as
well as the main properties that can be associated with each of them.

.. figure:: introduction-to-the-gmp-library-pspic1.svg
   :name: fig:gmp.concepts
   :height: 524 px
   :width: 412 px
   :scale: 125 %

   Concepts associated with a GMP

.. rubric:: Generated mathematical program instances

For every ``MathematicalProgram`` declaration in your model,
modifications in the index sets and input data referenced in constraints
and variable definitions may give rise to completely different instances
of the coefficient matrix when the mathematical program at hand is being
generated.

.. rubric:: An example: indexed instances

An illustrative example of such differing instances occurs when the
constraints and variables of a symbolic mathematical program are indexed
over a subset of some other superset. If you let the subset contain a
single element of the superset, the generated instances will be
completely different for each element of the superset. The effect of
changing the contents of the subset in this manner, would almost compare
to having an indexed ``MathematicalProgram`` *declaration* (which AIMMS
does not support). In the worked example of
:ref:`sec:gmp.examples.indexed` you will see, however, how you can
obtain an indexed collection of generated mathematical program
*instances* using the GMP library.

.. rubric:: Need for multiple instances

With the standard ``SOLVE`` statement (see :ref:`sec:mp.solve`) you only
have access to a single generated mathematical program instance for
every symbolic mathematical program, namely the instance associated with
the last call to the ``SOLVE`` statement for that particular
mathematical program. This effectively eliminates the capability to
efficiently implement an algorithm which requires the interaction
between two or more generated instances of the same symbolic
mathematical program. For this reason, the GMP library allows you to
maintain and work with a collection of generated mathematical program
instances simultaneously.

.. rubric:: Matrix manipulation

The GMP library also allows you to manipulate the rows, columns and
coefficients of the matrix of a mathematical program instance once it
has been generated. If the number of modifications is relatively small,
manipulating the matrix directly will save a considerable amount of time
compared to letting AIMMS completely regenerate the matrix again through
the standard ``SOLVE`` statement. You can use matrix manipulation, for
instance

-  to quickly add columns, and adapt the existing rows of the matrix
   accordingly, in a column generation scheme, or

-  to dynamically add cuts to a mixed integer linear program.

.. rubric:: Keeping multiple solutions

With the standard ``SOLVE`` statement, you only have access to a single
solution of a mathematical program, namely the one stored in the
symbolic variables and constraints that make up the mathematical
program. There are, however, many situations where it would be
convenient to have access to a repository of solutions. A solution
repository can be used, for instance

-  to store a collection of starting solutions for a NLP or MINLP
   problem. Solving the problem, in either a serial or parallel manner,
   with each of these starting solutions may help you find a better
   solution than by simply solving the problem with only a single
   starting solution.

-  during the solution process of a mixed integer program, if you are
   interested in other integer solutions than the final solution
   returned by the solver. You can use the solution repository to store
   a fixed size collection of the best incumbent solutions returned by
   the solver during the solution process.

.. rubric:: Solution repository

The GMP library comes with a solution repository for each generated
mathematical program instance, and offers a number of functions to
easily transfer a solution from and to either

-  the data of the variables and constraints that make up the associated
   mathematical program in your model, or

-  any solver session (explained below) associated with the generated
   mathematical program instance.

In fact, in the GMP library there is no direct solution/starting point
transfer between a solver and the model, but such transfer always takes
place through the solution repository.

.. rubric:: Solver session pool

The final concept that is part of the GMP library is that of solver
sessions. In principle, the GMP library is prepared to allow a generated
mathematical program instance to keep a pool of associated solver
sessions, each possibly set up with a different solver, or with
different solver settings, and to be run either locally or remotely.

.. rubric:: When useful

Using multiple solver session it becomes possible, for example, to let
the same (or another) solver with different solver settings solve a
mixed integer program instance in parallel, and pass tighter bound
information found by one solver session to the other sessions by means
of a callback implemented in your model.

.. rubric:: ``GMP`` namespace

To prevent naming conflicts, all functions and procedure in the GMP
library are member of the predefined ``GMP`` namespace. The ``GMP``
namespace is further partitioned into the namespaces

-  ``GMP::Instance``,

-  ``GMP::Row``,

-  ``GMP::Column``,

-  ``GMP::Coefficient``,

-  ``GMP::Event``,

-  ``GMP::QuadraticCoefficient``,

-  ``GMP::Solution``,

-  ``GMP::SolverSession``,

-  ``GMP::Stochastic``,

-  ``GMP::Robust``,

-  ``GMP::Benders``,

-  ``GMP::Linearization``, and

-  ``GMP::ProgressWindow``.

In the following sections we will discuss the procedures and functions
contained in each of these namespaces.

.. rubric:: Return values

When using the GMP library, it may be particularly important to check
for any kind of error conditions that can occur. To help you catch such
errors, the procedures and functions in the ``GMP`` namespace either
return

-  a 1 when successful, or 0 otherwise (for procedures), or

-  a non-empty element in one of the GMP-related predefined sets when
   successful, or the empty element otherwise (for functions).

Note that, for the sake of brevity, most of the examples in this chapter
do not perform error checking of any kind.