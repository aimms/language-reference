.. _sec:api.model.editing:

Model Edit Functions
====================

.. rubric:: AIMMS Model Edit Functions

The AIMMS API supports Model Edit Functions allowing external
applications to inspect, modify, or even construct AIMMS models. In this
section, the model edit functions are introduced using a small example.
Subsequently, after briefly describing the relation to runtime libraries
plus the conventions used, several tables containing model edit
functions, are presented and described. Finally, the limitations of
using model edit functions through the AIMMS API are described briefly.

.. rubric:: Small example

In the following example, an element parameter ``nextCity`` is created
with a simple definition. Model editing is done using **model editor**
handles. These handles provide access to the identifiers in the model,
and should not be confused with the data handles and procedure handles
described elsewhere in this chapter.

The model editor handle ``int dsMEH`` refers to a declaration section,
whereas the model editor handle ``int ncMEH`` refers to the parameter
``nextCity``.

.. code-block:: c

	1  AimmsMeCreateNode("nextCity", AIMMSAPI_ME_IDTYPE_ELEMENT_PARAMETER, dsMEH, 0, &ncMEH);
	2  AimmsMeSetAttribute(ncMEH, AIMMSAPI_ME_ATTR_INDEX_DOMAIN, "i");
	3  AimmsMeSetAttribute(ncMEH, AIMMSAPI_ME_ATTR_RANGE, "Cities");
	4  AimmsMeSetAttribute(ncMEH, AIMMSAPI_ME_ATTR_DEFINITION,
	                "if i == last(Cities) then first(Cities) "
	                "else Element(Cities,ord(i)+1) endif");
	5  AimmsMeCompile(ncMEH);
	6  AimmsMeCloseNode(ncMEH);

A line by line explanation of this example follows below. For the sake
of brevity, error handling, such as suggested in
:ref:`sec:api.error.handling`, is omitted here.

Line 1
   Creates an element parameter named ``nextCity``. The fourth argument
   of ``AimmsMeCreateNode`` is the position within the section. A 0
   indicates that it should be placed at the end of the section.

Lines 2-4
   Set the attributes ``IndexDomain``, ``Range``, and ``Definition`` of
   this parameter. Note that only the text is passed, these calls do not
   use the AIMMS compiler to compile them.

Line 5
   Compiles the element parameter ``nextCity``. Only now is the text of
   the attributes actually checked and compiled.

Line 6
   The function ``AimmsMeCloseHandle`` de-allocates the handle ``ncMEH``
   but the created identifier ``nextCity`` remains in the model.

.. rubric:: Relation to runtime libraries

:ref:`sec:module.runtime` describes the model editing facility available
in the AIMMS language using runtime libraries. The advantage of using
the AIMMS API, instead of runtime libraries, for model editing is that
the entire model can be edited, including the main model, provided that
there is no AIMMS procedure active while executing a model edit function
from within the AIMMS API. The cost is that multiple languages have to
be used.

.. rubric:: Conventions for model edit functions

The model edit functions follow the following conventions:

-  Each function starts with ``AimmsMe``.

-  These functions return either ``AIMMSAPI_SUCCESS`` or
   ``AIMMSAPI_FAILURE``.

-  A model editor handle ``MEH`` has to be closed by either
   ``AimmsMeCloseNode`` or ``AimmsMeDestroyNode``.

-  No distinction is made between identifiers and nodes in the model
   editor tree, they are both called "nodes".

-  String output arguments use the type ``AimmsString`` as is explained
   in :ref:`expl:extern.passing-values`.

.. rubric:: Model roots

:numref:`table:api.model.edit.roots` lists the functions available for
manipulating model editor roots. The number of roots available for model
editing is stored by the function ``AimmsMeRootCount(count)`` in its
output argument ``count``. Note that ``count`` is always at least 1,
since there is always the main model. The root
``Predeclared identifiers`` is not included in this count. As the root
``Predeclared identifiers`` and its sub-nodes cannot be changed, it is
not included in this count. To obtain a handle for an existing root, the
function ``int AimmsMeOpenRoot(pos, MEH)`` can be used. A model editor
handle is then created and stored in ``MEH``. If ``pos`` is ``0``, the
main model root is opened. If ``pos`` is in the range
``{ 1 .. count-1 }`` then a library is opened. If ``pos`` equals
``count`` then the predeclared root ``Predeclared identifiers`` is
opened. The root ``Predeclared identifiers`` and its sub-nodes are read
only. In order to create a new runtime library the function
``AimmsMeCreateRuntimeLibrary(name, prefix, MEH)`` can be used. The
position of the new library is at the end of the existing libraries.

