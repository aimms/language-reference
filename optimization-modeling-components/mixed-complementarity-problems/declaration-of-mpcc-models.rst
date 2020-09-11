.. _sec:compl.mpcc:

Declaration of MPCC Models
==========================

.. _mpcc:

.. rubric:: MPCC models

Through the KNITRO solver, AIMMS also supports **m**\ athematical
**p**\ rograms with **c**\ omplementarity **c**\ onstraints (MPCC
models). MPCC models are also more commonly denoted by other modeling
languages as MPEC models, which form a more general, and much more
difficult, class of optimization problems. A MPCC model is an ordinary
NLP model with additional complementarity constraints that have to be
satisfied.

.. rubric:: Declaring MPCC models

To define a MPCC model, you must declare a ``MathematicalProgram`` (see
also :ref:`sec:mp.mp`) and specify ``mpcc`` as the ``Type`` attribute of
the ``MathematicalProgram``. The variable set of a
``MathematicalProgram`` of a MPCC model can contain ordinary variables
as well as complementarity variables. Contrary to pure mixed
complementary models, a MPCC model has an objective function.

.. rubric:: Solving MPCC models

To solve MPCC models in AIMMS, you need a license for the KNITRO solver.
If you do not have a license for the KNITRO solver, AIMMS will return an
error that it has no suitable solver available for the ``mpcc`` class,
whenever you try to solve a MPCC model. The KNITRO solver can also be
used for solving pure mixed complementarity problems, but is, in
general, far less efficient in that case than dedicated ``mcp`` solvers.