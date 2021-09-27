.. _sec:module.intro:

Introduction
============

.. rubric:: Support for large models

When a model grows larger, the need for a clear and logical storage
structure of all its constituting components also grows. In the absence
of such a logical storage structure, you will find that it becomes
increasingly hard to find your way in the model source because of the
huge amount of information it contains. To support you in structuring
your model, AIMMS offers several development tools and language
constructs just for this purpose.

.. rubric:: The model tree

To support you in structuring your model, AIMMS lets you organize all
identifier declarations and procedures of your model in the form of a
tree, called the *model tree*. You can access the model tree in a
graphical manner, using the **Model Explorer** tool (see also
:doc:`creating-and-managing-a-model/the-model-explorer/index`). Several language constructs of
the AIMMS language, such as collections of identifiers declarations, or
the procedures and functions included in your model, are visible as
separate nodes within the model tree.

.. rubric:: Main model node

All model declarations in an AIMMS model are located underneath the root
node of the model tree, the ``Model`` node. The ``Model`` node is always
present in the **Model Explorer**, even when you start a new AIMMS
project, and cannot be deleted. For the ``Model`` node itself, you can
specify several attributes that have a global impact, such as the
licensing arrangements for your model, or the unit convention (if any)
that is applicable to your application as a whole. The attributes of the
``Model`` node are discussed in full detail in :ref:`sec:module.model`.

.. rubric:: Model sections ...

As you start adding identifier declarations, procedures and functions to
a new model, you will soon notice that storing all these declarations
directly underneath the ``Model`` node will result in a nearly
unmanageable list of declarations. Finding information in such a
(linear) list soon becomes a daunting task. To support you in adding
additional structure to your model tree AIMMS provides ``Section``
nodes, which allow you to add depth to the model tree, much like
directories add depth to a file system.

.. rubric:: ...to structure a model

By adding ``Section`` nodes with meaningful names to the model tree, and
storing all model declarations that you find relevant for these section
underneath them, you can impose any logical structure on your model tree
that you find useful. Because AIMMS allows identifiers to be used prior
to their declaration, you do not even have to worry about the
declaration order when you reorganize the model tree in this manner.

.. rubric:: Separate source file

In addition to providing the structuring capabilities described above,
the contents of a ``Section`` node can also be stored in a separate
source file. You can import the contents of such a source file into a
section of another model, or permanently link the contents of a section
to the contents of the source file. This allows you to reuse part of one
model within similar applications. This method of sharing functionality,
however, has its limitations. Name clashes can occur when an imported
section redeclares an identifier already declared in the main model. If
you run into these limitations, you are advised to use the ``Module``
concept discussed below.

.. rubric:: ``Section`` attributes

The attributes of a ``Section`` node allow you to specify such issues as
whether its contents needs to be stored in a separate source file, and
if the usage of such a source file needs to be licensed. The attributes
of a ``Section`` node are discussed in full detail in
:ref:`sec:module.section`.

.. rubric:: Complex modeling environments

When the development of modeling applications becomes the core business
of an organization, this will almost certainly lead to a multitude of
related modeling projects, collaborating developers, and various
end-user types, all subject to frequent changes over time. Projects
evolve naturally due to feedback from end-users, changing application
environments, and rotating personnel. Changes in the pool of model
developers are inevitable, and may cause major fluctuations in
application knowledge, experience, and modeling skills. End-users of
applications also change jobs, which may result in new requirements and
customization requests from the newcomers.

.. rubric:: Need for modularization

In such a dynamic modeling world, the exchange of information becomes a
crucial element to avoid unnecessary duplication. When projects are
customized for different end-users, there is apt to be quite a bit of
commonality between these projects. If these commonalities are not
exchanged properly, there will be multiple and differing versions of
essentially the same model segments. As a result, extensive and costly
human resources will be needed to maintain these multiple related
models. Modularization can help to overcome these problems.

.. rubric:: Collections of functions and procedures

