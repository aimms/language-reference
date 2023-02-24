.. _sec:gmp.matrix:

Matrix Manipulation Procedures
==============================

.. rubric:: Matrix manipulation

The matrix manipulation procedures in the GMP library allow you to
implement efficient algorithms for generated mathematical program
instances which require only slight modifications of the matrix
associated with the mathematical program instance during successive
runs. These procedures operate directly on the coefficient matrix
underlying the mathematical program, and thus avoid the
constraint-generation process normally initiated by the ``SOLVE``
statement after input data has been modified.

.. rubric:: This section

Prior to discussing the individual matrix manipulation procedures, the
following section will provide some motivation when and when not to use
matrix manipulation.

When to Use Matrix Manipulation
-------------------------------

.. rubric:: When to use matrix manipulation

Even though AIMMS offers a library of matrix manipulation procedures,
you should not use them blindly. As explained below, it is important to
distinguish between manual and automatic input data changes inside an
AIMMS application. Your decision whether or not to use the matrix
manipulation procedures described in this section, should depend on this
distinction.

.. rubric:: Manual data input ...

Consider an end-user of an AIMMS application who, after having looked at
the results of a mathematical program, wants to make changes in the
input data and then look again at the new solution of the mathematical
program. The effect of the data changes on the input to the solver
cannot be predicted in advance. Even a single data change could lead to
multiple changes in the input to the solver, and could also cause a
change in the number of constraints and variables inside the particular
mathematical program.

.. rubric:: ...requires structure recognition

As a result, AIMMS has to determine whether or not the structure of the
underlying mathematical program has changed. Only then can AIMMS decide
whether the value of existing coefficients can be overwritten, or
whether a new and structurally different data set has to be provided to
the solver. This structure recognition step is time consuming, and
cannot be avoided in the absence of any further information concerning
the changes in input data.

.. rubric:: Automatic data input ...

Whenever input data are changed inside an AIMMS procedure, their effect
on the input to the solver can usually be determined in advance. This
effect may be nontrivial, in which case it is not worth the effort to
establish the consequences. Rather, letting AIMMS perform the required
structure recognition step through the regular ``SOLVE`` statement
before passing new information to the solver seems to be a better
remedy. There are several instances, however, in which the effect of
data changes on the solver input data is easy to determine.

.. rubric:: ...may reflect particular structure

Consider, for instance, automatic data changes that have a one-to-one
correspondence with values in the underlying mathematical program. In
these instances, the incidence of variables in constraints is not
modified, and only the replacement values of some coefficients need to
be supplied to the particular solver. Other examples include automatic
data changes that could create new values for particular
variable-constraint combinations, or that could even cause new
constraints or variables to be added to the input of the solver. In all
these instances, the exact effects on the input of the solver can easily
be determined in advance, and there is no need to let AIMMS perform of
the computationally intensive structure recognition step of the
``SOLVE`` statement before passing new information to the solver.

.. rubric:: Restrictions on usage

The above effects of data input modifications on the input to the solver
are straightforward to implement with linear and quadratic mathematical
programs, because the underlying data structures are matrices with rows,
columns and nonzero elements. The input data structures for nonlinear
mathematical programs are essentially nonlinear expressions.
Modifications of the type discussed in the previous paragraph are not
easily passed onto these nonlinear data structures. For this reason, the
efficient updating of solver input has been confined to

-  linear and quadratic constraints, and

-  coefficients of nonlinear constraints with respect to variables that
   only occur linearly in that constraint.

.. rubric:: Regeneration of nonlinear constraints

Whenever the input data of a nonlinear expression in a nonlinear
constraint has changed, it is not possible anymore to change the
nonlinear expression used by the solver directly to reflect the data
change. You can still request AIMMS to regenerate the entire row, which
will then use the updated inputs. You should note, however, that any
modifications to the linear part of the regenerated constraint are lost
after the constraint has been regenerated.

.. rubric:: Scalar arguments only

All matrix procedures listed in
:ref:`this table <table:gmp.coefficient>`-:ref:`this table <table:gmp.column>` and most
procedures listed in :ref:`this table <table:gmp.linearization>` have
scalar-valued arguments. The *row* argument should always be

-  a scalar reference to an existing constraint name in your model, or

-  a row number which is an integer in the range :math:`\{ 0 .. m-1 \}`
   whereby :math:`m` is the number of rows.

The *column* argument should always be

-  a scalar reference to an existing variable name in your model, or

-  a column number which is an integer in the range
   :math:`\{ 0 .. n-1 \}` whereby :math:`n` is the number of columns.

