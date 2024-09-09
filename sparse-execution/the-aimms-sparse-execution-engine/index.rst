.. _chap:sparse:

The AIMMS Sparse Execution Engine
=================================

.. rubric:: Learning about sparse execution

In this chapter, we look under the hood of the AIMMS sparse execution
engine. It is not only interesting to know what AIMMS can do, but also,
to some extent, how it is done. An understanding of the inner workings
of the AIMMS execution engine may also give you a framework for
understanding why some formulations of AIMMS statements are more
efficient than others, leading to more efficient applications.
Increasing the efficiency of your application will help make it a
success.

.. rubric:: Sparse matrix technology

The AIMMS execution system borrows and extends two simple but powerful
concepts from sparse matrix technology. These concepts are:

-  only store the non-zero values, and

-  do not compute ``0+0`` and ``0*``\ :math:`x` (:math:`x` any number),
   because these computations always result in 0.0 and these results are
   consequently not stored.

.. rubric:: AIMMS extensions

The AIMMS extensions to these borrowed concepts are that:

-  only non-default values are stored, where the default is a selectable
   value, and

-  many operations such as ``OR`` and ``AND`` have similar behaviors as
   ``+`` and ``*`` respectively.

Note, however, that other operators, such as the ``/`` and ``=``
operators, will have to consider zeros:

-  the computation ``0.0 / 0.0`` results in ``UNDF``, and

-  the computation ``0.0 = 0.0`` results in ``1.0``

The results of these computations are not equal to 0.0 and need to be
stored; and therefore 'sparse execution' is not applicable to these
operators.

.. toctree::
   :maxdepth: 1

   storage-and-basic-operations-of-the-execution-engine
   modifying-the-sparsity
   overview-of-operator-efficiency
   
See also
^^^^^^^^

This material is presented differently in the `AIMMS Academy <https://elearning.aimms.com/course/execution-efficiency>`_ master course "Execution Efficiency".