.. _table:api.model.edit.roots:

.. table:: Model edit functions for roots and nodes

   +--------------------------------------------------------------------------------+
   | ``int AimmsMeRootCount(int *count)``                                           |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeOpenRoot(int pos, int *MEH)``                                     |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeCreateRuntimeLibrary(char *name, char *prefix, int *MEH)``        |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeNodeExists(char*name, int nMEH, int *exists)``                    |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeOpenNode(char*name, int nMEH, int *MEH)``                         |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeCreateNode(char *name, int idtype, int pMEH, int pos, int *MEH)`` |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeCloseNode(int MEH)``                                              |
   +--------------------------------------------------------------------------------+
   | ``int AimmsMeDestroyNode(int MEH)``                                            |
   +--------------------------------------------------------------------------------+

.. rubric:: Opening or creating a node

The function ``AimmsMeNodeExists(name, nMEH, exists)`` can be used to
test if an identifier exists. This function returns ``AIMMSAPI_FAILURE``
when nMEH does not indicate a valid namespace, or when name is not a
valid identifier name. If the name is a declared identifier in namespace
``nMEH``, then ``exists`` is set to 1, and if not to 0. The function
``AimmsMeOpenNode(name, nMEH, MEH)`` creates a handle to the node with
name ``name`` in the namespace determined by the model editor handle
``nMEH``. If successful, a model editor handle is created and stored in
the output argument ``MEH``. If ``nMEH`` equals
``AIMMSAPI_NULL_HANDLE_NUMBER``, then the namespace of the main model is
used. A new node with name ``name`` and type ``idtype`` can be created
using the function ``AimmsMeCreateNode(name, idtype, pMEH, pos, MEH)``.
The value of ``idtype`` must be one of the constants defined in
``aimmsapi.h`` starting with ``AIMMSAPI_ME_IDTYPE_``. The parent node of
the new node is determined by the model editor handle ``pMEH``. The
value ``pos`` determines the new position of the node within the parent
node. If ``pos`` is outside the range of existing children {1..n}, the
new identifier is placed at the end, otherwise the existing children at
positions ``pos`` .. ``n`` are shifted to positions ``pos+1`` .. ``n+1``
where ``n`` was the old number of children of ``pMEH``.

.. rubric:: Closing or destroying a node

:numref:`table:api.model.edit.roots` not only lists the functions to
open or create nodes, but also shows the complementary functions to
close or destroy nodes. The function ``AimmsMeCloseNode(MEH)``
de-allocates the handle ``MEH`` but leaves the corresponding node in the
model intact. The function ``AimmsMeDestroyNode(MEH)`` destroys the node
corresponding to ``MEH`` and all nodes below that node in the model, and
subsequently deallocates the handle ``MEH``.

.. rubric:: The name of a node

:numref:`table:api.model.edit.name` lists the functions that return the
name of a node. The function ``AimmsMeName(MEH, name)`` stores the name
of the node to which ``MEH`` refers without any prefixes in the output
argument ``name``. The function
``AimmsMeRelativeName(MEH, rMEH, rName)`` stores the name of ``MEH``
such as it should be used from within the node ``rMEH`` in the output
argument ``rName``. A fully qualified name is stored in ``rName`` when
``MEH`` is the ``AIMMSAPI_ME_NULL_HANDLE_NUMBER`` handle.

.. _table:api.model.edit.name:

.. table:: Model edit functions for name and type

   +-----------------------------------------------------------------------------------------+
   | ``int AimmsMeName(int MEH, AimmsString *name)``                                         |
   +-----------------------------------------------------------------------------------------+
   | ``int AimmsMeRelativeName(int MEH, int rMEH, AimmsString *rName)``                      |
   +-----------------------------------------------------------------------------------------+
   | ``int AimmsMeType(int MEH, int *meType)``                                               |
   +-----------------------------------------------------------------------------------------+
   | ``int AimmsMeTypeName(int typeNo, AimmsString *tName)``                                 |
   +-----------------------------------------------------------------------------------------+
   | ``int AimmsMeAllowedChildTypes(int MEH, int *typeBuf, int typeBufsize, int *maxTypes)`` |
   +-----------------------------------------------------------------------------------------+

