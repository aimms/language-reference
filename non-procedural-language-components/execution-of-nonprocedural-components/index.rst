.. _chap:nonproc:

Execution of Nonprocedural Components
=====================================

.. _execution_of_nonprocedural_components:

.. rubric:: This chapter

The collection of all set and parameter definitions form a system of
functional relationships which AIMMS keeps up-to-date automatically.
This chapter discusses the dependency structure of the system, the kind
of expressions and statements allowed inside the definitions, and the
way in which the relationships are re-computed.

.. rubric:: Spreadsheets

The nonprocedural execution mechanism discussed in this chapter
resembles the execution of spreadsheets. Definitions can be placed in
any order by the model builder, but the logical order of execution is
determined by the system. As a result, you can easily formulate
spreadsheet-based applications in the AIMMS modeling language by merely
using definitions for sets and parameters. Of course, the modeling
language in AIMMS goes beyond the modeling paradigm of spreadsheets, as
AIMMS also offers procedural execution which is found in programming
languages but not in spreadsheets.

.. toctree::
   :maxdepth: 1

   dependency-structure-of-definitions
   expressions-and-statements-allowed-in-definitions
   nonprocedural-execution