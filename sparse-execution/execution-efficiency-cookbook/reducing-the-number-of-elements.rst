.. _section:eff.reduc-elements:

Reducing the Number of Elements
===============================

.. rubric:: Application phases

In general, one can divide an application in three phases:

#. reading input data, often referred to as reading and preprocessing,

#. processing data, often referred to as the core model, and

#. writing output results, often referred to as reporting.

Interactive applications add the on/off switching of various application
features, the setting of tuning parameters, the consideration of various
scenarios, the output to screen, and so on. This does not change the
basic concept, however. It only means that the inputs come from various
sources and the outputs go to various destinations. An important
observation is that, usually, most of the computation time is spent in
the core model as this involves:

-  the execution of assignments,

-  the evaluation of definitions,

-  the generation of constraints, and

-  the execution of one or more ``SOLVE`` statements.

.. rubric:: Reducing the core model

Obviously, the fewer data we have in the core model, the sooner we're
finished. Often, a considerable percentage of the data read in during
the data input phase is irrelevant to the final result. We could,
therefore, consider spending more time in the data input phase and try
to remove such irrelevant data with the primary objective of reducing
the amount of data used in the core model. Experience shows that this
effort is usually, but not always, worthwhile.

.. rubric:: Reducing the number of elements

In this section, two complementary methods of reducing the model size
are considered, namely reducing the number of elements in

-  one-dimensional sets, and

-  multidimensional identifiers.

.. _subsection:eff.reduc-elements.active-sets:

Size Reduction of One-Dimensional Sets
--------------------------------------

.. rubric:: Two approaches

If, after the data input phase, a one-dimensional set contains a large
number of elements that are irrelevant to the core model, there are two
possible approaches to removing them from computations in the core
model. These are:

-  adding a condition to all identifiers indexed over that set, or

-  introducing a subset of active elements, and using an index to that
   active subset.

These two approaches are illustrated below.

.. rubric:: Tanks example

As a running example, consider a collection of tanks. Let us introduce a
few identifiers related to tanks:

.. code-block:: aimms

	Set Periods {
	    Index        :  t;
	}
	Set Tanks {
	    Index        :  Tnks;
	}
	Set BrokenTanks {
	    SubsetOf     :  Tanks;
	}
	Parameter StrategicReserve {
	    IndexDomain  :  Tnks;
	}

.. code-block:: aimms

	Parameter SizeOfTank {
	    IndexDomain  :  Tnks;
	}
	Parameter TankIsRelevant {
	    IndexDomain  :  Tnks;
	    Range        :  binary;
	    Definition   :  {
	        1 $ [ ( not Tnks in BrokenTanks                       ) AND
	              ( SizeOfTank( Tnks ) > StrategicReserve( Tnks ) )     ]
	    }
	}
	Variable TankLevel {
	    IndexDomain  :  (t,Tnks) | TanksIsRelevant( Tnks );
	}
	Constraint TankLimit {
	    IndexDomain  :  (t,Tnks) | TanksIsRelevant( Tnks );
	    Definition   :  TankLevel( t,Tnks ) <= SizeOfTank( Tnks );
	}

The example above illustrates the first approach, in which the
restriction on the tanks is embodied by the parameter
``TankIsRelevant``.

.. rubric:: Introducing active subsets

To illustrate the second approach, we change the above model section by
introducing the *active subset* ``ActiveTanks`` and modifying the
declaration of the variable ``TankLevel`` and the constraint
``TankLimit`` as presented below.

.. code-block:: aimms

	Set ActiveTanks {
	    SubsetOf     :  Tanks;
	    Index        :  tnk, tnk2;
	    Definition   :  { Tnks | TankIsRelevant(Tnks) };
	}
	Variable TankLevel {
	    IndexDomain  :  (t,tnk);
	}
	Constraint TankLimit {
	    IndexDomain  :  (t,tnk);
	    Definition   :  TankLevel( t,tnk ) <= SizeOfTank( tnk );
	}

The core model still consists of the variable ``TankLevel`` and the
constraint ``TankLimit`` but their index domain has been changed. These
identifiers are now declared over active tanks only. Because of this
change in the index domain, the parameter ``TankIsRelevant`` is no
longer needed in their index domain condition.

.. rubric:: Speedup by active subsets

