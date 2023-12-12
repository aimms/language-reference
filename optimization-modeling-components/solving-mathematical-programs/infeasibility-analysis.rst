.. _sec:mp.infeas:

Infeasibility Analysis
======================

.. rubric:: Infeasibility analysis

One of the more daunting tasks in mathematical programming is to find
the cause of an infeasible mathematical program. Such infeasibilities
may occur

-  either when you are developing a new model due to modeling errors,

-  or in a complete (and well-tested), model-based, end-user application
   employed by your customers due to inconsistencies in the model data.

.. rubric:: Infeasibilities due to modeling errors

There are several types of modeling errors that you can make during the
development of a mathematical program that can lead to hard-to-explain
infeasibilities. The most common are:

-  simple typing errors, leading, for instance, to a wrong variable
   being referenced in a constraint,

-  a logical flaw in the model formulation, i.e. the formulation of one
   or more constraints just makes no sense,

-  the domain restriction of a constraint is not restrictive enough,
   i.e. constraints are generated that should not be generated,

-  the domain restriction of a variable is wrong, leading to too many or
   too few terms being generated in constraints referring to such a
   variable, or

-  the restriction in iterative operators (such as ``SUM`` or ``PROD``)
   in the definition of constraints or defined variables is wrong,
   leading to too many or too little terms being generated in that
   particular constraint.

In general, trying to find infeasibilities that occur during model
development may force you to generate a constraint listing of your
mathematical program and carefully examine the generated constraints in
order to find the modeling error.

.. rubric:: Infeasibilities due to data inconsistencies

Even when the formulation of a mathematical program is internally
consistent, and shipped as an end-user application to your customers,
infeasibilities may occur due to inconsistencies in the model data. The
most common data errors are:

-  inconsistencies in the structural data defining the topology of a
   model, e.g. in a network model a demand node may have been added for
   which no incoming arcs have been specified, or

-  inconsistencies in the quantitive model data, e.g. to total demand
   exceeds the total supply.

While most data inconsistencies may be detected by methodically checking
the consistency all input data prior to actually solving the
mathematical program (for example, by using ``Assertions``, see also
:ref:`sec:data.assert`), it is often hard to cover all possible data
inconsistencies.

.. rubric:: Adding excess variables

A commonly used approach to try and deal with infeasibilities, is to add
explicit excess variables to all or some constraints in a model, along
with a penalty term in the objective that will keep all excess variables
equal to 0 if the model is feasible. If this procedure is executed
properly, the *modified* mathematical program will always be feasible,
while the *original* mathematical program is feasible if and only if the
excess variables are all equal to 0. In the case of an infeasibility, an
examination of the excess variables may provide useful information about
the cause of infeasibility.

.. rubric:: Laborious procedure

While adding excess variables to your model may certainly help you to
resolve any infeasibilities, the process of manually adding these excess
variables to a mathematical program is laborious and error-prone:

-  you have to add the declarations of the excess variables for all (or
   some) constraints in your model,

-  the selected constraints have to be modified to include these excess
   variables, and

-  the objective has to be modified to include the excess-related
   penalty terms.

In addition, adding excess variables may considerably increase the size
of the generated matrix, so you may want to write supporting code to
exclude the excess variables from your mathematical program unless you
encounter an infeasibility.

.. _sec:mp.infeas.specifying:

Adding Infeasibility Analysis to Your Model
-------------------------------------------

.. rubric:: The ``ViolationPenalty`` attribute

To ease the manual process described above, AIMMS offers support to
*automatically* extend your mathematical program with excess variables
during the generation of the matrix for the solver. You enable this
feature through the ``ViolationPenalty`` attribute of a
``MathematicalProgram`` declaration. The value of the
``ViolationPenalty`` attribute must be either a

-  1-dimensional parameter with index domain
   :any:`AllVariablesConstraints`, or

-  2-dimensional parameter defined over :any:`AllVariablesConstraints` and
   :any:`AllViolationTypes`.

The predefined set :any:`AllVariablesConstraints` is a subset of the set
:any:`AllIdentifiers` and contains the names of all the variables and
constraints in your model. Through one of these two types of parameters
you can specify for which variables and constraints in your mathematical
program AIMMS must generate excess variables, as well as the penalty
coefficient of these excess variables in the modified objective.