.. rubric:: The type of a node

In addition, :numref:`table:api.model.edit.name` lists the functions for
the type of a node. The function ``AimmsMeType(MEH, meType)`` stores the
type of the node ``MEH`` in the output argument ``meType``. The value of
``meType`` refers to one of the constants in ``aimmsapi.h`` starting
with ``AIMMSAPI_ME_IDTYPE_``. The function
``AimmsMeAllowedChildTypes(MEH, typeBuf, typeBufsize, maxTypes)`` stores
the types of children allowed below the node ``MEH`` in the buffer
``typeBuf`` while respecting its size ``typeBufsize``. The maximum
number of child types below ``MEH`` is stored in the output argument
``maxTypes``. The utility function ``AimmsMeTypeName(typeNo, tName)``
stores the name of the type ``typeNo`` in the output argument ``tName``.

.. _table:api.model.edit.attributes:

.. table:: Model edit functions for attributes

   +--------------------------------------------------------------------------------------+
   | ``int AimmsMeGetAttribute(int MEH, int attr, AimmsString *text)``                    |
   +--------------------------------------------------------------------------------------+
   | ``int AimmsMeSetAttribute(int MEH, int attr, const char *txt)``                      |
   +--------------------------------------------------------------------------------------+
   | ``int AimmsMeAttributes(int MEH, int attrsBuf[], int attrBufSize, int *maxNoAttrs)`` |
   +--------------------------------------------------------------------------------------+
   | ``int AimmsMeAttributeName(int attr, AimmsString *name)``                            |
   +--------------------------------------------------------------------------------------+

.. rubric:: The attributes of a node

:numref:`table:api.model.edit.attributes` lists the functions available
for handling the attributes of a node. All attributes correspond to
constants in the ``aimmsapi.h`` file. These constants start with
``AIMMSAPI_ME_ATTR_``. The function
``AimmsMeGetAttribute(MEH,attr,text)`` stores the contents of attribute
``attr`` of node ``MEH`` in the output argument ``text``. The function
``AimmsMeSetAttribute(MEH,attr,txt)`` sets the contents of attribute
``attr`` of node ``MEH`` to ``txt``. This function will fail if
attribute ``attr`` is not applicable to identifier ``MEH``, but the text
itself is not checked for errors. The function
``AimmsMeAttributes(MEH, attrsBuf, attrBufSize, maxNoAttrs)`` provides
the applicable attributes for these two functions. It will store the
constants corresponding to the attributes available to node ``MEH`` in
``attrBuf`` while respecting the size of that buffer ``attrBufSize``.
The maximum number of attributes available to node ``MEH`` is stored in
``maxNoAttrs``. The function ``AimmsMeAttributeName(attr, name)`` stores
the name of ``attr`` in ``name``.

.. _table:api.model.node.manipulations:

.. table:: Model edit functions for node manipulations

   +------------------------------------------------------------------------------------------+
   | ``int AimmsMeNodeRename(int MEH, char *newName)``                                        |
   +------------------------------------------------------------------------------------------+
   | ``int AimmsMeNodeMove(int MEH, int pMEH, int pos)``                                      |
   +------------------------------------------------------------------------------------------+
   | ``int AimmsMeNodeChangeType(int MEH, int newType)``                                      |
   +------------------------------------------------------------------------------------------+
   | ``int AimmsMeNodeAllowedTypes(int MEH, int* typeBuf, int typeBufsize, int *maxNoTypes)`` |
   +------------------------------------------------------------------------------------------+

.. rubric:: Basic node manipulations

The functions that support changing the aspects of a node such as name,
location, and type of a node are also shown in
:numref:`table:api.model.node.manipulations`. The function
``AimmsMeNodeRename(MEH, newName)`` changes the name of a node, and the
namechange is applied to the attribute texts that reference this node.
An entry is appended to the name change file if the node is not a
runtime node. The function ``AimmsMeNodeMove(MEH, pMEH, pos)`` moves the
node ``MEH`` to child position ``pos`` of node ``pMEH``. If this results
in a change of namespace, the corresponding namechange is applied to the
attributes that reference this node. In addition, an entry is appended
to the corresponding name change file if this node is not a runtime
node. Moves from one library to another are not supported, nor is a move
in or out of the main model. The function
``AimmsMeNodeChangeType(MEH, newType)`` changes the type of a node. It
will retain available attributes whenever possible. The function
``AimmsMeNodeAllowedTypes`` can be used to query which types, if any, a
particular node can be changed to. The function
``AimmsMeNodeAllowedTypes(MEH, typeBuf, typeBufsize, maxNoTypes)`` will
store all the types into which node ``MEH`` can be changed in a buffer
``typeBuf`` that respects the size ``typeBufsize``. The maximum number
of types into which ``MEH`` can be changed is stored in ``maxNoTypes``.

