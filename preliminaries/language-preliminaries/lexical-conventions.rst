.. _sec:prelim.lex:

Lexical Conventions
===================

.. rubric:: Lexical conventions

Before treating the more intricate features of the AIMMS language, we
have to discuss its lexical conventions. That is, we have to define the
basic building blocks of the AIMMS language. Each one is described in a
separate paragraph.

.. rubric:: Characters

The set of characters recognized by AIMMS consists of the set of all
printable characters, together with the tab character. Tab characters
are not expanded by AIMMS. The character immediately following a tab
character is positioned at column 9, 17, 25, 33, etc. All other
unprintable or control characters are illegal. The presence of an
illegal character causes a compiler error.

.. _integer:

.. rubric:: Numbers

Numerical values are entered in a style similar to that in other
computer languages. For data storage AIMMS supports the integer data
type as well as the real data type (floating point numbers). During
execution, however, AIMMS will always use a double precision floating
point representation.

.. rubric:: Scientific notation

Following standard practice, the letter ``e`` denotes the scientific
notation allowing convenient representation of very large or small
numbers. The number following the ``e`` can only be a positive or
negative integer. Two examples of the use of scientific notation are
given by

.. math::

   \begin{align}
   &{\texttt{1.2e5}}=1.2\times 10^5=120,000 \\
   &{\texttt{2.72e-4}}=2.72\times 10^{-4}=0.000272
   \end{align}

.. rubric:: Special numbers

In addition to the ordinary real numbers, AIMMS allows the special
symbols ``INF``, ``-INF``, ``UNDF``, ``NA``, and ``ZERO`` as numbers.
The precise meaning and use of these symbols is described later in
:ref:`sec:expr.num.arith-ext`.

.. rubric:: No blanks within numbers

Blanks cannot be used inside a number since AIMMS treats a blank as a
separator. Thus, valid examples of expressions recognized as numbers by
AIMMS are

.. code-block:: aimms

	0         0.0       .0        0.        +1        1.
	0.5       .5        +0.5      +.5       -0.3      -.3
	2e10      2e+10     2.e10     0.3e-5    .3e-5     -.3e-05
	INF       -INF      NA        ZERO

.. rubric:: Machine precision

The range of values allowed by AIMMS and the number of significant
digits is machine-dependent. AIMMS takes advantage of the accuracy of
your machine. This may cause different results when a single model is
run on two different machines. Expressions that cause arithmetic under-
or overflow evaluate to the symbols ``ZERO`` and ``INF``, respectively.
Functions and operators requiring integer arguments also accept real
numbers that lie within a machine-dependent tolerance of an integer.

.. rubric:: Identifiers

Identifiers are the unique names given to sets, indices, parameters,
variables, etc. Identifiers can be any sequence of the letters
``a``-``z``, the digits ``0``-``9`` and the underscore ``_``. They must
start with either a letter or an underscore. The length of an identifier
is limited to 255 characters. Examples of legal identifiers include:

.. code-block:: aimms

	a       b78     _c_
	A_very_long_but_legal_identifier_containing_underscores

The following are not identifiers:

.. code-block:: aimms

	39      39id    A-ident      a&b

.. rubric:: Namespaces

In principle, AIMMS operates with a global namespace for all declared
identifiers. By introducing modules into your model (see also
:ref:`sec:module.module`), you can introduce multiple namespaces, which
can be convenient when a particular model section contains logic that
can be shared by multiple AIMMS models. Procedures and functions
automatically create a separate namespace, allowing for local
identifiers with the same name as global identifiers in your model. You
can use the *namespace resolution* operator ``::`` to refer to an
identifier in a particular namespace (see also
:ref:`sec:module.module`).

.. rubric:: Redeclaring AIMMS keywords

In general, you are not allowed to redeclare AIMMS keywords as
identifiers, unless a keyword refers to a non-essential feature of the
language. Whenever you try to redeclare an existing AIMMS keyword, AIMMS
will produce a compiler error when a keyword cannot be redeclared, or
will give you a one-time option to redeclare a non-essential keyword as
a model identifier. In the latter case, the non-essential feature will
be permanently unavailable within your project.

.. rubric:: Case sensitivity

The AIMMS language is *not* case sensitive. This means that upper and
lower case letters can be mixed freely in identifier names but are
treated identically by AIMMS. However, AIMMS is *case aware*, in the
sense that it will try to preserve or restore the original case wherever
possible.

.. _suffix:

.. rubric:: Identifiers with suffices

Some AIMMS data types have additional data associated with them. You
have access to this extra data through the identifier name plus a
suffix, where the suffix is separated from the identifier by a dot.
Examples of suffices are:

.. code-block:: aimms

	c.Derivative      Transport.ReducedCost      OutputFile.PageSize

You can use a suffix expression associated with a particular identifier
as if it were an identifier itself.

.. rubric:: Case referencing

