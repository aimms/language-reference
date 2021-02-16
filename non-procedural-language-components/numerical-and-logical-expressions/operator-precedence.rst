.. _sec:expr.oper-prec:

Operator Precedence
===================

.. rubric:: Combined precedence order

In the previous sections we have introduced unary and binary operators
for several types of expressions, together with their relative
precedence order. :ref:`this table <table:expr.oper-prec>` provides an overview of
all of them. The last column lists the expression types in which the
operator is used, where the letters "N", "L", "E", and "S" stand for
*N*\ umerical, *L*\ ogical, set *E*\ lement and *S*\ et expressions,
respectively.

.. _table:expr.oper-prec:

.. table:: Operator precedence (highest to lowest)

   ========== ============================= =====
   Precedence Name                          Type
   ========== ============================= =====
   14         ``ONLYIF $``                  N
   13         ``^``                         N
   12         ``+ -`` (unary)               N
   11         ``* /``                       N,S
   10         ``+ - ++ -`` (binary)         N,E,S
   9          ``CROSS``                     S
   8          ``IN``                        L
   7          ``< <= > >= = <>``            L
   6          ``NOT``                       L
   5          ``AND``                       L
   4          ``OR``                        L
   3          ``XOR``                       L
   2          ``|``                         S
   1          ``IF THEN ELSEIF ELSE ENDIF`` N
   ========== ============================= =====