.. _chap:data:

Data Initialization, Verification and Control
=============================================

.. rubric:: Aspects of the use of data

Data initialization, verification and control are important aspects of
modeling applications. In general, verification of initialized data is
required to check for input and consistency errors. When handling
multiple data input sets, data control helps you to clean and maintain
your internal data.

.. rubric:: This chapter

This chapter describes how AIMMS implements data initialization, as well
as the ``Assert`` mechanisms that you can use to verify the validity of
the data of your model. In addition, this chapter describes the data
control statements that you can use to maintain the data of your model
in good order. All explicit forms of data communication with text files,
cases and external databases are discussed in subsequent chapters.

.. toctree::
   :maxdepth: 1

   model-initialization-and-termination
   assertions
   data-control
   working-with-the-set-allidentifiers