In addition, AIMMS also uses the dot notation to refer to the data
associated from another case file. An example is given below.

.. code-block:: aimms

	CaseDifference(i,j) := Transport(i,j) - ReferenceCase.Transport(i,j);

In this example the values of a variable ``Transport(i,j)`` currently in
memory are compared to the values in a particular reference case on
disk, identified by the case identifier ``ReferenceCase``. You will find
more information about case references in :ref:`sec:expr.num.ref`.

.. _constant:

.. rubric:: Value types

Any constant or parameter in AIMMS must assume one of the following
value types:

-  number (either integer or floating point),

-  string,

-  set element, or

-  unit expression.

All value types except unit expressions are discussed below. Unit
expressions are explained in :ref:`sec:units.expr`.

.. _constant-string-expression:

.. rubric:: Strings

Constants of string type in AIMMS are delimited by a double quote
character ``"``. To include the double quote character itself in a
string, it should be escaped by the backslash character ``\`` (see also
:ref:`sec:set-expr.string.format`). Strings can be used as constants in
expressions, as arguments of procedures and functions, and in the
initialization of string-valued parameters. The size of strings is
limited to 64 Kb.

.. _element:

.. _quoted-element:

.. rubric:: Sets and set elements

A set is a group of like elements. Sets can be *simple*
(one-dimensional) or a *relation* (multi-dimensional). The elements of a
simple set are represented either by

-  an integer number,

-  a single-quoted string of a length less than 255 characters, or

-  an unquoted string subject to conditions explained below.

The elements of a relation are represented by tuples of such integers or
strings.

.. rubric:: Integer elements

The elements of an integer set can be used in expressions as if they
were integer numbers. Reversely, you can use integer-valued numerical
expressions to indicate an element of an integer set. Some operations
with integer set elements are ambiguous, and you have to indicate to
AIMMS how you want such operations to be interpreted. This is discussed
in :ref:`sec:set.integer`.

.. rubric:: Quoted string elements

The characters allowed in a quoted string elements are the set printable
characters except for tab and newline.

.. rubric:: Unquoted string elements

For your convenience, the elements of a string set need not be delimited
by a single quote when all of the following conditions are met:

-  the string used as a set element consists only of letters, digits,
   underscores and the sign characters ``+`` and "``-``,"

-  the set element is not a reserved word or token, and

-  the set element is used inside a constant expression such as a
   constant *enumerated set* or *list* expression (see also
   :ref:`sec:set-expr.set.enum` and :ref:`sec:expr.num.list`), or inside
   *table* or a *composite table* used for the initialization of
   parameters and variables (see also :ref:`sec:text.table` and
   :ref:`sec:text.composite`).

String-valued set elements that are referenced explicitly under any
circumstance other than the ones mentioned above, must be quoted
unconditionally. To include a single quote character in a set element,
it should be preceded by the backslash character ``\``.

.. rubric:: Examples of set elements

The following set elements are examples of set elements that can be used
without quotation marks under the conditions mentioned above:

.. code-block:: aimms

	label1          1998            1997-12         1997_12
	january         january-1998    h2so4           04-Mar-47

The following character strings are also valid as set elements, but must
be quoted in all cases.

.. code-block:: aimms

	'An element containing spaces'
	'label with nested quotes: "a*b"'

.. rubric:: String elements do not have a value

Contrary to integer set elements, string elements do *not* have an
associated number value. Thus, the string element ``'1993'`` does not
have the value 1993. If you use string elements to represent numbers,
you can use the :any:`Val` function to obtain the associated value. Thus,
``Val('1993')`` represents the number 1993.

.. rubric:: Delimiters

The following delimiters are used by AIMMS:

-  a space " " separates keywords, identifiers and numbers,

-  a pair of single quotes "'" or double quotes """ delimits set
   elements and strings, respectively,

-  a semicolon ``;`` separates statements,

-  braces ``{`` and ``}`` denote the beginning and end of sets and
   lists,

-  a comma ``,`` separates elements of sets and lists,

-  parentheses ``(`` and ``)`` delimit expressions, tuples of
   indices and set elements, as well as argument lists of functions and
   references, and

-  square brackets ``[`` and ``]`` are used to delimit unit
   expressions as well as numeric and element ranges. They can also be
   used as parentheses in expressions and argument lists of functions
   and references, and for grouping elements in components of an element
   tuple (see also :ref:`sec:set-expr.set.enum`).

In most other expressions parentheses and square brackets can be used
interchangeably as long as they match. This feature is useful for making
deeply nested expressions more readable.

.. rubric:: Limits in AIMMS

The following limits apply within AIMMS.

-  the length of a line is limited to 255 characters,

-  the number of set elements per set is at most :math:`2^{30}`,

-  the number of indices associated with an identifier is at most 32,
   and

-  the number of running indices used in iterative operations such as
   ``SUM`` and ``FOR`` is at most 16.