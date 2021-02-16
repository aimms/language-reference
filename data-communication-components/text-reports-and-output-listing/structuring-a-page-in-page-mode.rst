.. _sec:report.page-mode:

Structuring a Page in Page Mode
===============================

.. rubric:: Page-based files

In addition to the continuous stream mode of operation of the ``PUT``
statement discussed in the previous section, AIMMS also provides a
page-based file format. AIMMS divides a page-based file into pages of a
specified length, each consisting of a header, a body, and a footer.
:numref:`fig:report.page-mode` gives an overview of a page in a
page-based report.

.. figure:: structuring-a-page-in-page-mode-pspic1.svg
   :name: fig:report.page-mode

   Overview of a page in a page based report

.. rubric:: Switching to page mode

You can switch between page and stream by setting the :ref:`.PageMode`
suffix of a file identifier to ``'on'`` or ``'off'`` (the elements of
the predefined set :any:`OnOff`), respectively, as in the statement
``ResultFile.PageMode := 'on'``. The value of the :ref:`.PageMode` suffix
is ``'off'`` by default. When switching to another mode AIMMS will begin
with a new page or close the last page.

.. rubric:: Page size and width

The default page size is 60 lines. You can overwrite this default by
setting the :ref:`.PageSize` suffix of the file identifier to another
positive integer value. For instance, ``ResultFile.PageSize := 10`` will
give short pages with only ten lines per page. The default page width is
132 columns. You can change this default by setting the :ref:`.PageWidth`
suffix of the file identifier.

.. rubric:: Headers and footers

The header and footer of a document can be specified by using the
``PUTHD`` and ``PUTFT`` statements. They are equivalent to the ``PUT``
statement but write in the header and footer area instead of in the page
body. The size of the header and footer is not preset, but is determined
by the contents of the ``PUTHD`` and ``PUTFT`` statements. The header
and footer keep their contents from page to page.

.. rubric:: Margins

There are no specific attributes for either the top, bottom, left or
right margins of a page. You essentially control these margins by either
resizing the header or footer of a page, or by positioning the ``PUT``
items in a starting column of your choice using the ``@`` operator of
the ``PUT`` statement.

.. rubric:: Page structure

:ref:`this table <table:report.file-suffix>` summarizes the file attributes for
structuring pages. With the exception of the page body size (read only)
you can modify their defaults by using assignment statements.

.. _footersize:

.. _footercurrentrow:

.. _footercurrentcolumn:

.. _headersize:

.. _headercurrentrow:

.. _headercurrentcolumn:

.. _bodysize:

.. _bodycurrentrow:

.. _bodycurrentcolumn:

.. _pagenumber:

.. _pagewidth:

.. _pagesize:

.. _pagemode:

.. _table:report.file-suffix:

.. table:: Page structure attributes

   =========================== ===================== =========
   Suffix                      Description           Default
   =========================== ===================== =========
   :ref:`.PageMode`            Mode                  ``'off'``
   :ref:`.PageSize`            Page size             60
   :ref:`.PageWidth`           Page width            132
   :ref:`.PageNumber`          Current page number   1
   :ref:`.BodyCurrentColumn`   Body current column   -
   :ref:`.BodyCurrentRow`      Body current row      -
   :ref:`.BodySize`            Body size             -
   :ref:`.HeaderCurrentColumn` Header current column -
   :ref:`.HeaderCurrentRow`    Header current row    -
   :ref:`.HeaderSize`          Header size           -
   :ref:`.FooterCurrentColumn` Footer current column -
   :ref:`.FooterCurrentRow`    Footer current row    -
   :ref:`.FooterSize`          Footer size           -
   =========================== ===================== =========

.. rubric:: Positioning in page mode

The positioning operators ``@``, ``#``, and ``/`` explained in
:ref:`sec:report.put` are also applicable in page mode. However, AIMMS
offers you additional file attributes for positioning items in a
page-based file.

.. rubric:: Current row and column

Whenever you ``PUT`` an item into a header, footer, or page body, there
is a current row and a current column. AIMMS keeps track of which row
and column are current through the suffices :ref:`.BodyCurrentRow` and
:ref:`.BodyCurrentColumn` of the ``File`` identifier. You can either read
or overwrite these values using assignment statements. Similar suffices
also exist for the header and the footer area.

.. rubric:: Modifying size of page sections

After having specified the header, footer, or page body, you may want to
change their size at some stage during the process of writing pages. By
specifying the :ref:`.BodySize`, :ref:`.HeaderSize` and :ref:`.FooterSize`
suffices you can modify the size (or empty) the page body, the header,
or the footer. The value of the :ref:`.BodySize` suffix can be at most the
value of the :ref:`.PageSize` suffix minus the value of the :ref:`.HeaderSize`
and :ref:`.FooterSize` suffices.

.. rubric:: Printing the page number

Whenever you write the contents of the :ref:`.PageNumber` suffix of a
``File`` identifier in its header or the footer area, AIMMS will replace
it with the current page number whenever it prints a page of a page
based report. By default, the first page will be numbered 1, but you can
override this by assigning another value to the :ref:`.PageNumber` suffix.