.. _chap:compl:

Mixed Complementarity Problems
==============================

.. _Mixed_Complementarity_Prob:

.. rubric:: This chapter

This chapter discusses the special identifier types and language
constructs that AIMMS offers to allow you to formulate mixed
complementarity problems. Although mixed complementarity problems do not
involve optimization, they are specified through variables which are
linked to constraints in terms of these variables, and thus fall into
the common framework of a ``MathematicalProgram``. AIMMS also supports
nonlinear optimization problems with additional complementarity
constraints (also known as MPCC or MPEC problems)

.. toctree::
   :maxdepth: 1

   complementarity-problems
   complementaryvariable-declaration-and-attributes
   declaration-of-mixed-complementarity-models
   declaration-of-mpcc-models