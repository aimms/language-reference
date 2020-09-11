.. _sec:set-expr.string:

String Expressions
==================

.. rubric:: String expressions

String expressions are useful for

-  creating descriptive texts associated with particular set elements
   and identifiers, or

-  forming customized messages for display in the graphical user
   interface or in output reports.

This section discusses all available string expressions in AIMMS.

.. _string-expression:

.. rubric:: Syntax

*string-expression:*

.. raw:: html

	<div class="svg-container" style="overflow: auto;">	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg
	   xmlns:dc="http://purl.org/dc/elements/1.1/"
	   xmlns:cc="http://creativecommons.org/ns#"
	   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
	   xmlns:svg="http://www.w3.org/2000/svg"
	   xmlns="http://www.w3.org/2000/svg"
	   viewBox="0 0 264.94935 187.2"
	   height="187.2"
	   width="264.94934"
	   xml:space="preserve"
	   id="svg2"
	   version="1.1"><metadata
	     id="metadata8"><rdf:RDF><cc:Work
	         rdf:about=""><dc:format>image/svg+xml</dc:format><dc:type
	           rdf:resource="http://purl.org/dc/dcmitype/StillImage" /></cc:Work></rdf:RDF></metadata><defs
	     id="defs6" /><g
	     transform="matrix(1.3333333,0,0,-1.3333333,0,1213.6)"
	     id="g10"><g
	       transform="scale(0.1)"
	       id="g12"><path
	         id="path14"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 240,9000 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g16"><text
	           id="text20"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,29,896)"><tspan
	             id="tspan18"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/preliminaries/language-preliminaries/lexical-conventions.html#constant-string-expression">constant-string-expression</a></tspan></text>
	</g><path
	         id="path22"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1747.12,9000 50,-20 v 40" /><path
	         id="path24"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,9000 -20,-50 h 40" /><path
	         id="path26"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 410.043,8400 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g28"><text
	           id="text32"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,46.0043,836)"><tspan
	             id="tspan30"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#operator-expression">operator-expression</a></tspan></text>
	</g><path
	         id="path34"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1577.08,8400 50,-20 v 40" /><path
	         id="path36"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1867.13,9000 -20,-50 h 40" /><path
	         id="path38"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,9000 -20,-50 h 40" /><path
	         id="path40"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 530.102,8700 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g42"><text
	           id="text46"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,58.0102,866)"><tspan
	             id="tspan44"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/numerical-and-logical-expressions/numerical-expressions.html#enumerated-list">enumerated-list</a></tspan></text>
	</g><path
	         id="path48"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1457.02,8700 50,-20 v 40" /><path
	         id="path50"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1867.12,9000 -20,-50 h 40" /><path
	         id="path52"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,9000 -20,-50 h 40" /><path
	         id="path54"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 623.461,8100 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g56"><text
	           id="text60"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,67.3461,806)"><tspan
	             id="tspan58"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/procedural-language-components/procedures-and-functions/calls-to-procedures-and-functions.html#function-call">function-call</a></tspan></text>
	</g><path
	         id="path62"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1363.66,8100 50,-20 v 40" /><path
	         id="path64"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1867.12,9000 -20,-50 h 40" /><path
	         id="path66"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 120,9000 -20,-50 h 40" /><path
	         id="path68"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 420.063,7800 -50,20 v -40" /><g
	         transform="scale(10)"
	         id="g70"><text
	           id="text74"
	           style="font-style:italic;font-variant:normal;font-size:11px;font-family:'Lucida Sans';-inkscape-font-specification:LucidaSans-Italic;writing-mode:lr-tb;fill:#d22d2d;fill-opacity:1;fill-rule:nonzero;stroke:none"
	           transform="matrix(1,0,0,-1,47.0063,776)"><tspan
	             id="tspan72"
	             y="0"
	             x="0"><a href="https://documentation.aimms.com/language-reference/non-procedural-language-components/set-set-element-and-string-expressions/set-element-expressions.html#element-expression">element-expression</a></tspan></text>
	</g><path
	         id="path76"
	         style="fill:#ffffff;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1567.06,7800 50,-20 v 40" /><path
	         id="path78"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1867.12,9000 -20,-50 h 40" /><path
	         id="path80"
	         style="fill:#000000;fill-opacity:1;fill-rule:nonzero;stroke:none"
	         d="m 1987.12,9000 -50,20 v -40" /><path
	         id="path82"
	         style="fill:none;stroke:#000000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:round;stroke-miterlimit:10;stroke-dasharray:none;stroke-opacity:1"
	         d="m 0,9000 h 120 m 0,0 v 0 h 120 v 100 H 1747.09 V 9000 8900 H 240 v 100 m 1507.12,0 h 120 M 120,9000 v -500 c 0,-55.23 44.773,-100 100,-100 h 70.043 120 v 100 H 1577.05 V 8400 8300 H 410.043 v 100 m 1167.037,0 h 120 70.05 c 55.22,0 100,44.77 100,100 v 500 M 120,9000 v -200 c 0,-55.23 44.773,-100 100,-100 h 190.102 120 v 100 H 1457 V 8700 8600 H 530.102 v 100 m 926.918,0 h 120 190.1 c 55.23,0 100,44.77 100,100 v 200 M 120,9000 v -800 c 0,-55.23 44.773,-100 100,-100 h 283.461 120 v 100 H 1363.64 V 8100 8000 H 623.461 v 100 m 740.199,0 h 120 283.46 c 55.23,0 100,44.77 100,100 v 800 M 120,9000 V 7900 c 0,-55.23 44.773,-100 100,-100 h 80.063 120 v 100 H 1567.04 V 7800 7700 H 420.063 v 100 m 1146.997,0 h 120 80.06 c 55.23,0 100,44.77 100,100 v 1100 h 120" /></g></g></svg></div>