One may argue that nothing is gained because the selection through
``TankIsRelevant`` is now replaced by the index ``tnk`` of the active
subset ``ActiveTanks``. However, the AIMMS execution engine has been
tuned to select relevant elements of parameters and variables through
indices in subsets. The selection via a condition such as
``TankIsRelevant(Tnks)`` will force AIMMS to retrieve the values for:

-  the parameter or variable at hand,

-  the parameter ``TanksIsRelevant``, and then

-  combine these values using the 'such that' operator ``|``.

Both approaches produce identical results and limit the core model
execution to relevant elements only. The first approach using the
``TankIsRelevant`` condition takes more execution time than the second
approach using an index in the active subset ``ActiveTanks`` because
this latter approach selects the relevant elements more directly.

.. rubric:: Multiple active subsets

Intuitively you might expect the improvement to be minor because
probably only a few tanks, if any, are removed from the collection of
all tanks. However, for other indices of the model the gain may be
significant. More significant gains may be observed, for example, when

-  you study a few periods from a large model calendar,

-  you study a few scenarios from a large database of scenarios,

-  you study a rather limited region,

-  there are only a few crudes available from a large collection of
   available crudes, or

-  there are only a few products ordered from a large catalog.

A large dimensional identifier, indexed over multiple active subsets,
will have the effect.

.. rubric:: Starting with a core model

What if your model does not limit the number of elements in
one-dimensional sets at all? Following the active subset approach, as
illustrated above, you will have to modify the core model wherever you
use the root set or an index in the root set. In such a situation, you
can also implement "active subsets" by introducing a superset of the
root set, and letting the original root set take on the role of an
active subset.

.. rubric:: Example

We continue the running example by presenting a core model version of
it.

.. code-block:: aimms

	Set Periods {
	    Index        :  t;
	}
	Set Tanks {
	    Index        :  tnk;
	}

.. code-block:: aimms

	Parameter SizeOfTank {
	    IndexDomain  :  tnk;
	}
	Variable TankLevel {
	    IndexDomain  :  (t,tnk);
	}
	Constraint TankLimit {
	    IndexDomain  :  (t,tnk);
	    Definition   :  TankLevel( t,tnk ) <= SizeOfTank( tnk );
	}

In implementing the active subset approach, we introduce a new superset
``AllTanks`` and redefine the original set ``Tanks`` as an active subset
of the superset ``AllTanks`` as follows.

.. code-block:: aimms

	Set AllTanks {
	    Index        :  Tnks;
	}
	Set BrokenTanks {
	    SubsetOf     :  AllTanks;
	}
	Parameter StrategicReserve {
	    IndexDomain  :  Tnks;
	}
	Parameter TankIsRelevant {
	    IndexDomain  :  Tnks;
	    Range        :  binary;
	    Definition   :  {
	        1 $ [ ( not Tnks in BrokenTanks                       ) AND
	              ( SizeOfTank( Tnks ) > StrategicReserve( Tnks ) )     ]
	    }
	}
	Set Tanks {
	    SubsetOf     :  AllTanks;
	    Index        :  tnk;
	    Definition   :  { Tnks | TankIsRelevant(Tnks) };
	}
	Parameter SizeOfTank {
	    IndexDomain  :  Tnks;
	    Comment      :  Now Wrt AllTanks instead of Tanks;
	}

Note that the variable and constraint declarations in the core model
above have not been altered, but their size has been reduced by the size
reduction in the set ``Tanks``.

.. _subsection:eff.reduc-elements.index-domain:

Size Reduction of Multidimensional Identifiers
----------------------------------------------

.. rubric:: Limiting multidimensional identifiers

Having illustrated limiting the number of elements in one-dimensional
sets, we want to consider limiting the number of elements in
multidimensional parameters, variables, and constraints. The AIMMS
language facilitates this through the ``IndexDomain`` attribute.

.. rubric:: Index domain conditions

Domain conditions can be specified in the ``IndexDomain`` attribute of
multidimensional parameters, variables, and constraints. Whenever such
an identifier is assigned, generated, or referenced in an expression,
AIMMS will automatically add the domain condition so keeping your
assignments and constraints more concise and efficient.

.. rubric:: Continued example

We illustrate this by extending the above example as follows.

