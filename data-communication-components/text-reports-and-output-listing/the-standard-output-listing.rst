.. _sec:report.listing:

The Standard Output Listing
===========================

.. rubric:: The ``.lis`` extension

AIMMS produces a standard output listing file for each run of a
procedure and each solution of a mathematical program. The name of this
listing is the base name of the model file with the extension
``.lis``. The listing is optionally generated during the first
execution in a session and, depending on the option settings, can also
be generated during subsequent execution-after updates to parameters and
variables.

.. rubric:: Contents of a listing file

A standard output listing file can contain one or more of the following
items:

-  a *source listing*-the source code as compiled,

-  a *constraint listing*-a printout of the generated individual
   constraints of a mathematical program,

-  a *solution listing*-the solution values for its variables and
   constraints,

-  a *solver status file*-a progress report on the solution process, and

-  any *undirected text output* produced from ``PUT`` or ``DISPLAY``
   statements.

.. rubric:: Output activated via options

By default, the standard output listing will be empty unless you set
options that activate AIMMS to print one or more of the items in the
list above. By not setting options, you avoid the creation of lengthy
output files every time you run a model. In addition, you speed up the
solution process by avoiding unnecessary overhead.

.. rubric:: Examining the solution process

Whenever you want to inspect the model at the individual constraint
level, or want to examine the performance of the solver in some detail,
then a listing file is your ultimate source of information. The required
options for the production of this file can be set from within the model
text or from within the graphical interface of AIMMS. They are retained
with your project. For more specific information on each of the
available options, please consult the AIMMS help file.

.. rubric:: Example

After setting the option ``constraint_listing`` to 1, AIMMS produces the
following standard listing for the transport model used throughout this
manual. The model uses a small example data set containing just a few
Dutch cities. A detailed explanation of the listing format is given at
the end.

.. rubric:: The constraint listing

.. code-block:: aimms

	This is the first constraint listing of TransportModel.

	----  MeetDemand

	MeetDemand('Amsterdam') .. [ 1 | 1 | after ]

	    + 1 * Transport('Amsterdam' ,'Amsterdam' ) + 1 * Transport('Rotterdam' ,'Amsterdam' )
	    >= 5.88 ; (lhs=5.88)

	MeetDemand('Rotterdam') .. [ 1 | 2 | after ]

	    + 1 * Transport('Amsterdam' ,'Rotterdam' ) + 1 * Transport('Rotterdam' ,'Rotterdam' )
	    >= 12.4 ; (lhs=12.4)

	MeetDemand('Den Haag') .. [ 1 | 3 | after ]

	    + 1 * Transport('Amsterdam' ,'Den Haag'  ) + 1 * Transport('Rotterdam' ,'Den Haag'  )
	    >= 12.8 ; (lhs=12.8)

	----  MeetSupply

	MeetSupply('Amsterdam') .. [ 1 | 4 | after ]

	    + 1 * Transport('Amsterdam' ,'Amsterdam' ) + 1 * Transport('Amsterdam' ,'Rotterdam' )
	    + 1 * Transport('Amsterdam' ,'Den Haag'  )
	    <= 16 ; (lhs=15.1)

	MeetSupply('Rotterdam') .. [ 1 | 5 | after ]

	    + 1 * Transport('Rotterdam' ,'Amsterdam' ) + 1 * Transport('Rotterdam' ,'Rotterdam' )
	    + 1 * Transport('Rotterdam' ,'Den Haag'  )
	    <= 16 ; (lhs=16)

	----  TotalCost_definition

	TotalCost_definition .. [ 1 | 6 | after ]

	    + 1 * TotalCost
	    - 3.34 * Transport('Amsterdam','Amsterdam') - 11.7 * Transport('Amsterdam','Rotterdam')
	    -   13 * Transport('Amsterdam','Den Haag' ) -    9 * Transport('Rotterdam','Amsterdam')
	    -    2 * Transport('Rotterdam','Rotterdam') -    3 * Transport('Rotterdam','Den Haag' )
	    = 0 ; (lhs=0)

.. rubric:: Explanation

The above listing contains all the individual constraints generated by
AIMMS on the basis of the model formulation and the particular data set
loaded at the time of the ``SOLVE`` statement. Each individual
constraint name is followed by three entries within square brackets.

-  The first entry represents the number of times that a ``SOLVE``
   statement has been executed.

-  The second entry is a consecutive number assigned to each individual
   constraint being printed.

-  The third entry indicates when the constraint listing is generated
   (either "before" or "after" a ``SOLVE`` statement has been executed).

Bracketed at the end of each constraint is the value of the left-hand
side. You can compare this with the right-hand side to evaluate the
status of the constraint. By setting the option
``constraint_variable_values`` to 1 you get a more extensive listing
that also includes the values and bounds of the variables that are
included in each constraint.

.. rubric:: Solution listing

The following solution listing results from setting the option
``solution_listing`` to 1. Note that the listing includes values for
each of the suffices attached to variables and constraints. The
``status`` column for variables indicates whether or not the variable is
basic, frozen, at bound, or bound exceeded. Similarly, the status column
for constraints indicates the same basis and bound information as for
variables.

.. rubric:: Example solution listing

.. code-block:: aimms

	This is the first solution report of TransportModel after a solve.

	The 1 scalar variable:
	Name       Lower    level  Upper  ReducedCost  Status
	---------  -----  -------  -----  -----------  ------
	TotalCost   -inf  172.079    inf            0  Basic

	The variable "Transport(i,j)" contains the following 6 columns:
	         i           j  Lower   level  Upper  ReducedCost  Status
	----------  ----------  -----  ------  -----  -----------  ------
	Amsterdam   Amsterdam       0   5.880    inf        0.000  Basic
	Amsterdam   Rotterdam       0   9.200    inf        0.000  Basic
	Amsterdam   'Den Haag'      0   0.000    inf        0.300  At bound
	Rotterdam   Amsterdam       0   0.000    inf       15.360  At bound
	Rotterdam   Rotterdam       0   3.200    inf        0.000  Basic
	Rotterdam   'Den Haag'      0  12.800    inf        0.000  Basic

	The 1 scalar constraint:
	Name                  ShadowPrice  Status
	--------------------  -----------  ------
	TotalCost_definition            0

	The constraint "MeetDemand(j)" contains the following 3 rows:
	         j   Lower   level  Upper  ShadowPrice  Status
	----------  ------  ------  -----  -----------  ------
	Amsterdam    5.880   5.880    inf        3.340  At bound
	Rotterdam   12.400  12.400    inf       11.700  At bound
	'Den Haag'  12.800  12.800    inf       12.700  At bound

	The constraint "MeetSupply(i)" contains the following 2 rows:
	         i  Lower   level  Upper  ShadowPrice  Status
	----------  -----  ------  -----  -----------  ------
	Amsterdam    -inf  15.080     16        0.000  Basic
	Rotterdam    -inf  16.000     16       -9.700  At bound