The format of list expressions are the same for string-valued and
numerical expressions. They are discussed in :ref:`sec:expr.num.list`.

.. _sec:set-expr.string.operators:

String Operators
----------------

.. rubric:: String operators

There are three binary string operators in AIMMS, string concatenation
(``+`` operator), string subtraction (``-`` operator), and string
repetition (``*`` operator). There are no unary string operators.

.. rubric:: String concatenation

The simplest form of composing strings in AIMMS is by the concatenation
of two existing strings. String concatenation is represented as a simple
addition of strings by means of the ``+`` operator.

.. rubric:: String subtraction

In addition to string concatenation, AIMMS also supports subtraction of
two strings by means of the ``-`` operator. The result of the operation
:math:`s_1 -
s_2` where :math:`s_1` and :math:`s_2` are string expressions will be
the substring of :math:`s_1` obtained by

-  omitting :math:`s_2` on the right of :math:`s_1` when :math:`s_1`
   ends in the string :math:`s_2`, or

-  just :math:`s_1` otherwise.

.. rubric:: String repetition

You can use the multiplication operator ``*`` to obtain the string that
is the result of a given number of repetitions of a string. The
left-hand operand of the repetition operator ``*`` must be a string
expression, while the right-hand operand must be an integer numerical
expression.

.. rubric:: Examples

The following examples illustrate some basic string manipulations in
AIMMS.

.. code-block:: aimms

	"This is "     + "a string"            ! "This is a string"
	"Filename.txt" - ".txt"                ! "Filename"
	"Filename"     - ".txt"                ! "Filename"
	"--"           * 5                     ! "----------"

.. _sec:set-expr.string.format:

Formatting Strings
------------------

.. _formatstring-LR:

.. rubric:: The function :any:`FormatString`

With the :any:`FormatString` function you can compose a string that is
built up from combinations of numbers, strings and set elements. Its
arguments are:

-  a *format string*, which specifies how the string is composed, and

-  one or more *arguments* (number, string or element) which are used to
   form the string as specified.

.. rubric:: The format string

The first argument of the function :any:`FormatString` is a mixture of
ordinary text plus *conversion specifiers* for each of the subsequent
arguments. A conversion specifier is a code to indicate that data of a
specified type is to be inserted as text. Each conversion specifier
starts with the ``%`` character followed by a letter indicating its
type. The conversion specifier for every argument type are given in
:numref:`table:set-expr.string.conv-codes`.

.. _table:set-expr.string.conv-codes:

.. table:: 

	========================= =========================
	**Conversion specifiers** **Argument type**
	========================= =========================
	``%s``                    String expression
	``%e``                    Element expression
	``%f``                    Floating point number
	``%g``                    Exponential format number
	``%i``                    Integer expression
	``%n``                    Numerical expression
	``%u``                    Unit expression
	``%%``                    % sign
	========================= =========================
	