.. rubric:: Tree walk of the model

:numref:`table:api.model.edit.tree.walk` lists the functions that permit
walking all nodes in the model editor tree. The function
``AimmsMeParent(MEH, pMEH)`` creates a model editor handle to the parent
of ``MEH``, and stores this handle in the output argument ``pMEH``. The
function ``AimmsMeFirst(MEH, fMEH)`` creates a model editor handle to
the first child of ``MEH``, and stores this handle in the output
argument ``fMEH``. The function ``AimmsMeNext( MEH, nMEH)`` creates a
model editor handle to the node next to ``MEH``, and stores this handle
in the output argument ``nMEH``. If such a parent, first child, or next
node does not exist the ``AIMMSAPI_ME_NULL_HANDLE_NUMBER`` handle is
stored in the output argument although the corresponding function does
not fail.

.. _table:api.model.edit.tree.walk:

.. table:: Reading, writing and tree walking a model editor tree

   +---------------------------------------------------------------+
   | ``int AimmsMeParent(int MEH, int *pMEH)``                     |
   +---------------------------------------------------------------+
   | ``int AimmsMeFirst(int MEH, int *fMEH)``                      |
   +---------------------------------------------------------------+
   | ``int AimmsMeNext(int MEH, int *nMEH)``                       |
   +---------------------------------------------------------------+
   | ``int AimmsMeImportNode(int MEH, char *fn, const char *pwd)`` |
   +---------------------------------------------------------------+
   | ``int AimmsMeExportNode(int MEH, char *fn, const char *pwd)`` |
   +---------------------------------------------------------------+

.. rubric:: Reading and writing (portions of) a model

The functions that allow the reading of an AIMMS section from a file, or
writing a section to a file are also listed in
:numref:`table:api.model.edit.tree.walk`. They use the ``Text .ams``
file format. The function ``AimmsMeImportNode(MEH, fn, pwd)`` reads a
file ``fn`` and stores the resulting model structure at node ``MEH``.
The function ``AimmsMeExportNode(MEH, fn, pwd)`` writes the model
structure at node ``MEH`` to file ``fn``. If ``MEH`` does not refer to
an AIMMS section, module, library, or model, the functions
``AimmsMeImportNode`` and ``AimmsMeExportNode`` will fail.

.. rubric:: Compilation

The model edit functions available for compilation and model status
queries are listed in :numref:`table:api.model.edit.compilation`. The
central function ``AimmsMeCompile (MEH)`` compiles the node ``MEH`` and
all its sub-nodes. The entire application (main model and libraries) is
compiled if the argument ``MEH`` equals
``AIMMSAPI_ME_NULL_HANDLE_NUMBER``. If this compilation step is
successful then the procedures are runnable.

The function ``AimmsMeIsRunnable(MEH, r)`` stores 1 in the output
argument ``r`` if the procedure referenced by ``MEH`` is runnable. The
function ``AimmsMeIsReadOnly(MEH, r)`` stores 1 in the output argument
``r`` if the node resides in a read-only library, such as the
``predeclared identifiers``, or a library that was read from a read only
file.

.. _table:api.model.edit.compilation:

.. table:: Model edit functions for compilation and status queries

   +--------------------------------------------+
   | ``int AimmsMeCompile(int MEH)``            |
   +--------------------------------------------+
   | ``int AimmsMeIsRunnable(int MEH, int *r)`` |
   +--------------------------------------------+
   | ``int AimmsMeIsReadOnly(int MEH, int *r)`` |
   +--------------------------------------------+

.. rubric:: Limitations

The following limitations apply to model edit functions from within the
AIMMS API:

#. The ``SourceFile`` attribute is not supported.

#. The current maximum number of identifiers is thirty thousand.

Further, when an AIMMS procedure is running, the identifiers in the main
application can not be modified as explained in
:ref:`sec:module.runtime`.