.. _sec:text.file:

Text Data Files
===============

.. rubric:: Allowed text formats

Text data files must contain one or a sequence of identifier assignments
with a *constant* right-hand side. All assignments must be terminated by
a semi-colon. The following constant formats can be assigned:

-  assignment of *scalar constants*,

-  assignment of *constant enumerated set expressions*,

-  assignment of *constant enumerated list expressions*,

-  assignment of *constant tabular expressions*, and

-  assignment via *composite tables*.

The first three formats can also be used in ordinary expressions, and
have been discussed in :ref:`chap:set-expr` and :ref:`chap:expr`. The
tabular and composite table formats are mostly placed in external data
files, and will be discussed in this chapter.

.. rubric:: AIMMS generated output

When you use the ``WRITE`` statement to write the contents of some or
all identifiers in your model to a text file, AIMMS will select the
appropriate format and write the resulting output accordingly. If you
want actual control over the way identifiers are printed, you should use
the ``PUT`` or ``DISPLAY`` statements (see also :ref:`sec:report.put`
and :ref:`sec:report.display`).

.. rubric:: Easily generated

The text formats allowed in AIMMS are straightforward, and it is not
difficult to generate these formats either manually or through an
external program. As a result, text files form an ideal input medium
when you quickly need to create a small data set to test your AIMMS
application, or when data is obtained from a program to which a direct
link cannot be made.

.. rubric:: Example

The following initialization statements illustrate an arrangement of
assignments of scalar constants, constant enumerated sets and lists
which can be used in an text data file.

.. code-block:: aimms

	Cities      := DATA { Amsterdam, Rotterdam, Antwerp, Berlin, Paris } ;

	Supply(i)   := DATA { Amsterdam :  50,
	                      Rotterdam : 100,
	                      Antwerp   :  75  } ;
	PricePerMile := 50 ;

	LargestCity := 'Paris' ;

.. rubric:: Dimensions must match

There is an important rule that applies to any data initialization
statement in an text data file: the dimensions of left-hand side
identifier and the right-hand side expressions must be equal. For
instance, the assignment

.. code-block:: aimms

	Supply(i) := 100 ;

cannot be made inside an text data file for data initialization. Of
course, the above statement is a valid assignment when used inside a
procedure in AIMMS.

.. rubric:: Reducing the dimension

Sometimes it is more convenient to initialize multidimensional
parameters and variables using several tables of lesser dimension than
by providing a huge table covering the full index space at once. This is
especially convenient when data in your model is supplied in natural
portions (for instance, all city-dependent data separate for each city).
AIMMS helps you in these situations by allowing you to initialize a
*slice* of a parameter or a variable.

.. rubric:: Sliced initialization

You can specify a slice of a non-scalar identifier by replacing one or
more of its indices by explicit elements. The result of a slice can be
either a scalar quantity which you can initialize by assigning a scalar,
or a non-scalar quantity which you can initialize using either a
enumerated list, a table, or a composite table.

.. rubric:: Example

The following data assignments illustrate valid examples of sliced
initialization.

.. code-block:: aimms

	Supply('Amsterdam')     := 75;

	Distance('Amsterdam',j) := DATA { Rotterdam :  85,
	                                  Antwerp   : 170,
	                                  Berlin    : 660,
	                                  Paris     : 530  } ;