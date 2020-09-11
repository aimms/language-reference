.. _sec:xml.intro:

XML in 10 Points
================

.. rubric:: XML is for structuring data

Structured data includes things like spreadsheets, address books,
configuration parameters, financial transactions, and technical
drawings. XML is a set of rules (you may also think of them as
guidelines or conventions) for designing text formats that let you
structure your data. XML is not a programming language, and you don't
have to be a programmer to use it or learn it. XML makes it easy for a
computer to generate data, read data, and ensure that the data structure
is unambiguous. XML avoids common pitfalls in language design: it is
extensible, platform-independent, and it supports internationalization
and localization. XML is fully Unicode-compliant.

.. rubric:: XML looks a bit like HTML

Like HTML, XML makes use of tags (words bracketed by '\ ``<``\ ' and
'\ ``>``\ ') and attributes (of the form ``name="value"``). While HTML
specifies what each tag and attribute means, and often how the text
between them will look in a browser, XML uses the tags only to delimit
pieces of data, and leaves the interpretation of the data completely to
the application that reads it. In other words, if you see ``<p>`` in
an XML file, do not assume it is a paragraph. Depending on the context,
it may be a price, a parameter, a person, a p...(and who says it has to be
a word with a "p"?).

.. rubric:: XML is text, but isn't meant to be read

Programs that produce spreadsheets, address books, and other structured
data often store that data on disk, using either a binary or text
format. One advantage of a text format is that it allows people, if
necessary, to look at the data without the program that produced it; in
a pinch, you can read a text format with your favorite text editor. Text
formats also allow developers to more easily debug applications. Like
HTML, XML files are text files that people shouldn't have to read, but
may when the need arises. Less like HTML, the rules for XML files are
strict. A forgotten tag, or an attribute without quotes makes an XML
file unusable, while in HTML such practice is tolerated and is often
explicitly allowed. The official XML specification forbids applications
from trying to second-guess the creator of a broken XML file; if the
file is broken, an application has to stop right there and report an
error.

.. rubric:: XML is verbose by design

Since XML is a text format and it uses tags to delimit the data, XML
files are nearly always larger than comparable binary formats. That was
a conscious decision by the designers of XML. The advantages of a text
format are evident (see point 3), and the disadvantages can usually be
compensated at a different level. Disk space is less expensive than it
used to be, and compression programs like zip and gzip can compress
files very well and very fast. In addition, communication protocols such
as modem protocols and HTTP/1.1, the core protocol of the Web, can
compress data on the fly, saving bandwidth as effectively as a binary
format.

.. rubric:: XML is a family of technologies

XML 1.0 is the specification that defines what "tags" and "attributes"
are. Beyond XML 1.0, "the XML family" is a growing set of modules that
offer useful services to accomplish important and frequently demanded
tasks. Xlink describes a standard way to add hyperlinks to an XML file.
XPointer and XFragments are syntaxes in development for pointing to
parts of an XML document. An XPointer is a bit like a URL, but instead
of pointing to documents on the Web, it points to pieces of data inside
an XML file. CSS, the style sheet language, is applicable to XML as it
is to HTML. XSL is the advanced language for expressing style sheets. It
is based on XSLT, a transformation language used for rearranging, adding
and deleting tags and attributes. The DOM is a standard set of function
calls for manipulating XML (and HTML) files from a programming language.
XML Schemas 1 and 2 help developers to precisely define the structures
of their own XML-based formats. There are several more modules and tools
available or under development. Keep an eye on W3C's technical reports
page.

.. rubric:: XML is new, but not that new

Development of XML started in 1996 and has been a W3C Recommendation
since February 1998, which may make you suspect that this is rather
immature technology. In fact, the technology isn't very new. Before XML
there was SGML, developed in the early '80s, an ISO standard since 1986,
and widely used for large documentation projects. The development of
HTML started in 1990. The designers of XML simply took the best parts of
SGML, guided by the experience with HTML, and produced something that is
no less powerful than SGML, and vastly more regular and simple to use.
Some evolutions, however, are hard to distinguish from revolutions...And
it must be said that while SGML is mostly used for technical
documentation and much less for other kinds of data, with XML it is
exactly the opposite.

.. rubric:: XML leads HTML to XHTML

There is an important XML application that is a document format: W3C's
XHTML, the successor to HTML. XHTML has many of the same elements as
HTML. The syntax has been changed slightly to conform to the rules of
XML. A document that is "XML-based" inherits the syntax from XML and
restricts it in certain ways (e.g, XHTML allows ``<p>``, but not
``<r>``); it also adds meaning to that syntax (XHTML says that
``<p>`` stands for "paragraph", and not for "price", "person", or
anything else).

.. rubric:: XML is modular

XML allows you to define a new document format by combining and reusing
other formats. Since two formats developed independently may have
elements or attributes with the same name, care must be taken when
combining those formats (does ``<p>`` mean "paragraph" from this
format or "person" from that one?). To eliminate name confusion when
combining formats, XML provides a namespace mechanism. XSL and RDF are
good examples of XML-based formats that use namespaces. XML Schema is
designed to mirror this support for modularity at the level of defining
XML document structures, by making it easy to combine two schemas to
produce a third which covers a merged document structure.

.. rubric:: XML is the basis for RDF and the Semantic Web

W3C's Resource Description Framework (RDF) is an XML text format that
supports resource description and metadata applications, such as music
playlists, photo collections, and bibliographies. For example, RDF might
let you identify people in a Web photo album using information from a
personal contact list; then your mail client could automatically start a
message to those people stating that their photos are on the Web. Just
as HTML integrated documents, menu systems, and forms applications to
launch the original Web, RDF integrates applications and agents into one
Semantic Web. Just like people need to have agreement on the meanings of
the words they employ in their communication, computers need mechanisms
for agreeing on the meanings of terms in order to communicate
effectively. Formal descriptions of terms in a certain area (shopping or
manufacturing, for example) are called ontologies and are a necessary
part of the Semantic Web. RDF, ontologies, and the representation of
meaning so that computers can help people do work are all topics of the
Semantic Web Activity.

.. rubric:: XML is licensefree, platformindependent and wellsupported

By choosing XML as the basis for a project, you gain access to a large
and growing community of tools (one of which may already do what you
need!) and engineers experienced in the technology. Opting for XML is a
bit like choosing SQL for databases: you still have to build your own
database and your own programs and procedures that manipulate it, and
there are many tools available and many people who can help you. And
since XML is license-free, you can build your own software around it
without paying anybody anything. The large and growing support means
that you are also not tied to a single vendor. XML isn't always the best
solution, but it is always worth considering.