.. rubric:: Floating point vs. exponential format

When using the ``%f`` or ``%g`` conversion specifier you explicitly
choose a floating point or exponential format, respectively. The ``%n``
conversion specifier makes this choice for you. If the absolute value of
the corresponding argument is greater or equal to 1, ``%n`` assures that
you get the shortest representation of ``%f`` or ``%g`` (or even ``%i``
if the argument value is integral). However when a non zero width is
specified, AIMMS assumes that the alignment of the decimal point is
important and thus ``%n`` will stick to the use of the floating point
format as long as that fits within the given width. If the absolute
value of the corresponding argument is less than 1, ``%n`` uses the
floating point format as long as the result shows at least 1 significant
digit.

.. rubric:: Example

In the example below, the current value of the parameter ``SmallVal``
and ``LargeVal`` are 10 and 20, the current value of ``CapitalCity`` is
the element ``'Amsterdam'``, and ``UnitPar`` is a unit-valued parameter
with value ``kton/hr``. The following calls to :any:`FormatString`
illustrate its use.

.. code-block:: aimms

	FormatString("The numbers %i and %i", 10, 20)                ! "The numbers 10 and 20"
	FormatString("The numbers %i and %i", SmallVal, LargeVal)    ! "The numbers 10 and 20"
	FormatString("The string %s", "is printed")                  ! "The string is printed"
	FormatString("The element %e", CapitalCity)                  ! "The element Amsterdam"
	FormatString("The unit is %u", UnitPar)                      ! "The unit is kton/hr"
	FormatString("The number %n", 4*ArcTan(1))                   ! "The number 3.141"
	FormatString("The large number %n", 1e+6)                    ! "The large number 1.000e+06"
	FormatString("The integer %n", 10)                           ! "The integer 10"
	FormatString("The fraction %n", 0.01)                        ! "The fraction 0.010"
	FormatString("The fraction %n", 0.0001)                      ! "The fraction 1.000e-04"

.. |blank|   unicode:: U+02423 .. OPEN BOX

.. rubric:: Modification flags

By default, AIMMS will use a default representation for arguments of
each type. By modifying the conversion specifier, you further dictate
the manner in which a particular argument of the :any:`FormatString`
function is printed. *This is done by inserting modification flags in
between the %-sign and the conversion character*. The following
modification directives can be added:

-  *flags*:

   ``<``
      for left alignment

   ``<>``
      for centered alignment

   ``>``
      for right alignment

   ``+``
      add a plus sign (nonnegative numbers)

   |blank|
      add a space (instead of the above ``+`` sign)

   ``0``
      fill with zeroes (right-aligned numbers only)

   ``t``
      print number using thousand separators, using local convention for
      both the thousand separator and decimal separator. Controlling
      these separators is via the options ``Number 1000 separator`` and
      ``Number decimal separator``.

-  *field width*: the converted argument will be printed in a field of
   at least this width, or wider if necessary

-  *dot*: separating the field width from the precision

-  *precision*: the number of decimals for numbers, or the maximal
   number of characters for strings or set elements.

.. rubric:: Note the order

It is important to note that the modification flags must be inserted in
the order as described above.

.. rubric:: Field width and precision

Both the field width and precision of a conversion specifier can be
either an integer constant, or a wildcard, ``*``. In the latter case the
:any:`FormatString` expects one additional integer argument for each
wildcard just before the argument of the associated conversion
specifier. This allows you to compute and specify either the field width
or precision in a dynamic manner. If you do not specify a precision as
modification directive, the default precision is taken from the option
``Listing_number_precision``. Similarly, the default width is taken from
the option ``Listing_number_width``.

.. rubric:: Example

The following calls to :any:`FormatString` illustrate the use of
modification flags.

.. code-block:: aimms

	FormatString("The number %>+08i", 10)               ! "The number +0000010"
	FormatString("The number %>t8i", 100000)            ! "The number  100,000"
	FormatString("The number %> 8.2n", 4*ArcTan(1))     ! "The number     3.14"
	FormatString("The number %> *.*n", 8,2,4*ArcTan(1)) ! "The number     3.14"
	FormatString("The element %<5e", CapitalCity)       ! "The element Amsterdam"
	FormatString("The element %<>5.3e", CapitalCity)    ! "The element  Ams "
	FormatString("The large number %10.1n", 1e+6)       ! "The large number  1000000.0"