.. code-block:: aimms

	Variable Flow {
	    IndexDomain  : (t,tnk,tnk2);
	}
	Constraint TankLevelBalance {
	    IndexDomain  : (t,tnk) | t <> first(Periods);
	    Definition   : {
	        TankLevel(t-1,tnk)              ! Level of previous period
	                   - Sum( tnk2, Flow(t,tnk,tnk2) ) ! Flow out of the tank
	                   + Sum( tnk2, Flow(t,tnk2,tnk) ) ! Flow in to the tank
	                   = TankLevel(t,tnk)              ! Current level
	    }
	    Comment      : {
	           "Level at end of previous period
	            minus outflow
	            plus  inflow is
	            level at end of current period"
	    }
	}

Note that, using this formulation, AIMMS generates matrix columns for
every possible pair of tanks, whereas in practice only a small selection
can have an actual flow. If this selection of possible connections
between tanks is represented by a relation ``TankConnections``, the
constraint ``TankLevelBalance`` could be written more efficiently as:

.. code-block:: aimms

	Set TankConnections {
	    SubsetOf     : (AllTanks, AllTanks);
	}
	Variable Flow {
	    IndexDomain  : (t,tnk,tnk2);
	}
	Constraint TankLevelBalance {
	    IndexDomain  : (t,tnk) | t <> first(Periods);
	    Definition   : {
	        TankLevel(t-1,tnk)
	            - Sum( tnk2 | (tnk,tnk2) in TankConnections, Flow(t,tnk,tnk2) )
	            + Sum( tnk2 | (tnk2,tnk) in TankConnections, Flow(t,tnk2,tnk) )
	            = TankLevel(t,tnk)
	    }
	}

Note the repetition of the condition in the above formulation. This is
because the condition is actually a restriction on the ``Flow``
variable, and should therefor be a part of its declaration. This leads
to a much more concise formulation, as presented below.

.. code-block:: aimms

	Variable Flow {
	    IndexDomain  : (t,tnk,tnk2) | (tnk,tnk2) in TankConnections;
	}
	Constraint TankLevelBalance {
	    IndexDomain  : (t,tnk) | t <> first(Periods);
	    Definition   : {
	        TankLevel(t-1,tnk)
	            - Sum( tnk2, Flow(t,tnk,tnk2) )
	            + Sum( tnk2, Flow(t,tnk2,tnk) )
	            = TankLevel(t,tnk)
	    }
	}

.. rubric:: Using binary parameters

A frequently observed alternative to using relations is the use of
binary parameters. The above example could then be written as follows:

.. code-block:: aimms

	Parameter TankIsConnected {
	    IndexDomain  : (tnk,tnk2);
	    Range        : {0, 1};
	}
	Variable Flow {
	    IndexDomain  : (t,tnk,tnk2) | TankIsConnected(tnk,tnk2);
	}

The outflow term of ``TankLevelBalance`` will then be generated as if it
were written:

.. code-block:: aimms

	Sum( tnk2, Flow(t,tnk,tnk2) $ TankIsConnected(tnk,tnk2) )

The notation using binary parameters is equivalent to that with
relations. Which option you use is only a matter of taste and style.

.. rubric:: Why use index domain conditions?

We would encourage you to employ index domain conditions, as using them
has the following advantages:

#. Index domain conditions speed up the execution because:

   -  They exclude irrelevant elements in assignments to parameters with
      an index domain condition,

   -  Having index domain conditions on variables effectively makes the
      referencing of such variables sparse, as only relevant columns are
      generated, and

   -  Index domain conditions on a constraint avoid the generation of
      irrelevant rows of that constraint.

#. Index domain conditions permits concise formulations. As illustrated
   above, you do not need to include the domain condition of the
   ``Flow`` variables while constructing the ``TankLevelBalance``
   constraint. Moreover, you do not need to worry that you mightforget
   such a condition at a particular place in the model.

#. Whenever you determine a more restrictive condition on an identifier
   ``A``, you only need to change your model at one place, namely in the
   index domain condition of that identifier ``A``. You don't need to go
   through the entire model changing every reference to the identifier
   ``A``.

.. rubric:: Tight conditions

To make index domain conditions as effective as possible, they should
remove all, or almost all, irrelevant combinations. Constructing such
"tight" index domain conditions, can be far from straightforward.
However, the time spent on constructing tight index domain conditions
often pays off with a significant reduction in the total execution time
of your model.