.. rubric:: The set :any:`AllViolationTypes`

The predefined set :any:`AllViolationTypes` is a fixed set containing the
three types of possible violations for which AIMMS can generate excess
variables. The elements in the set :any:`AllViolationTypes` are

-  ``Lower``: generate excess variables for the violation of a lower
   bound,

-  ``Upper``: generate excess variables for the violation of an upper
   bound, and

-  ``Definition``: generate excess variables for the violation of the
   equality between a defined variable and its definition.

.. rubric:: Interpretation of ``ViolationPenalty`` attribute

If a parameter you entered in the ``ViolationPenalty`` attribute
contains no data, AIMMS will generate the mathematical program without
any generated excess variables. If you specify a 2-dimensional parameter
which is not empty, all values must be nonnegative or assume the special
value ``ZERO`` (see also :ref:`sec:expr.num.arith-ext`), and AIMMS will
interpret its contents as follows.

.. rubric:: Penalty for objective variable

The modified objective will include the original objective, unless a
value of ``ZERO`` has been assigned to ``Definition`` violation type for
the original objective variable. AIMMS will treat any other penalty
value than ``ZERO`` assigned to the objective variable as 1.0! Note that
by including the original objective the penalized mathematical program
may become unbounded.

.. rubric:: Penalty for constraints

AIMMS will add nonnegative excess variables for the violation of a
(finite) lower and/or upper bound of every constraint for which a
penalty value other than 0.0 has been specified for the ``Lower`` and/or
``Upper`` violation type, respectively. If a bound is infinite, no
corresponding excess variable will be generated. A penalty term will be
added to the modified objective consisting of the product of the
specified (nonnegative) penalty coefficient times the excess variable
associated with the constraint, unless a penalty of ``ZERO`` has been
specified in which case the corresponding term will not be added to the
modified objective.

.. rubric:: Penalty for variables

AIMMS will add nonnegative excess variables for the violation of a
(finite) lower and/or upper bound of every variable for which a penalty
value other than 0.0 has been specified for the ``Lower`` and/or
``Upper`` violation type, respectively. If a bound is infinite, no
corresponding excess variable will be generated. A penalty term will be
added to the modified objective consisting of the product of the
specified (nonnegative) penalty coefficient times the excess variable
associated with the variable, unless a penalty of ``ZERO`` has been
specified in which case the corresponding term will not be added to the
modified objective. The effect of using ``Lower`` and/or ``Upper``
violations is that the variable can assume values outside their bounds
throughout the mathematical program.

.. rubric:: Penalty for variable definitions

AIMMS will add nonnegative excess variables for the violation of the
equality between a defined variable and its definition for every defined
variable for which a penalty value other than 0.0 has been specified for
the ``Definition`` violation type. A penalty term will be added to the
modified objective consisting of the product of the specified
(nonnegative) penalty times the excess variable(s) associated with the
constraint expressing the equality, unless a penalty of ``ZERO`` has
been specified in which case the corresponding term(s) will not be added
to the modified objective.

.. rubric:: Definition versus lower/upper violations

You can both use the ``Lower`` and/or ``Upper`` violation types and
``Definition`` violation type to compensate for a violation between the
value of the defined variable and its definition. However, when you use
the ``Definition`` violation type, the value of the variable will remain
within its specified bounds throughout the mathematical program. It is
up to you to decide which violation type suits your needs best for a
particular defined variable.

.. rubric:: Interpretation of 1-dimensional parameter

If you specify a 1-dimensional parameter for the ``ViolationPenalty``
attribute, AIMMS will interpret this parameter as if it were a
2-dimensional parameter, with the same value for all three violation
types ``Lower``, ``Upper`` and ``Definition``.

.. rubric:: FeasOpt and FeasRelax

Gurobi and CPLEX offer functionality to extend the method of Violation 
Penalties described in this section. If the option 
``Feasibility relaxation`` is set to ``'advanced'``, AIMMS will call 
FeasOpt (CPLEX) or FeasRelax (Gurobi). Note that this option is only 
available for these two solvers. 

As before, AIMMS will still automatically generate the violation 
variables. However, there are some differences.  