.. rubric:: Special characters
   :name: special-char

AIMMS offers a number of special characters to allow you to use the full
range of characters in composing strings. These special characters are
contained in :numref:`table:set-expr.string.spec-kars`.

.. _table:set-expr.string.spec-kars:

.. table:: Special characters

   +-------------------+-----------+---------------------------------------------------+
   | Special character | text code | Meaning                                           |
   +===================+===========+===================================================+
   | ``\f``            | FF        | Form feed                                         |
   +-------------------+-----------+---------------------------------------------------+
   | ``\t``            | HT        | Horizontal tab                                    |
   +-------------------+-----------+---------------------------------------------------+
   | ``\n``            | LF        | Newline character                                 |
   +-------------------+-----------+---------------------------------------------------+
   | ``\"``            | ``"``     | Double quote                                      |
   +-------------------+-----------+---------------------------------------------------+
   | ``\\``            | ``\``     | Backslash                                         |
   +-------------------+-----------+---------------------------------------------------+
   | ``\``\ :math:`n`  | :math:`n` | character :math:`n` (:math:`001\leq n\leq 65535`) |
   +-------------------+-----------+---------------------------------------------------+

.. rubric:: Example

Examples of the use of special characters within :any:`FormatString`
follow.

.. code-block:: aimms

	FormatString("%i \037 \t %i %%", 10, 11)     ! "10 %       11 %"
	FormatString("This is a \"%s\" ", "string")  ! "This is a "string" "

.. _stringtoupper-LR:

.. _stringtolower-LR:

.. _stringcapitalize-LR:

.. rubric:: Case conversion functions

With the functions :any:`StringToUpper`, :any:`StringToLower` and
:any:`StringCapitalize` you can convert the case of a string to upper case,
to lower case, or capitalize it, as illustrated in the following
example.

.. code-block:: aimms

	StringToUpper("Convert to upper case")    ! "CONVERT TO UPPER CASE"
	StringToLower("CONVERT to lower case")    ! "convert to lower case"
	StringCapitalize("capitaLIZED senTENCE")  ! "Capitalized sentence"

.. _sec:set-expr.string.functions:

String Manipulation
-------------------

.. rubric:: Other string related functions

In addition to the :any:`FormatString` function, AIMMS offers a number of
other functions for string manipulation. They are:

-  ``Substring`` to obtain a substring of a particular string,

-  :any:`StringLength` to determine the length of a particular string,

-  :any:`FindString` to obtain the position of the first occurrence of a
   particular substring,

-  :any:`FindNthString` to obtain the position of the :math:`n`-th
   occurrence of a particular substring, and

-  :any:`StringOccurrences` to obtain the number of occurrences of a
   particular substring.

.. _substring-LR:

.. rubric:: The function :any:`SubString`

With the :any:`SubString` function you can obtain a substring from a
particular begin position :math:`m` to an end position :math:`n` (or to
the end of the string if the requested end position exceeds the total
string length). The positions :math:`m` and :math:`n` can both be
negative (but with :math:`m \leq n`), in which case AIMMS will start
counting backwards from the end of the string. Examples are:

.. code-block:: aimms

	SubString("Take a substring of me", 8, 16)    ! returns "substring"
	SubString("Take a substring of me", 18, 100)  ! returns "of me"
	SubString("Take a substring of me", -5, -1)   ! returns "of me"

.. rubric:: The function :any:`StringLength`

The function :any:`StringLength` can be used to determine the length of a
string in AIMMS. The function will return 0 for an empty string, and the
total number of characters for a nonempty string. An example follows.

.. code-block:: aimms

	StringLength("Guess my length")               ! returns 15

.. _findstring-LR:

.. _findnthstring-LR:

.. rubric:: The functions :any:`FindString` and :any:`FindNthString`

With the functions :any:`FindString` and :any:`FindNthString` you can
determine the position of the second argument, the *key*, within the
first argument, the *search* string. The functions return zero if the
key is not contained in the search string. The function :any:`FindString`
returns the position of the first occurrence of the key in the search
string starting from the left, while the function :any:`FindNthString` will
return the position of the :math:`n`-th appearance of the key. If
:math:`n` is negative, the function :any:`FindNthString` will search
backwards starting from the right. Examples are:

