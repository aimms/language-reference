.. _sec:module.library:

``LibraryModule`` Declaration and Attributes
============================================

.. _library_module:

.. rubric:: ``LibraryModule`` declaration and attributes

``LibraryModule`` nodes create a separate tree in the model tree along
with a separate namespace for all identifier declarations in that
subtree. The model contents associated with a ``LibraryModule`` is
always stored in a separate source file. Contrary to ``Section`` and
``Module`` nodes, the name of this source file cannot be specified in
the ``LibraryModule`` declaration. Rather, it is specified when you add
the library to your project using the **Library Manager**, as discussed
in Section 3.1 of the `User's Guide <https://documentation.aimms.com/_downloads/AIMMS_user.pdf>`__. The
attributes of ``LibraryModule`` nodes are listed in
:numref:`table:module.attr-library`.

.. _table:module.attr-library:

.. table:: 

	============= ================= =============================================================
	Attribute     Value-type        See also page
	============= ================= =============================================================
	``Prefix``    *identifier*         
	``Interface`` *identifier-list*    
	``Property``  ``NoSave``        :ref:`The Property attribute <attr:module.property>`
	``Comment``   *comment string*  :ref:`The Text and Comment attributes <attr:prelim.comment>`
	============= ================= =============================================================
	
.. rubric:: Library modules and namespaces

Like a normal module, each ``LibraryModule`` is supplied with a separate
namespace. Compared to normal modules, however, the visibility rules for
identifiers in a library modules are different. They are more in line
with the intended use of libraries, i.e. to enable a single developer to
work independently on the model source of a library.

.. _library_module.interface:

.. rubric:: The ``Interface`` attribute

Through the ``Interface`` attribute of a ``LibraryModule`` you can
specify the list of identifiers in the module that you want to be part
of its public interface. Only identifiers in the library interface can
be accessed in model declarations, pages and menu items that are not
part of the library at hand. Library identifiers not in the interface
are strictly private to the library, and can never be used outside of
the library.

.. _library_module.prefix:

.. rubric:: The ``Prefix`` attribute

With the *mandatory* ``Prefix`` attribute of a ``LibraryModule`` node,
you must specify a module-specific prefix to be used in conjunction with
the ``::`` operator. The value of the ``Prefix`` attribute should be a
unique name within the main model.

.. rubric:: No propagation to global namespace

Even though identifiers in the interface of the library are visible
outside of the library, AIMMS *always* requires the use of the library
prefix to reference such identifiers. Library modules do not support the
``Public`` attribute of ordinary modules to propagate identifiers to the
global namespace.

.. rubric:: Library initialization and termination

When creating a new library, AIMMS will automatically add
``LibraryInitialization``, ``PostLibraryInitialization``,
``PreLibraryTermination`` and ``LibraryTermination`` procedures to it.
These procedures will be executed during the initialization and
termination of your model. The distinction between these steps are
explained in more detail in :ref:`sec:data.init`.