For the default method of handling Violation Penalties, AIMMS will 
add the penalty term to the original objective function (unless a value 
of ``ZERO`` has been assigned to ``Definition`` violation type for the 
original objective variable). In contrast, for FeasOpt and FeasRelax 
the objective will ignore the original objective. This allows the user 
to compute a minimum cost relaxation. 

Additionally,  the user can choose between several objective metrics. 
The objective metric can be set in the option 
``Feasibility relaxation objective``. The options are: 
-  ``'weighted sum of violations'``, 
-  ``'weighted sum of squared violations'``,  
-  ``'weighed number of violations'``.  

Optionally, after the first phase of computing a minimum cost relaxation, 
the user can choose to activate a second phase. In the second phase, the 
original objective is optimized among all minimum cost relaxations. 
The second phase can be activated by using the option 
``Feasibility relaxation optimize original objective``. 

Some other difference are: 
-  CPLEX and Gurobi are unable to process ``ZERO`` violation 
penalties. The violation variables are generated AIMMS, but these 
variables are not sent to the FeasOpt/FeasRelax model
-  The ``Definition`` penalty values are ignored for FeasOpt/FeasRelax 
model. 


.. _sec:mp.infeas.inspect:

Inspecting Your Model for Infeasibilities
-----------------------------------------

.. rubric:: Finding violations

After you have let AIMMS extend your model with excess variables to find
an infeasibility, you must inspect the variables and constraints in your
model to find the violations. AIMMS allows you to do this through the
use of two suffices, the :ref:`.Violation` suffix and the
:ref:`.DefinitionViolation` suffix.

.. rubric:: The :ref:`.Violation` suffix...

The :ref:`.Violation` suffix denotes the amount by which a variable or
constraint violates its lower or upper bound. If you have specified a
nonzero violation penalty for the ``Upper`` violation type, the
:ref:`.Violation` suffix can assume positive values, while it can assume
negative values whenever you have specified a nonzero violation penalty
for the ``Lower`` violation type.

.. rubric:: ... for variables

For variables the :ref:`.Violation` suffix denotes the amount by which the
variable violates its

-  upper bound (if the suffix assumes a positive value), or

-  lower bound (if the suffix assumes a negative value).

.. rubric:: ... for constraints

For constraints the :ref:`.Violation` suffix denotes the amount by which
the constraint violates its

-  upper bound (if the suffix assumes a positive value),

-  lower bound (if the suffix assumes a negative value, for ranged
   constraints).

If the constraint is an equality constraint, the :ref:`.Violation` suffix
denotes the (positive or negative) amount by which the left hand side
differs from the (constant) right hand side.

.. rubric:: The :ref:`.DefinitionViolation` suffix

With the :ref:`.DefinitionViolation` suffix, you can locate violations in
the definitions of defined variables for which you have specified a
positive penalty for the ``Definition`` violation type. The value of the
suffix denotes the (positive or negative) amount by which the defined
variable differs from its definition. Note that a defined variable may
violate both its bounds and its definition, depending on the type of
allowed violations you have specified.

.. rubric:: Locating violations

To locate violations in a model which was extended by AIMMS with excess
variables, you may use the :any:`Card` function to locate variables and
constraints with nonzero ``.Violations`` suffices. The following example
shows how to proceed, where ``v`` is assumed to be an index in
:any:`AllVariables`.

.. code-block:: aimms

	for ( v | Card(v, 'Violation') ) do

	    ! Take any action that you want to perform on this violated variable

	endfor;

.. _sec:mp.infeas.goal-programming:

Application to Goal Programming
-------------------------------

.. rubric:: Goal programming ...

In goal programming a distinction is made between *hard constraints*
that cannot be violated and *soft constraints*, which represent goals or
targets one would like to achieve. The objective function in goal
programming is to minimize the weighted sum of deviations from the goals
set by the soft constraints.

.. rubric:: ...interpreted as violations

In AIMMS, goal programming can be easily implemented using the
``ViolationPenalty`` attribute of a mathematical program, without the
need to modify the formulation of all soft constraints. For each soft
constraint in your goal programming model, you can assign the
appropriate weight to the ``ViolationPenalty`` attribute to penalize
deviations from the set target for that constraint.

.. rubric:: Inspecting deviations

Through the :ref:`.Violation` suffix of constraints and variables you can
inspect the deviations from the goals of the soft constraints in your
goal programming model.