.. code-block:: aimms

	FindString      ("Find a string in a string", "string"     )  ! returns 8
	FindNthString   ("Find a string in a string", "string",  2 )  ! returns 20
	FindNthString   ("Find a string in a string", "string", -1 )  ! returns 20

	FindString      ("Find a string in a string", "this string")  ! returns 0
	FindNthString   ("Find a string in a string", "string",  3 )  ! returns 0

.. rubric:: Case sensitivity

By default, the functions :any:`FindString` and :any:`FindNthString` will use
a case sensitive string comparison when searching for the key. You can
modify this behavior through the option
``Case_Sensitive_String_Comparison``.

.. _stringoccurences:

.. rubric:: The function :any:`StringOccurrences`

The function :any:`StringOccurrences` allows you to determine the number of
occurrences of the second argument, the ``key``, within the first
argument, the *search* string. You can use this function, for instance,
to delimit the number of calls to the function :any:`FindNthString` a
priori. An example follows.

.. code-block:: aimms

	StringOccurrences("Find a string in a string", "string"     )  ! returns 2

.. _sec:set-expr.string.convert:

Converting Strings to Set Elements
----------------------------------

.. rubric:: Converting strings to set elements

Converting strings to new elements to or renaming existing elements in a
set is not an uncommon action when end-users of your application are
entering new element interactively or when you are obtaining strings (to
be used as set elements) from other applications through external
procedures. AIMMS offers the following support for dealing with such
situations:

-  the procedure :any:`SetElementAdd` to add a new element to a set,

-  the procedure :any:`SetElementRename` to rename an existing element in a
   set, and

-  the function :any:`StringToElement` to convert strings to set elements.

.. _setelementadd-LR:

.. rubric:: Adding new set elements

The procedure :any:`SetElementAdd` lets you add new elements to a set. Its
arguments are:

-  the *set* to which you want to add the new element,

-  an *element parameter* into *set* which holds the new element after
   addition, and

-  the *stringname* of the new element to be added.

When you apply :any:`SetElementAdd` to a root set, the element will be
added to that root set. When you apply it to a subset, the element will
be added to the subset as well as to all its supersets, up to and
including its associated root set.

.. _setelementrename-LR:

.. rubric:: Renaming set elements

Through the procedure :any:`SetElementRename` you can provide a new name
for an existing element in a particular set whenever this is necessary
in your application. Its arguments are:

-  the *set* which contains the element to be renamed,

-  the *element* to be renamed, and

-  the *stringname* to which the element should be renamed.

After renaming the element, all data defined over the old element name
will be available under the new element name.

.. _stringtoelement-LR:

.. rubric:: The function :any:`StringToElement`

With the function :any:`StringToElement` you can convert string arguments
into (existing) elements of a set. If there is no such element, the
function evaluates to the empty element. Its arguments are:

-  the *set* from which the element corresponding to *stringname* must
   be returned,

-  the *stringname* for which you want to retrieve the corresponding
   element, and

-  the optional *create* argument (values 0 or 1, with a default of 0)
   indicating whether nonexisting elements must be added to the set.

With the *create* argument set to 1, a call to :any:`StringToElement` will
always return an element in *set*. Alternatively to setting the *create*
argument to 1, you can call the procedure :any:`SetElementAdd` to add the
element to the set.

.. rubric:: Example

The following example illustrates the combined use of
:any:`StringToElement` and :any:`SetElementAdd`. It checks for the existence
of the string parameter ``CityString`` in the set ``Cities``, and adds
it if necessary.

.. code-block:: aimms

	ThisCity := StringToElement( Cities, CityString );
	if ( not ThisCity ) then
	   SetElementAdd( Cities, ThisCity, CityString );
	endif;

Alternatively, you can combine both statements by setting the optional
*create* argument of the function :any:`StringToElement` to 1.

.. code-block:: aimms

	ThisCity := StringToElement( Cities, CityString, create: 1 );

.. rubric:: Converting element to string

Reversely, you can use the ``%e`` specifier in the :any:`FormatString`
function to get a pure textual representation of a set element, as
illustrated in the following assignment.

.. code-block:: aimms

	CityString := FormatString("%e", ThisCity );