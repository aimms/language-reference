.. _sec:compl.mp:

Declaration of Mixed Complementarity Models
===========================================

.. _mcp:

.. rubric:: Mixed complementarity models

To define a pure mixed complementarity model, you must declare a
``MathematicalProgram`` (see also :ref:`sec:mp.mp`) and specify ``mcp``
as the ``Type`` attribute of the ``MathematicalProgram``. In the
``Variables`` attribute you can specify a subset of the set of all
``ComplementarityVariables`` to be included in the mixed complementarity
model at hand. Based on this specification, AIMMS will automatically
generate all constraints associated with these complementarity
variables, resulting in a square system.

.. rubric:: Additional variables and constraints

In addition, AIMMS allows you to add ordinary variables to the
``Variables`` attribute, and to specify additional constraints in the
``Constraints`` attribute of the ``MathematicalProgram`` that must be
satisfied as well. If the solver used to solve the mixed complementarity
model requires a square system, AIMMS will automatically add auxiliary
constraints or variables to the generated system, and provide the
linkages with the ordinary variables and constraints you have added to
the system.

.. rubric:: No optimization

For a mixed complementarity problem you should not specify the
``Objective`` and ``Direction`` attributes, as a complementarity solver
will only compute a feasible solution that satisfies all the
complementarity conditions specified. If these attributes are not empty,
AIMMS will produce a runtime error when you apply the ``SOLVE``
statement the corresponding ``MathematicalProgram`` (see also
:ref:`sec:mp.solve`).

.. rubric:: Example

A mixed complementarity model containing the declaration of the
complementarity variable ``MembraneHeight`` declared in the previous
section, is defined by the following declaration.

.. code-block:: aimms

	MathematicalProgram Membrane {
	    Variables   : AllVariables;
	    Type        : mcp;
	}

As usual, you can solve the ``Membrane`` through the statement

.. code-block:: aimms

	solve Membrane;

which will generate the mixed complementarity model and invoke a
suitable solver for ``mcp`` problem type.