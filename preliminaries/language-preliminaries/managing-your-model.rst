.. _sec:prelim.model:

Managing Your Model
===================

.. rubric:: Models in AIMMS

AIMMS is a language for the specification and implementation of
multidimensional modeling applications. An AIMMS *model* consists of

-  a *declarative part* which specifies all sets and multidimensional
   identifiers defined over these sets, together with the fixed
   functional relationships defined over these identifiers,

-  an *algorithmic part* consisting of one or more procedures which
   describes the sequence of statements that transform the input data of
   a model into the output data, and

-  a *utility part* consisting of additional identifier declarations and
   procedures to support a graphical end-user interface for your
   application.

.. rubric:: Optimization included ...

The declarative part of a model in AIMMS may include the specification
of optimization problems containing simultaneous systems of equations.
In the algorithmic part you can call a special ``SOLVE`` statement to
translate such optimization problems to a format suitable for a linear
or nonlinear solver.

.. rubric:: ...but not necessary

Although optimization modeling will be an important part of most AIMMS
applications, AIMMS is also a convenient tool for other types of
applications.

-  The purely symbolic representation of set and parameter definitions
   with their automatic dependency structure provides spreadsheet-like
   functionality but with the benefit of much greater maintainability.

-  Because of its simple data structures and power of expression, AIMMS
   lends itself for use as a rapid prototyping language.

.. rubric:: Interfacing with the GUI

Although it is possible to create a simple end-user interface showing
your model's data in the form of tables and graphs, a much more advanced
user interface is possible by exploiting the capabilities of the AIMMS
interface builder. Mostly, this involves the introduction of various
additional sets and parameters in your model, as well as the
implementation of additional procedures to perform special
interface-related tasks.

.. rubric:: The model tree

Modeling in AIMMS is centered around a graphical tool called the *model
explorer*. In the model explorer the contents and structure of your
model is presented in a tree-like fashion, which is also referred to as
the *model tree*. The model tree can contain various types of nodes,
each with their own use. They are:

-  *structuring* sections, which you can use to partition the
   declarations and procedures that are part of your model into logical
   groups,

-  *declaration* sections which contain the *declarations* of the global
   identifiers (like sets, parameters and variables) in your model, and

-  *procedures* and *functions* which contain the statements that
   describe the algorithmic part of your application.

.. rubric:: Creating new models

When you start a new model AIMMS will automatically create a skeleton
model tree which is suitable for small applications. The skeleton
contains the following nodes:

-  a single *declaration section* where you can store the declarations
   used in your model,

-  the predefined procedure ``MainInitialization`` which is called
   directly after compiling your model and can be used to initialize
   your model,

-  the predefined procedure ``MainExecution`` where you can put all the
   statements necessary to execute the algorithmic part of your
   application, and

-  the predefined procedure ``MainTermination`` which is called just
   prior to leaving AIMMS.

.. rubric:: Changing the skeleton

Whenever the number of declarations in your model grows too large to be
easily managed within a single declaration section, or when you want to
divide the execution associated with your application into several
procedures, you are free to change the skeleton model tree created by
AIMMS. You can group particular declarations into separate declaration
sections with a meaningful name, and introduce new procedures and
functions.

.. rubric:: Structuring your model

When you feel that particular groups of declarations, procedures and
functions belong together in a logical manner, you are encouraged to
create a new structuring section with a descriptive name within the
model tree, and store the associated model components underneath it.
When your application grows in size, a clear hierarchical structure of
all the information stored will help tremendously to find your way
within your application easily and quickly.

.. rubric:: Storage on disk

The contents of a model is stored in one or more text files with the
``.ams`` (**A**\ IMMS **m**\ odel **s**\ ource) extension. By default the entire
model is stored in a single file, but for each structural section you
can indicate that you want to store the subtree underneath it in a
separate source file. This is especially useful when particular parts of
your application are shared with other AIMMS applications, or when there
are multiple developers, each responsible for a particular part of the
model.

.. rubric:: Character encoding used in text files
   :name: text.file.encoding

.. _Character.Encoding.Text.File:

A text is a sequence of characters. A text file contains such a text
whereby the characters are encoded into numbers. The mapping between
these characters in a text and these numbers in a file is called an
encoding. The historically prevailing encoding is ASCII which defines
the encoding for some control characters, the English alphabet, digits,
and frequently used punctuation characters for the values 1 .. 127.
However, as characters are stored in bytes, the values 128 .. 255 are
free and these are used at different locales for different purposes.
These locale specific extensions of ASCII are also called code pages. As
a consequence, the characters displayed of an ASCII file containing some
of the numbers 128 .. 255, depend on the active code page selected. The
problem here is that the contents of ASCII files were ambiguous when the
code page to be used was not known (see also
https://en.wikipedia.org/wiki/Code_page). In
order to circumvent this problem, the Unicode consortium enumerated all
characters into more than 64 thousand so-called code points. The first
127 Unicode code points match the first 127 characters of ASCII. These
Unicode code points can be encoded, again, in various ways in a file. To
emphasize that a particular number is a Unicode point, such a number is
often denoted as U+xxxx whereby xxxx is a hexadecimal number. An example
Unicode encoding is ``UTF8``, which stores the first 127 code points in
a single byte. This makes a ``UTF8`` file closely resemble ASCII when no
values above 127 are used. To identify the Unicode encoding used in a
file, a so-called Byte Order Mark (BOM) can be used in the first few
bytes of that file. See also http://www.unicode.org and
https://en.wikipedia.org/wiki/Byte_order_mark.

.. rubric:: UTF8 encoding preferred

UTF8 is a popular encoding; it resembles ASCII for the first 127 code
points and can be used by applications deployed at different locales to
unambiguously exchange data. Most modern text editors, including the one
in AIMMS, are able to handle UTF8 text files. We recommend UTF8 encoding
for AIMMS files, especially when AIMMS is used inside international
organizations. AIMMS system files, including the ``.ams`` model file and
the ``.aimms`` project file, use the UTF8 encoding.

.. rubric:: Version control

After each editing session AIMMS will only save the last version of your
model files, and will not retain a backup of the previous version of
your model files. You are therefore strongly encouraged to use a version
control system to keep a history of the changes you made to your model.

.. rubric:: Other model files

In addition to the model files AIMMS stores a number of other files with
each model. They are:

-  a *project file* containing the pages of the graphical (end-)user
   interface that you have created for your application and all other
   relevant information such as project options, user menus, fonts,
   etc., and

-  a *data tree file* containing all the stored datasets and cases
   associated with your application.