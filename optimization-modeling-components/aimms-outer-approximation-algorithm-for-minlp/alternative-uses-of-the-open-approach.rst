.. _sc:aoa:alternative_uses:

Alternative Uses of the Open Approach
=====================================

.. rubric:: Customize algorithm

Using the open outer approximation approach for solving MINLP models it
is possible to add to the existing procedures or write alternative
procedures to meet the needs of the final user. For instance, a user
evaluating the performance of the algorithm may want to add certain
performance measurements and print statements to the existing code. Some
less trivial examples of modifications are provided in the next few
paragraphs.

.. rubric:: Solve more NLPs

Practical experience has shown that it is sometimes difficult to get a
feasible solution to the initial relaxed NLP model. Based on the
particular application, the user may specify how multiple starting
values can be found, and then modify the algorithm to solve multiple
NLPs to get a feasible and/or a better solution. While doing so, it is
also possible to specify how the algorithm should switch between
different solvers (using the predefined AIMMS identifier
:any:`CurrentSolver`). Such extensions could then also be applied to the
NLP subproblem inside the ``While`` statement.

.. rubric:: Retain integer solutions

It is possible to activate a MIP callback procedure whenever the MIP
solver finds an integer solution. Even though these intermediate
solutions are not optimal, the user may want to save the integer portion
of these solutions for later evaluation. Once the main algorithm has
terminated, all these integer solutions can be retrieved and evaluated
by solving the corresponding nonlinear subproblem. In some instances,
one of these extra solutions may be a better solution to the original
MINLP model than the one produced by the main algorithm.

.. rubric:: Adjust penalties

Setting the penalties for the deviations of the linear approximation
constraints in the master MIP subproblem is a delicate manner, and has
an effect on the solution quality when the nonlinear subproblems are
nonconvex. The user can consider several problem-dependent strategies to
adjust the penalty values, and implement them inside the basic AOA
algorithm.

.. rubric:: Example of modified procedure

The following procedure is a variant of the termination procedure
provided in the previous section. Assuming that the two parameters that
refer to the previous and current NLP objective function values have
been properly set in the procedure that solves the NLP subproblem, then
termination is invoked whenever there is insufficient progress between
two subsequent NLP solutions, or between the objective values of the
master MIP problem and the current NLP subproblem. The third termination
criterion is the number of iterations reaching its maximum.

.. code-block:: aimms

	return when ( MINLPAlgorithmHasFinished );

	if    (not MINLPSolutionImprovement( NLPCurrentObjectiveValue,
	                                     NLPPreviousObjectiveValue ))
	   or (not MINLPSolutionImprovement( GMP::Solution::GetObjective(GMINLP, SolNumb),
	                                     NLPCurrentObjectiveValue ))
	   or ( IterationCounter = IterationMax ) then

	    MINLPTerminate;

	else
	    ! Prepare for next iteration

	    IterationCount += 1 ;
	    GMP::Solution::SetIterationCount( GMINLP, SolNumb, IterationCount ) ;
	    GMP::Instance::AddIntegerEliminationRows( GMIP, SolNumb, EliminationCount ) ;
	    EliminationCount += 1 ;
	endif ;

.. rubric:: Conclusion

The above paragraphs indicate just a few of the ways in which you can
alter the basic implementation of the outer approximation algorithm in
AIMMS. Of course, it is not necessary to develop your own variant.
Whenever you need to solve a MINLP model using the AOA algorithm, you
can simply call the basic implementation described in the previous
section. As soon as you can see improved ways to solve a particular
model, you can apply your own ideas by modifying the procedures as you
see fit.