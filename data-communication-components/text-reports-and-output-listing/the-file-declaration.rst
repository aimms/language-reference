.. _sec:report.file:

The ``File`` Declaration
========================

.. _file:

.. _file_identifier:

.. _file-identifier:

External file names that you want to use for reporting must be linked to
AIMMS identifiers in your model. In this way, external file names become
data. Whenever you want to send output to a particular external file,
you must refer to its associated identifier. This linking is achieved
using a ``File`` declaration, the attributes of which are given in
:numref:`table:report.attr-file`.

.. _table:report.attr-file:

.. table:: 

	+----------------+--------------------------------------------+--------------------------------------------------------+
	| Attribute      | Value-type                                 | See also page                                          |
	+================+============================================+========================================================+
	| ``Name``       | *string-expression*                        |                                                        |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	| ``Device``     | ``disk``, ``window``, ``void``.            |                                                        |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	| ``Mode``       | ``replace``, ``merge``                     |                                                        |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	| ``Encoding``   | an element in :any:`AllCharacterEncodings` | :ref:`text.file.encoding`                              |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	| ``Text``       | *string*                                   | :ref:`attr:prelim.text`                                |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	| ``Comment``    | *comment string*                           | :ref:`attr:prelim.comment`                             |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	| ``Convention`` | *convention*                               | :ref:`attr:db.convention`, :ref:`sec:units.convention` |
	+----------------+--------------------------------------------+--------------------------------------------------------+
	
.. _file.name:

.. rubric:: The ``Name`` attribute

With the ``Name`` attribute you can specify the actual name of the disk
file or window that you want to refer to. If the file identifier refers
to a disk file, the ``Name`` will be the file name on disk. If it refers
to a window the ``Name`` attribute will serve as the title of the
window. If you do not specify a name, AIMMS will construct a default
name, using the internal identifier name as the root and ``.put`` as
the extension.

.. _file.device:

.. _disk:

.. _window:

.. _void:

.. rubric:: The ``Device`` attribute

The ``Device`` attribute can have three values

-  ``disk`` (default),

-  ``window``, and

-  ``void``.

You can use it to indicate whether the output should be directed to an
external file on disk, a window in the graphical user interface, or
whether no output should be generated at all. This latter ``void``
device is very convenient, for instance, to hide output statements in
your code that are useful during the development of your model but
should not be displayed in an end-user version.

.. _file.mode:

.. rubric:: The ``Mode`` attribute

You can use the ``Mode`` attribute to specify whether the file or window
should be overwritten (``replace`` mode, default), or appended to
(``merge`` mode). The graphical window in the user interface differs
from a file in that it can be closed manually by the user. In this case,
its contents are lost and AIMMS starts writing to a new instance
regardless of the mode.

.. rubric:: Example

The following ``File`` declarations illustrate the declaration of a link
to the external file ``result.dat`` in the ``Output`` subdirectory of
the project directory, and a text window that will appear with the title
``Model results``. The contents of ``ResultFile`` will be overwritten
whenever it is opened, while the window ``ResultWindow`` will be
appended to whenever possible.

.. code-block:: aimms

	File ResultFile {
	    Name       : "Output\\result.dat";
	    Device     : disk;
	    Mode       : replace;
	}
	File ResultWindow {
	    Name       : "Model results";
	    Device     : window;
	    Mode       : merge;
	}
	
.. _attr.file.encoding:

.. _file.encoding:

.. rubric:: The ``Encoding`` attribute

In the ``Encoding`` attribute of a file, a specific character encoding
can be specified for that file, either as a specific element of the set
:any:`AllCharacterEncodings` or as an element parameter with the set
:any:`AllCharacterEncodings` as its range. Encodings are explained in
Paragraph *Text files* on Page :ref:`text.file.encoding`. In the example
below, the attribute ``Encoding`` states that code page ``WINDOWS-1252``
should be used for the file ``WindmillLocations.txt``. This code page is
not uncommon in the Netherlands.

.. code-block:: aimms

	File WindMillLocs {
	    Name       :  "WindmillLocations.txt";
	    Encoding   :  'WINDOWS-1252';
	}

The statement ``Write to file WindMillLocs ;`` will subsequently write
the file ``"WindmillLocations.txt"`` using the character encoding
``WINDOWS-1252``. When the ``Encoding`` attribute is not specified, the
statements ``Read`` ``from`` ``file`` and ``Write`` ``to`` ``file`` will
use the encodings specified by the options
``default_input_character_encoding`` and
``default_output_character_encoding`` respectively. The default of these
options is the preferred encoding ``UTF8``. The ``Encoding`` attribute
is ignored when reading from files which start with a Unicode BOM (Byte
Order Mask).

.. rubric:: The ``Convention`` attribute
   :name: attr:file.convention

.. _file.convention:

With the ``Convention`` attribute you can indicate that AIMMS must
assume that the data in the file is to be stored according to the units
provided in the specified convention. If the unit specified in the
convention differs from the unit in which AIMMS stores its data
internally, the data is scaled just prior to data transfer. For the
declaration of ``Conventions`` you are referred to
:ref:`sec:units.convention`.