In :ref:`chap:intern` you were introduced to functions and procedures as
the initial tools to modularize the functionality within an AIMMS
project. As explained above, collections of functions and procedures,
along with the required identifier declarations, can be stored in model
sections. These can be exported to separate ``.ams`` files, and can
subsequently be imported by, or linked into, any other AIMMS project.
Every time an AIMMS project is started containing a section link, it
will automatically pick up the latest version of the file. This means
that when such a collection of functions, procedures and identifier
declarations at a customer's site need to be updated, only their
corresponding files need to be replaced.

.. rubric:: Name clashes

One problem that you are likely to run into with the above approach,
however, is the occurrence of name clashes. Some of the identifier names
of procedures, functions, and identifiers in a model section may also
occur in the model in which the section is to be included. Such name
clashes will effectively prevent AIMMS from importing or linking the
section into your model. A possible solution to this problem would be to
rename the offending identifiers, either in your model or in the section
to be included. However, using either approach, the same problems are
likely to return when you get an updated version of the included model
section.

.. rubric:: Modules ...

A more structural solution to the name clash problem is provided by the
concept of *modules* in AIMMS, which allow you to share common model
source into multiple models, without the risk of running into name
clashes. Modules are inserted into the model tree by means of ``Module``
nodes. These nodes are essentially ``Section`` nodes with a separate
namespace, along with attributes to manipulate the global model
namespace. The attributes of ``Module`` nodes are discussed in full
detail in :ref:`sec:module.module`.

.. rubric:: ...avoid name clashes

Like ``Section`` nodes, ``Module`` nodes can be exported to a separate
source file, which can be imported or linked into another model.
However, because all identifiers declared within the ``Module`` node
only live in its associated namespace, importing a module into another
project will not lead to name clashes anymore.

.. rubric:: Dividing a project into sub-projects...

When a project becomes larger, the operational demands and sheer amount
of work involved in implementing the project, may become too demanding
for a single modeler to keep up with. It is then time to divide the
project into a number of manageable sub-projects, on which individual
developers can work more or less independently.

.. rubric:: ...unsuitable for modules

Modules, as discussed above, are not necessarily the most suitable
instrument to facilitate a division into sub-projects. This is mainly
due to the fact that the module concept does not allow identifiers in
the module to be strictly private to that module. Because of this, other
developers can, in principle, refer to all identifiers in the module,
and, consequently, the chances of a single structural change in any of
the modules breaking the entire application are considerable.

.. rubric:: Library projects

To address the problem of allowing multiple developers to work
independently on manageable sub-projects of a big AIMMS project more
thoroughly, AIMMS supports the concept of *library projects*. Library
projects go far beyond modules-they do not only support independent
model development, but a developer can also create end-user pages and
menus as part of the library project. When a library project is included
in a main project, the associated overall application can then be
composed by combining the model source, pages, and menus created as part
of all its included libraries. Library projects are discussed in :doc:`introduction-to-aimms/collaborative-project-development/library-projects-and-the-library-manager`.

.. rubric:: Library modules

Library modules are the source code modules associated with library
projects. They can only be added to your model through the **Library
Manager** discussed in :doc:`introduction-to-aimms/collaborative-project-development/library-projects-and-the-library-manager`. 
AIMMS will insert library modules into the model tree as a
separate ``LibraryModule`` root node. The attributes of
``LibraryModule`` nodes are discussed in full detail in
:ref:`sec:module.library`.

.. rubric:: Library interface

As with ordinary modules, library modules have an associated namespace,
which helps to avoid name clashes when including a library project into
an AIMMS project. In addition, however, library modules provide a public
*interface* to the rest of the model. Within the library project, all
identifiers declared in the library can be freely used in the source of
the library module, its pages and menus. The main project, and all other
library projects included in the main project, however, can only access
the identifiers that are part of the interface of the library. This
allows a developer of a library to freely change any declaration that is
not part of the library interface, without the risk of breaking the
entire application.