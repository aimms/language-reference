.. _sec:db.control:

Data Removal
============

.. rubric:: Data removal

The AIMMS database interface offers limited capabilities to manage the
tables in a database. Such management is typically done through the use
of stored procedures within a database. AIMMS, however, offers you the
possibility to remove data from a database table by means of the
``EMPTY`` or ``TRUNCATE`` statement.

.. rubric:: Empty database columns

The ``EMPTY`` statement can remove data from a database table in two
manners.

-  When you use a database table identifier in the identifier selection
   in an ``EMPTY`` statement, AIMMS will remove all data from that
   table.

-  When you use a database table identifier behind the ``IN`` clause in
   an ``EMPTY`` statement, AIMMS will empty all columns in the
   corresponding database table which are mapped onto the AIMMS
   identifiers in the identifier selection of that ``EMPTY`` statement.

For more details on the ``EMPTY`` statement, refer to
:ref:`sec:data.control`.

.. rubric:: Examples

The examples in this paragraph illustrate various uses of the ``EMPTY``
statement applied to database tables.

-  The following statement removes all data from the table
   ``CityTable``.

   .. code-block:: aimms
   
   	empty CityTable ;

-  The following statement removes the data from the table ``CityTable``
   that maps onto the AIMMS identifier ``Demand``.

   .. code-block:: aimms
   
   	empty Demand in CityTable ;

-  The following statement removes the data associated with the version
   ``OldVersion`` from the indexed table ``RouteTable(v)``. The data
   associated with other versions will remain intact.

   .. code-block:: aimms
   
   	empty RouteTable(OldVersion) ;

-  The following statement removes the data from the table
   ``RouteTable(v)`` for all versions ``v`` in the set ``Versions``.

   .. code-block:: aimms
   
   	empty RouteTable;

-  The following statement removes the data from the table
   ``RouteTable(v)`` for all versions ``sv`` in the subset
   ``SelectedVersions`` of the set ``Versions``.

   .. code-block:: aimms
   
   	empty RouteTable(sv);

-  The following statement removes the data in the column mapped onto
   the AIMMS identifier ``Transport`` and associated with the version
   ``LatestVersion`` from the indexed table ``RouteTable(v)``.

   .. code-block:: aimms
   
   	empty Transport in RouteTable(LatestVersion) ;

.. rubric:: Truncate database tables

Depending on the type of the underlying data source you are connecting
to, you can use the ``TRUNCATE`` statement to empty the database table
in a very fast way. The drawbacks of the ``TRUNCATE`` statement are that
not all type of data sources support the  ``TRUNCATE`` statement and
rollback support for the ``TRUNCATE`` operation is also depending on the
type of data source you are connecting to. In case the underlying data
source does not support truncating, depending on the setting of the
option ``Warning_truncate_table`` a warning is issued and AIMMS will use
the slower ``EMPTY`` statement to empty the table.

.. rubric:: Example

The following statement removes all data from the table ``CityTable`` at
once.

.. code-block:: aimms

	truncate table CityTable ;