.. rubric:: Modifying a group of columns or rows

For most matrix procedures listed in
:ref:`this table <table:gmp.coefficient>`-:ref:`this table <table:gmp.column>`, that can be
used to modify a generated mathematical program, there also exists a *multi* variant which can be
applied to a group of columns of rows, belonging to one variable or constraint respectively. These
procedures are listed in :ref:`sec:matrix.multiproc`.

.. rubric:: Mathematical program instance required

Before you can apply any of the procedures of
:ref:`this table <table:gmp.coefficient>`-:ref:`this table <table:gmp.column>`, you must
first create a mathematical program instance using any of the functions
for this purpose discussed in :ref:`sec:gmp.instance`. Either of these
methods will set up the initial row-column matrix required by the matrix
manipulation procedures. Also, any row or column referenced in the
matrix manipulation procedures must either have been generated during
the initial generation step, or must have been generated later on by a
call to the procedures :any:`GMP::Row::Add`, or :any:`GMP::Column::Add`,
respectively.

.. _sec:gmp.matrix.coefficient:

Coefficient Modification Procedures
-----------------------------------

.. rubric:: Coefficient modification procedures

The procedures and functions of the ``GMP::Coefficient`` namespace are
listed in :ref:`this table <table:gmp.coefficient>` and take care of the
modification of coefficients in the matrix and objective of a generated
mathematical program instance.

.. _GMP::Coefficient::SetQuadratic-LR:

.. _GMP::Coefficient::GetQuadratic-LR:

.. _GMP::Coefficient::Set-LR:

.. _GMP::Coefficient::Get-LR:

.. _GMP::Coefficient::GetMinAndMax-LR:

.. _table:gmp.coefficient:

.. table:: : ``GMP::Coefficient`` routines

	+-------------------------------------------------------------------------------------------------------------------------+
	| :any:`Get <GMP::Coefficient::Get>`\ (*GMP*, *row*, *column*)                                                            |
	+-------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetMinAndMax <GMP::Coefficient::GetMinAndMax>`\ (*GMP*, *rowSet*, *colSet*, *minCoef*, *maxCoef*\ [, *absSense*]) |
	+-------------------------------------------------------------------------------------------------------------------------+
	| :any:`Set <GMP::Coefficient::Set>`\ (*GMP*, *row*, *column*, *value*)                                                   |
	+-------------------------------------------------------------------------------------------------------------------------+
	| :any:`GetQuadratic <GMP::Coefficient::GetQuadratic>`\ (*GMP*, *column1*, *column2*)                                     |
	+-------------------------------------------------------------------------------------------------------------------------+
	| :any:`SetQuadratic <GMP::Coefficient::SetQuadratic>`\ (*GMP*, *column1*, *column2*, *value*)                            |
	+-------------------------------------------------------------------------------------------------------------------------+
	
.. rubric:: Modifying coefficients

You can instruct AIMMS to modify any particular coefficient in a matrix
by specifying the corresponding row and column (in AIMMS notation),
together with the new value of that coefficient, as arguments of the
procedure :any:`GMP::Coefficient::Set`. This procedure can also be used
when a value for the coefficient does not exist prior to calling the
procedure.

.. rubric:: Quadratic coefficients

For quadratic mathematical programs, you can modify the quadratic
objective coefficients by applying the function
:any:`GMP::Coefficient::SetQuadratic` to the objective row. For every two
columns :math:`x_1` and :math:`x_2` you can specify the modified
coefficient :math:`c_{12}` if :math:`c_{12}x_1x_2` is to be part of the
quadratic objective.

.. _sec:gmp.matrix.quadratic:

Quadratic Coefficient Modification Procedures
---------------------------------------------

.. rubric:: Quadratic coefficient modification procedures

The procedures and functions of the ``GMP::QuadraticCoefficient``
namespace are listed in :ref:`this table <table:gmp.quadratic>` and take care of
the modification of coefficients of quadratic rows in the matrix other
than the objective of a generated mathematical program instance.

.. _GMP::QuadraticCoefficient::Set-LR:

.. _GMP::QuadraticCoefficient::Get-LR:

.. _table:gmp.quadratic:

.. table:: : ``GMP::QuadraticCoefficient`` routines

	+--------------------------------------------------------------------------------------------+
	| :any:`Get <GMP::QuadraticCoefficient::Get>`\ (*GMP*, *row*, *column1*, *column2*)          |
	+--------------------------------------------------------------------------------------------+
	| :any:`Set <GMP::QuadraticCoefficient::Set>`\ (*GMP*, *row*, *column1*, *column2*, *value*) |
	+--------------------------------------------------------------------------------------------+
	
.. rubric:: Modifying coefficients

You can instruct AIMMS to modify any particular quadratic coefficient in
a matrix by specifying the corresponding row and columns (in AIMMS
notation), together with the new value of that coefficient, as arguments
of the procedure :any:`GMP::QuadraticCoefficient::Set`. This procedure can
also be used when a value for the quadratic coefficient does not exist
prior to calling the procedure.

.. _sec:gmp.matrix.row:

Row Modification Procedures
---------------------------

.. rubric:: Row modification procedures

The procedures and functions of the ``GMP::Row`` namespace are listed in
:ref:`this table <table:gmp.row>` and take care of the modification of properties
of existing rows and the creation of new rows.

.. _GMP::Row::SetPoolType-LR:

.. _GMP::Row::GetStatus-LR:

.. _GMP::Row::SetRelaxationOnly-LR:

.. _GMP::Row::SetConvex-LR:

.. _GMP::Row::GetRelaxationOnly-LR:

.. _GMP::Row::GetConvex-LR:

.. _GMP::Row::SetIndicatorCondition-LR:

.. _GMP::Row::GetIndicatorCondition-LR:

.. _GMP::Row::GetIndicatorColumn-LR:

.. _GMP::Row::DeleteIndicatorCondition-LR:

.. _GMP::Row::SetType-LR:

.. _GMP::Row::GetType-LR:

.. _GMP::Row::SetRightHandSide-LR:

.. _GMP::Row::GetRightHandSide-LR:

.. _GMP::Row::SetLeftHandSide-LR:

.. _GMP::Row::GetLeftHandSide-LR:

.. _GMP::Row::Generate-LR:

.. _GMP::Row::Deactivate-LR:

.. _GMP::Row::Activate-LR:

.. _GMP::Row::Delete-LR:

.. _GMP::Row::Add-LR:

.. _table:gmp.row:

.. table:: : ``GMP::Row`` routines

	+---------------------------------------------------------------------------------------------------+
	| :any:`Add <GMP::Row::Add>`\ (*GMP*, *row*)                                                        |
	+---------------------------------------------------------------------------------------------------+
	| :any:`Delete <GMP::Row::Delete>`\ (*GMP*, *row*)                                                  |
	+---------------------------------------------------------------------------------------------------+
	| :any:`Activate <GMP::Row::Activate>`\ (*GMP*, *row*)                                              |
	+---------------------------------------------------------------------------------------------------+
	| :any:`Deactivate <GMP::Row::Deactivate>`\ (*GMP*, *row*)                                          |
	+---------------------------------------------------------------------------------------------------+
	| :any:`Generate <GMP::Row::Generate>`\ (*GMP*, *row*)                                              |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetLeftHandSide <GMP::Row::GetLeftHandSide>`\ (*GMP*, *row*)                                |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetLeftHandSide <GMP::Row::SetLeftHandSide>`\ (*GMP*, *row*, *value*)                       |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetRightHandSide <GMP::Row::GetRightHandSide>`\ (*GMP*, *row*)                              |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetRightHandSide <GMP::Row::SetRightHandSide>`\ (*GMP*, *row*, *value*)                     |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetType <GMP::Row::GetType>`\ (*GMP*, *row*) :math:`\to` :any:`AllRowTypes`                 |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetType <GMP::Row::SetType>`\ (*GMP*, *row*, *type*)                                        |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetStatus <GMP::Row::GetStatus>`\ (*GMP*, *row*) :math:`\to` :any:`AllRowColumnStatuses`    |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetIndicatorColumn <GMP::Row::GetIndicatorColumn>`\ (*GMP*, *row*)                          |
	+---------------------------------------------------------------------------------------------------+
	| :any:`DeleteIndicatorCondition <GMP::Row::DeleteIndicatorCondition>`\ (*GMP*, *row*)              |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetIndicatorCondition <GMP::Row::GetIndicatorCondition>`\ (*GMP*, *row*)                    |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetIndicatorCondition <GMP::Row::SetIndicatorCondition>`\ (*GMP*, *row*, *column*, *value*) |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetConvex <GMP::Row::GetConvex>`\ (*GMP*, *row*)                                            |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetConvex <GMP::Row::SetConvex>`\ (*GMP*, *row*, *value*)                                   |
	+---------------------------------------------------------------------------------------------------+
	| :any:`GetRelaxationOnly <GMP::Row::GetRelaxationOnly>`\ (*GMP*, *row*)                            |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetRelaxationOnly <GMP::Row::SetRelaxationOnly>`\ (*GMP*, *row*, *value*)                   |
	+---------------------------------------------------------------------------------------------------+
	| :any:`SetPoolType <GMP::Row::SetPoolType>`\ (*GMP*, *row*, *value*\ [, *mode*])                   |
	+---------------------------------------------------------------------------------------------------+
	
