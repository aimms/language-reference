.. _sec:compl.intro:

Complementarity Problems
========================

.. rubric:: Complementarity problems

Complementarity relations arise in a variety of engineering and
economics applications, most commonly to express an equilibrium of
quantities such as forces or prices. One standard application in
engineering arises in contact mechanics, where complementarity expresses
the fact that friction occurs only when two bodies are in contact. Other
applications are found in structural mechanics, structural design,
traffic equilibrium and optimal control.

.. rubric:: Economic models

Interest among economists in solving complementarity problems is due in
part to increased use of computational general equilibrium models, where
for instance complementarity is used to express Walras' Law, and in part
to the equivalence of various games to complementarity problems.

.. rubric:: Nonlinear optimization

Some generalizations of nonlinear programming, such as multi-level
optimization-in which auxiliary objectives are to be minimized-may be
reformulated as problems with complementarity conditions. Also, by
formulating the Kuhn-Tucker conditions of a nonlinear optimization model
one obtains a complementarity problem, which could be solved by a
complementarity solver. In the latter case, however, one requires
second-order derivative information of all constraints in the original
optimization model.

.. rubric:: Complementarity conditions

Complementarity problems are, in general, systems of nonlinear
constraints where variables in the system are linked to constraints in
the form of complementarity conditions. There are two forms of
complementarity conditions, the classical complementarity condition, and
its generalization, the mixed complementarity condition.

.. rubric:: Classical complementarity conditions

The classical form of a complementarity condition involves a nonnegative
variable :math:`x_i` and an associated function :math:`f_i(x)`. It
requires that

.. math::

   \begin{align}
   x_i = 0 &\quad\text{and}\quad f_i(x) \geq 0, \text{ or}\\
       x_i > 0 &\quad\text{and}\quad f_i(x) = 0.
   \end{align}

This condition states that of both inequalities, at least one must reach
its bound. Alternatively, one can formulate this complementarity
condition as :math:`x_i
\geq 0`, :math:`f_i(x) \geq 0` and :math:`x_i\cdot f_i(x) = 0`.

.. rubric:: Mixed complementarity condition

The mixed form of a complementarity condition involves a bounded
variable :math:`l_i\leq x_i\leq u_i` with an associated function
:math:`f_i(x)`. It requires that

.. math::

   \begin{align}
   x_i = l_i &\quad\text{and}\quad f_i(x) \geq 0, \text{ or}\\
       x_i = u_i &\quad\text{and}\quad f_i(x) \leq 0, \text{ or}\\
       l_i < x_i < u_i &\quad\text{and}\quad f_i(x) = 0.
   \end{align}

This condition states that either :math:`x_i` must reach one of its
bounds, or the function :math:`f_i(x)` must be zero. A mixed
complementarity condition can be split into two classical
complementarity conditions (albeit by introducing auxiliary variables).
The classical complementarity condition, on the other hand, is a special
case of the mixed complementarity condition by choosing :math:`l_i = 0`
and :math:`u_i = \infty`.

.. rubric:: Special cases

By choosing :math:`l_i = -\infty` and :math:`u_i = \infty`, the mixed
complementarity condition reduces to the special case

.. math:: x_i \text{ is ``free''}\quad \text{and}\quad f_i(x) = 0.

Another special case is obtained when :math:`l_i = u_i`. The mixed
complementarity condition then reduces to

.. math:: x_i = l_i \quad \text{and}\quad f_i(x) \text{ is ``free''}

.. rubric:: Supported complementarity conditions in AIMMS

All complementarity conditions described above can be represented by
associating a variable with a single constraint, which will form the
basis for representing complementarity conditions in AIMMS. Consider the
inequalities

.. math:: l_{x_i} \leq x_i \leq u_{x_i} \quad\text{and}\quad l_{f_i} \leq f_i(x) \leq u_{f_i}

where :math:`f_i(x)` is a nonlinear expression, and *exactly* two of the
constants :math:`l_{x_i}`, :math:`u_{x_i}`, :math:`l_{f_i}` and
:math:`u_{f_i}` are finite. The six possible cases are enumerated in
:numref:`table:compl.poss`, and are discussed below.

.. _table:compl.poss:

.. table:: Six allowed cases with exactly two finite bounds

	==== =============== =============== =============== ===============
	Case :math:`l_{x_i}` :math:`u_{x_i}` :math:`l_{f_i}` :math:`u_{f_i}`
	==== =============== =============== =============== ===============
	1    finite          finite          :math:`-\infty` :math:`\infty`
	2    finite          :math:`\infty`  finite          :math:`\infty`
	3    finite          :math:`\infty`  :math:`-\infty` finite
	4    :math:`-\infty` finite          finite          :math:`\infty`
	5    :math:`-\infty` finite          :math:`-\infty` finite
	6    :math:`-\infty` :math:`\infty`  finite          finite
	==== =============== =============== =============== ===============

.. rubric:: Case 1

The case :math:`l_{x_i} \leq x_i \leq u_{x_i}` and
:math:`-\infty \leq f_i(x) \leq \infty` corresponds to the mixed
complementarity condition already discussed above:

.. math::

   \begin{align}
   x_i = l_{x_i} &\quad\text{and}\quad f_i(x) \geq 0, \text{ or}\\
       x_i = u_{x_i} &\quad\text{and}\quad f_i(x) \leq 0, \text{ or}\\
       l_{x_i} < x_i < u_{x_i} &\quad\text{and}\quad f_i(x) = 0.
   \end{align}

.. rubric:: Case 2

The case :math:`l_{x_i} \leq x_i \leq \infty` and
:math:`l_{f_i} \leq f_i(x) \leq \infty` corresponds to the classical
complementarity condition

.. math::

   \begin{align}
   \hat{x}_i = 0 &\quad\text{and}\quad \hat{f}_i(x) \geq 0, \text{ or}\\
       \hat{x}_i > 0 &\quad\text{and}\quad \hat{f}_i(x) = 0.
   \end{align}

where :math:`\hat{x}_i = x_i - l_{x_i}` and
:math:`\hat{f}_i(x) = f_i(x) - l_{f_i}`.

.. rubric:: Case 3

The case :math:`l_{x_i} \leq x_i \leq \infty` and
:math:`-\infty \leq f_i(x) \leq u_{f_i}` corresponds to the classical
complementarity condition

.. math::

   \begin{align}
   \hat{x}_i = 0 &\quad\text{and}\quad \hat{f}_i(x) \geq 0, \text{ or}\\
       \hat{x}_i > 0 &\quad\text{and}\quad \hat{f}_i(x) = 0.
   \end{align}

where :math:`\hat{x}_i = x_i - l_{x_i}` and
:math:`\hat{f}_i(x) = u_{f_i} - f_i(x)`.

.. rubric:: Case 4

The case :math:`-\infty \leq x_i \leq u_{x_i}` and
:math:`l_{f_i} \leq f_i(x) \leq \infty` corresponds to the classical
complementarity condition

.. math::

   \begin{align}
   \hat{x}_i = 0 &\quad\text{and}\quad \hat{f}_i(x) \geq 0, \text{ or}\\
       \hat{x}_i > 0 &\quad\text{and}\quad \hat{f}_i(x) = 0.
   \end{align}

where :math:`\hat{x}_i = u_{x_i} - x_i` and
:math:`\hat{f}_i(x) = f_i(x) - l_{f_i}`.

.. rubric:: Case 5

The case :math:`-\infty \leq x_i \leq u_{x_i}` and
:math:`-\infty \leq f_i(x) \leq
u_{f_i}` corresponds to the classical complementarity condition

.. math::

   \begin{align}
   \hat{x}_i = 0 &\quad\text{and}\quad \hat{f}_i(x) \geq 0, \text{ or}\\
       \hat{x}_i > 0 &\quad\text{and}\quad \hat{f}_i(x) = 0.
   \end{align}

where :math:`\hat{x}_i = u_{x_i} - x_i` and
:math:`\hat{f}_i(x) = u_{f_i} - f_i(x)`.

.. rubric:: Case 6:

The case :math:`-\infty \leq x_i \leq \infty` and
:math:`l_{f_i} \leq f_i(x) \leq u_{f_i}` with :math:`l_{f_i} = u_{f_i}`
corresponds to the first special case of the mixed complementarity
condition

.. math:: x_i \text{ is ``free''}\quad \text{and}\quad \hat{f}_i(x) = 0.

where :math:`\hat{f}(x) = f_i(x) - l_{f_i}`.

.. rubric:: Case 6:

After the introduction of variables :math:`x_i^+, x_i^- \geq 0` and
functions

.. math::

   \begin{align}
   f_i^x(x) &= x_i - x_i^+ - x_i^-\\
       f_i^+(x) &= f_i(x) - l_{f_i}\\
       f_i^-(x) &= u_{f_i} - f_i(x)
   \end{align}

the case :math:`-\infty \leq x_i \leq \infty` and
:math:`l_{f_i} \leq f_i(x) \leq u_{f_i}` with :math:`l_{f_i} < u_{f_i}`
corresponds to a system of three simultaneous complementarity conditions

.. math::

   \begin{align}
   x_i \text{ is ``free''}&\quad \text{and}\quad f_i^x(x) = 0\\
                   & \\
       x_i^+ = 0 &\quad\text{and}\quad f_i^+(x) \geq 0, \text{ or}\\
       x_i^+ > 0 &\quad\text{and}\quad f_i^+(x) = 0 \\
                   & \\
       x_i^- = 0 &\quad\text{and}\quad f_i^-(x) \geq 0, \text{ or}\\
       x_i^- > 0 &\quad\text{and}\quad f_i^-(x) = 0.
   \end{align}

.. rubric:: AIMMS support

AIMMS supports the variable-constraint couples with two finite bounds,
as discussed above, through the special ``ComplementaryVariable`` data
type. The declaration and attributes of this data type are discussed in
the next section, while :ref:`sec:compl.mp` describes the declaration of
mixed complementarity models through the common ``MathematicalProgram``
declaration.

.. rubric:: Well-behaved systems

Like with nonlinear optimization models, not all mixed complementarity
systems that can be formulated are well-behaved. For instance, a
variable :math:`x \geq 0` with an associated constraint
:math:`1-x\geq 0`, only admits the solutions 0 and 1, which would
destroy the continuous character of complementarity problems. For
systems of complementarity conditions that are not well-behaved, the
solution process may produce no, or unexpected results.