.. rubric:: Row types

The row type refers to one of the four possibilities:

-  ``'<='``,

-  ``'='``,

-  ``'>='``, and

-  ``'ranged'``

You are free to change this type for each row. Deactivating and
subsequently reactivating a row are instructions to the solver to ignore
the row as part of the underlying mathematical program and then
reconsider the row again as an active row.

.. rubric:: Row generation

When you add a new row to a matrix using :any:`GMP::Row::Add`, the newly
added row will initially only have any zero coefficients, regardless of
whether the corresponding AIMMS constraint had a definition or not.
Through the procedure :any:`GMP::Row::Generate` you can tell AIMMS to
discard the current contents of a row in the matrix, and insert the
coefficients as they follow from the definition of the corresponding
constraint in your model.

.. rubric:: Indicator conditions

When you are using the CPLEX, Gurobi or ODH-CPLEX solver, you can
declaratively specify indicator constraints through the
``IndicatorConstraint`` property of a constraint declaration (see
:ref:`sec:var.constr.indicator`). You can also set and delete indicator
constraints programmatically for a given *GMP* using the functions
:any:`GMP::Row::SetIndicatorCondition` and
:any:`GMP::Row::DeleteIndicatorCondition`

.. rubric:: Lazy and cut pool constraints

When you are using the CPLEX, Gurobi or ODH-CPLEX solver, you can
declaratively specify constraints to be part of a pool of lazy
constraints or cuts through the ``IncludeInLazyConstraintPool`` and
``IncludeInCutPool`` properties of a constraint declaration respectively
(see :ref:`sec:var.constr.indicator`). You can also specify lazy and cut
pool constraints programmatically for a given *GMP* using the function
:any:`GMP::Row::SetPoolType`.

.. rubric:: Convex and relaxation-only constraints

Through the :ref:`.Convex` and :ref:`.RelaxationOnly` suffices of constraints
you can set special constraint properties for the BARON global
optimization solver (see also :ref:`sec:var.constr.glob-suff`). For a
given *GMP* you can also set these constraint properties
programmatically using the :any:`GMP::Row::SetConvex` and
:any:`GMP::Row::SetRelaxationOnly` functions.

.. _sec:gmp.matrix.column:

Column Modification Procedures
------------------------------

The procedures and functions of the ``GMP::Column`` namespace are listed
in :ref:`this table <table:gmp.column>` and take care of the modification of
properties of existing columns and the creation of new columns.

.. _GMP::Column::SetAsMultiObjective-LR:

.. _GMP::Column::GetStatus-LR:

.. _GMP::Column::SetAsObjective-LR:

.. _GMP::Column::SetType-LR:

.. _GMP::Column::GetType-LR:

.. _GMP::Column::SetUpperBound-LR:

.. _GMP::Column::GetUpperBound-LR:

.. _GMP::Column::SetLowerBound-LR:

.. _GMP::Column::GetLowerBound-LR:

.. _GMP::Column::SetDecomposition-LR:

.. _GMP::Column::Unfreeze-LR:

.. _GMP::Column::Freeze-LR:

.. _GMP::Column::Delete-LR:

.. _GMP::Column::Add-LR:

.. _table:gmp.column:

.. table:: : ``GMP::Column`` routines

	+--------------------------------------------------------------------------------------------------------+
	| :any:`Add <GMP::Column::Add>`\ (*GMP*, *column*)                                                       |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`Delete <GMP::Column::Delete>`\ (*GMP*, *column*)                                                 |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`Freeze <GMP::Column::Freeze>`\ (*GMP*, *column*, *value*)                                        |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`Unfreeze <GMP::Column::Unfreeze>`\ (*GMP*, *column*)                                             |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`GetLowerBound <GMP::Column::GetLowerBound>`\ (*GMP*, *column*)                                   |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`SetLowerBound <GMP::Column::SetLowerBound>`\ (*GMP*, *column*, *value*)                          |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`GetUpperBound <GMP::Column::GetUpperBound>`\ (*GMP*, *column*)                                   |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`SetUpperBound <GMP::Column::SetUpperBound>`\ (*GMP*, *column*, *value*)                          |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`GetType <GMP::Column::GetType>`\ (*GMP*, *column*) :math:`\to` :any:`AllColumnTypes`             |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`SetType <GMP::Column::SetType>`\ (*GMP*, *column*, *type*)                                       |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`GetStatus <GMP::Column::GetStatus>`\ (*GMP*, *column*) :math:`\to` :any:`AllRowColumnStatuses`   |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`SetDecomposition <GMP::Column::SetDecomposition>`\ (*GMP*, *column*, *value*)                    |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`SetAsObjective <GMP::Column::SetAsObjective>`\ (*GMP*, *column*)                                 |
	+--------------------------------------------------------------------------------------------------------+
	| :any:`SetAsMultiObjective <GMP::Column::SetAsMultiObjective>`\ (*GMP*, *column*, *priority*, *weight*) |
	+--------------------------------------------------------------------------------------------------------+
	
.. rubric:: Column types

The column type refers to one of the three possibilities:

-  ``'integer'``,

-  ``'continuous'``, and

-  ``'semi-continuous'``.

You are free to specify a different type for each column. For newly
added columns, AIMMS will (initially) use the lower bound, upper bound
and column type as specified in the declaration of the (symbolic)
variable associated with the added column. Freezing a column and
subsequently unfreezing it are instructions to the solver to fix the
corresponding variable to its current value, and then free it again by
letting it vary between its bounds.

.. rubric:: Changing the objective column

If you want to implement the procedures for reaching primal or dual
uniqueness as described in :ref:`sec:gmp.instance.dual`, you can use the
procedure

-  :any:`GMP::Column::SetAsObjective`

to change the objective function used by either the primal or dual
mathematical program instance that you want to solve for a second time.
Notice that the defining constraint for this variable should be

-  part of the original mathematical program formulation for which AIMMS
   has generated a mathematical program instance, or

-  added later on to the primal or dual generated mathematical program
   instance using the :any:`GMP::Row::Add` procedure, where the row
   definition is generated by AIMMS through the :any:`GMP::Row::Generate`
   procedure or constructed explicitly through several calls to the
   :any:`GMP::Coefficient::Set` procedure.

.. _sec:matrix.multiproc:

More Efficient Modification Procedures
--------------------------------------

If you want to change the data of many columns or rows belonging to some variable or constraint then
it is more efficient to use the multi variant of a modification procedure. The available multi
procedures of the ``GMP`` namespace are listed in :ref:`this table <table:gmp.multiproc>`.

.. _GMP::Coefficient::SetMulti-LR:

.. _GMP::Column::AddMulti-LR:

.. _GMP::Column::DeleteMulti-LR:

.. _GMP::Column::FreezeMulti-LR:

.. _GMP::Column::UnfreezeMulti-LR:

.. _GMP::Column::SetLowerBoundMulti-LR:

.. _GMP::Column::SetUpperBoundMulti-LR:

.. _GMP::Column::SetTypeMulti-LR:

.. _GMP::Column::SetDecompositionMulti-LR:

.. _GMP::Row::AddMulti-LR:

.. _GMP::Row::DeleteMulti-LR:

.. _GMP::Row::GenerateMulti-LR:

.. _GMP::Row::ActivateMulti-LR:

.. _GMP::Row::DeactivateMulti-LR:

.. _table:gmp.multiproc:

.. table:: : Multi procedures

	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Coefficient::SetMulti <GMP::Coefficient::SetMulti>`\ (*GMP*, *binding*, *row*, *column*, *value*)          |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::AddMulti <GMP::Column::AddMulti>`\ (*GMP*, *binding*, *column*)                                    |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::DeleteMulti <GMP::Column::DeleteMulti>`\ (*GMP*, *binding*, *column*)                              |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::FreezeMulti <GMP::Column::FreezeMulti>`\ (*GMP*, *binding*, *column*, *value*)                     |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::UnfreezeMulti <GMP::Column::UnfreezeMulti>`\ (*GMP*, *binding*, *column*)                          |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetLowerBoundMulti <GMP::Column::SetLowerBoundMulti>`\ (*GMP*, *binding*, *column*, *value*)       |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetUpperBoundMulti <GMP::Column::SetLowerBoundMulti>`\ (*GMP*, *binding*, *column*, *value*)       |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetTypeMulti <GMP::Column::SetTypeMulti>`\ (*GMP*, *binding*, *column*, *type*)                    |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetDecompositionMulti <GMP::Column::SetDecompositionMulti>`\ (*GMP*, *binding*, *column*, *value*) |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::AddMulti <GMP::Row::AddMulti>`\ (*GMP*, *binding*, *row*)                                             |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::DeleteMulti <GMP::Row::DeleteMulti>`\ (*GMP*, *binding*, *row*)                                       |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::GenerateMulti <GMP::Row::GenerateMulti>`\ (*GMP*, *binding*, *row*)                                   |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::ActivateMulti <GMP::Row::ActivateMulti>`\ (*GMP*, *binding*, *row*)                                   |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::DeactivateMulti <GMP::Row::DeactivateMulti>`\ (*GMP*, *binding*, *row*)                               |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::SetRightHandSideMulti <GMP::Row::SetRightHandSideMulti>`\ (*GMP*, *binding*, *row*, *value*)          |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::SetTypeMulti <GMP::Row::SetTypeMulti>`\ (*GMP*, *binding*, *row*, *type*)                             |
	+------------------------------------------------------------------------------------------------------------------+
	| :any:`Row::SetPoolTypeMulti <GMP::Row::SetPoolTypeMulti>`\ (*GMP*, *binding*, *row*, *value*, *mode*)            |
	+------------------------------------------------------------------------------------------------------------------+

.. rubric:: Binding argument

All procedures in :ref:`this table <table:gmp.multiproc>` contain an index binding argument. The index binding argument
specifies which columns or rows will be modified. If the procedure contains a value argument then the size of this vector is defined by the 
index binding argument. Further information on index binding can be found in :ref:`chap:bind`.

.. rubric:: Alternative procedures

An alternative approach to change or retrieve the data of multiple columns or rows is using the *raw* procedures, of the ``GMP`` namespace,
mentioned in :ref:`this table <table:gmp.rawproc>`.

.. _GMP::Coefficient::GetRaw-LR:

.. _GMP::Coefficient::SetRaw-LR:

.. _GMP::Column::DeleteRaw-LR:

.. _GMP::Column::FreezeRaw-LR:

.. _GMP::Column::UnfreezeRaw-LR:

.. _GMP::Column::GetLowerBoundRaw-LR:

.. _GMP::Column::SetLowerBoundRaw-LR:

.. _GMP::Column::GetUpperBoundRaw-LR:

.. _GMP::Column::SetUpperBoundRaw-LR:

.. _GMP::Column::SetTypeRaw-LR:

.. _GMP::Row::DeleteRaw-LR:

.. _GMP::Row::ActivateRaw-LR:

.. _GMP::Row::DeactivateRaw-LR:

.. _GMP::Row::GetRightHandSideRaw-LR:

.. _GMP::Row::SetRightHandSideRaw-LR:

.. _GMP::Row::SetTypeRaw-LR:

.. _table:gmp.rawproc:

.. table:: : Raw procedures

	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Coefficient::GetRaw <GMP::Coefficient::GetRaw>`\ (*GMP*, *rowSet*, *colSet*, *coef*)                |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Coefficient::SetRaw <GMP::Coefficient::SetRaw>`\ (*GMP*, *rowSet*, *colSet*, *coef*, *changeZero*)  |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::DeleteRaw <GMP::Column::DeleteRaw>`\ (*GMP*, *colSet*)                                      |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::FreezeRaw <GMP::Column::FreezeRaw>`\ (*GMP*, *colSet*, *value*)                             |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::UnfreezeRaw <GMP::Column::UnfreezeRaw>`\ (*GMP*, *colSet*)                                  |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::GetLowerBoundRaw <GMP::Column::GetLowerBoundRaw>`\ (*GMP*, *colSet*, *lbs*)                 |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetLowerBoundRaw <GMP::Column::SetLowerBoundRaw>`\ (*GMP*, *colSet*, *value*)               |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::GetUpperBoundRaw <GMP::Column::GetUpperBoundRaw>`\ (*GMP*, *colSet*, *ubs*)                 |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetUpperBoundRaw <GMP::Column::SetUpperBoundRaw>`\ (*GMP*, *colSet*, *value*)               |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Column::SetTypeRaw <GMP::Column::SetTypeRaw>`\ (*GMP*, *colSet*, *type*)                            |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Row::DeleteRaw <GMP::Row::DeleteRaw>`\ (*GMP*, *rowSet*)                                            |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Row::ActivateRaw <GMP::Row::ActivateRaw>`\ (*GMP*, *rowSet*)                                        |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Row::DeactivateRaw <GMP::Row::DeactivateRaw>`\ (*GMP*, *rowSet*)                                    |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Row::GetRightHandSideRaw <GMP::Row::GetRightHandSideRaw>`\ (*GMP*, *rowSet*, *rhs*)                 |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Row::SetRightHandSideRaw <GMP::Row::SetRightHandSideRaw>`\ (*GMP*, *rowSet*, *value*)               |
	+-----------------------------------------------------------------------------------------------------------+
	| :any:`Row::SetTypeRaw <GMP::Row::SetTypeRaw>`\ (*GMP*, *rowSet*, *type*)                                  |
	+-----------------------------------------------------------------------------------------------------------+

These procedures use a set of column and/or row numbers as input. These
sets of column and row numbers can be obtained by using the functions

-  :any:`GMP::Instance::GetColumnNumbers`, and
-  :any:`GMP::Instance::GetRowNumbers`

respectively.

.. _sec:matrix.extended:

Modifying an Extended Math Program Instance
-------------------------------------------

.. rubric:: Extended math program instances

To use the matrix manipulation routines of the GMP library, you must be
able to associate every row and column of the matrix of the math program
instance you want to manipulate with a symbolic constraint or variable
within your model. However, some routines in the GMP library generate
rows and columns that cannot be directly associated with specific
symbolic constraints and variables in your model. Examples of such
routines are:

-  the :any:`GMP::Instance::CreateDual` procedure, which may generate
   additional variables in the dual formulation for bounded variables
   and ranged constraints in the primal formulation (see also
   :ref:`sec:gmp.instance.dual`),

-  the :any:`GMP::Linearization::Add` and :any:`GMP::Linearization::AddSingle`
   procedures, which add linearizations of nonlinear constraints to a
   specific math program instance (see also :ref:`sec:gmp.lin`),

-  the :any:`GMP::Instance::AddIntegerEliminationRows` procedure, and

-  the :any:`GMP::Instance::AddLimitBinaryDeviationRow` procedure.

The rows and columns generated by these procedures can, however, be
*indirectly* associated with symbolic constraints, variables or
mathematical programs, as will be explained below.

.. rubric:: Extended suffices

To support the use of the matrix manipulation routines in conjunction
with rows and columns generated by AIMMS that can only be indirectly
associated with symbolic identifers in the model, AIMMS provides the
following suffices which allow you to do so:

-  :ref:`.ExtendedVariable`, and

-  :ref:`.ExtendedConstraint`.

These suffices are supported for ``Variables``, ``Constraints`` and
``MathematicalPrograms``. They behave like variables and constraints,
which implies that it is possible to refer to the :ref:`.ReducedCost` and
:ref:`.ShadowPrice` suffices of these extended suffices to get hold of
their sensitivity information.

.. rubric:: Suffix dimensions

Each of the suffices listed above has one additional dimension compared
to the dimension of the original identifier, over the predefined set
:any:`AllGMPExtensions`. For example, assuming that ``ae`` is an index into
the set :any:`AllGMPExtensions`,

-  if ``z(i,j)`` is a variable or constrain, the :ref:`.ExtendedVariable`
   suffix will have indices ``z.ExtendedVariable(ae,i,j)``,

-  if ``mp`` is a mathematical program, the :ref:`.ExtendedConstraint`
   suffix will have indices ``mp.ExtendedConstraint(ae)``.

Each of the procedures listed above, will add elements to the set
:any:`AllGMPExtensions` as necessary. The names of the precise elements
added to the set is explained below in more detail.

.. rubric:: Suffices generated by ``CreateDual``

The procedure :any:`GMP::Instance::CreateDual` will add the following
elements to the set :any:`AllGMPExtensions`:

-  ``DualObjective``, ``DualDefinition``, ``DualUpperBound``,
   ``DualLowerBound``.

In addition, it will generate the following extended variables and
constraints

-  For the mathematical program ``mp`` at hand

   -  the variable ``mp.ExtendedVariable('DualDefinition')``,

   -  the constraint ``mp.ExtendedConstraint('DualObjective')``.

-  For every ranged constraint ``c(i)``

   -  the constraint ``c.ExtendedConstraint('DualLowerBound',i)``,

   -  the constraint ``c.ExtendedConstraint('DualUpperBound' i)``.

-  For every bounded variable ``x(i)`` in :math:`[l_i,u_i]`

   -  | the constraint ``x.ExtendedConstraint('DualLowerBound',i)``
      | (if :math:`l_i\neq 0,-\infty`),

   -  | the constraint ``x.ExtendedConstraint('DualUpperBound' i)``
      | (if :math:`u_i\neq 0, \infty`).

.. rubric:: Modifying the dual math program

Using the matrix manipulation procedures, you can modify the matrix or
objective associated with a dual mathematical program instance created
by calling the procedure :any:`GMP::Instance::CreateDual`. Below you will
find how you can access the rows and columns of a dual mathematical
program instance created by AIMMS.

.. rubric:: Row and column names

For each procedure in the ``GMP::Coefficient``, ``GMP::Row`` and
``GMP::Column`` namespaces you must refer to a scalar constraint and/or
variable reference from your symbolic model. For the dual formulation,
you must

-  use the symbolic primal constraint name, to refer to the dual shadow
   price variable associated with that constraint in the dual
   mathematical program instance, and

-  use the symbolic primal variable name, to refer to the dual
   constraint associated with that variable in the dual mathematical
   program instance.

In other words, when modifying matrix coefficients, rows or columns the
role of the symbolic constraints and variables is interchanged.

.. rubric:: Implicitly added variables and constraints

You can refer to the implicitly added variables and constraints in the
procedures of the ``GMP::Coefficient``, ``GMP::Row`` and ``GMP::Column``
namespaces through the :ref:`.ExtendedVariable` and :ref:`.ExtendedConstraint`
suffices described above. After solving the dual math program, AIMMS
will store the dual solution in the suffices
``.ExtendedVariable.ReducedCost`` and
``.ExtendedConstraint.ShadowPrice``, respectively.

.. rubric:: Extended suffices for linearization

By calling the procedures :any:`GMP::Linearization::Add` or
:any:`GMP::Linearization::AddSingle`, AIMMS will add the linearization for
a single nonlinear constraint instance, or for all nonlinear constraints
from a set of nonlinear constraints to a given math program instance.
When doing so, AIMMS will add an element ``Linearization``\ :math:`k`
(where :math:`k` is a counter) to the set :any:`AllGMPExtensions`, and will
create for each nonlinear constraint ``c(i)``

-  a constraint
   ``c.ExtendedConstraint('Linearization``\ :math:`k`\ ``',i)``, and

-  a variable ``c.ExtendedVariable('Linearization``\ :math:`k`\ ``',i)``
   if deviations from the constraint are permitted (see also
   :ref:`sec:gmp.lin`).

.. rubric:: Elimination constraints and variables

By calling the procedure :any:`GMP::Instance::AddIntegerEliminationRows`,
AIMMS will add one or more constraints and variables to a math program
instance, which will eliminate the current integer solution from the
math program instance. When called, AIMMS will add elements of the form

-  ``Elimination``\ :math:`k`,

-  ``EliminationLowerBound``\ :math:`k`, and

-  ``EliminationUpperBound``\ :math:`k`

to the set :any:`AllGMPExtensions`. In addition, AIMMS will add

-  a constraint
   ``mp.ExtendedConstraint('Elimination``\ :math:`k`\ ``')`` to
   exclude current solution for all binary variables from the math
   program ``mp`` at hand, and

-  for every integer variable ``c(i)`` with a level value between its
   bounds the variables and constraints

   -  ``c.ExtendedVariable('Elimination``\ :math:`k`\ ``',i)``,

   -  ``c.ExtendedVariable('EliminationLowerBound``\ :math:`k`\ ``',i)``,

   -  ``c.ExtendedVariable('EliminationUpperBound``\ :math:`k`\ ``',i)``,

   -  ``c.ExtendedConstraint('Elimination``\ :math:`k`\ ``',i)``,

   -  ``c.ExtendedConstraint('EliminationLowerBound``\ :math:`k`\ ``',i)``,
      and

   -  ``c.ExtendedConstraint('EliminationUpperBound``\ :math:`k`\ ``',i)``.

.. rubric:: Constraints for limiting deviation

By calling the procedure :any:`GMP::Instance::AddLimitBinaryDeviationRow`,
AIMMS will add one constraint to a math program instance, which limits
the number of binary variables of which the solution value is allowed to change.
When called, AIMMS will add an element of the form

-  ``Deviation``\ :math:`k`

to the set :any:`AllGMPExtensions`. In addition, AIMMS will add

-  a constraint
   ``mp.ExtendedConstraint('Deviation``\ :math:`k`\ ``')`` to
   limit the number of binary variables from the math
   program ``mp`` at hand of which the solution value is allowed to change.
