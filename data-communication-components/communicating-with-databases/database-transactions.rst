.. _sec:db.transaction:

Database Transactions
=====================

.. _database_transactions:

.. rubric:: Transactions

By default, AIMMS places a transaction around any *single* ``WRITE``
statement to a database table. In this way, AIMMS makes sure that the
complete ``WRITE`` statement can be rolled back in the event of a
database error during the execution of that ``WRITE`` statement. You can
increase the amount of transactional control over ``READ``, ``WRITE``
statements and SQL queries through the procedures

-  :any:`StartTransaction`\ ([*isolation-level*])

-  :any:`CommitTransaction`

-  :any:`RollbackTransaction`

.. rubric:: The procedure :any:`StartTransaction`

With the procedure :any:`StartTransaction` you can manually initiate a
database transaction. As a consequence, you can commit or roll back the
changes in the database caused by all ``WRITE`` statements and SQL
queries executed within the context of the transaction simultaneously.
You can specify the exact semantics of the transaction through its only
(optional) argument *isolation-level*, which must be an element from the
predefined set :any:`AllIsolationLevels`. You cannot call
:any:`StartTransaction` recursively, i.e. you must call
:any:`CommitTransaction` or ``CallbackTransaction`` prior to the next call
to :any:`StartTransaction`. The procedure returns a value of 1 if the
transaction was started successfully, or 0 otherwise.

.. rubric:: The set :any:`AllIsolationLevels`

Besides the ability to commit roll back *all* the changes made to the
database during the transaction, AIMMS supports the following isolation
levels for transactions:

-  ``ReadUncommitted``: a transaction operating at this level can see
   uncommitted changes made by other transactions,

-  ``ReadCommitted`` (default): a transaction operating at this level
   cannot see changes made by other transactions until those
   transactions are committed,

-  ``RepeatableRead``: a transaction operating at this level is
   guaranteed not to see any changes made by other transactions in
   values it has already read during the transaction, and

-  ``Serializable``: a transaction operating at this level guarantees
   that all concurrent transactions interact only in ways that produce
   the same effect as if each transaction were entirely executed one
   after the other.

Note that not all database servers may support all of these isolation
levels, and may cause the call to :any:`StartTransaction` to fail.

.. rubric:: The procedure :any:`CommitTransaction`

Through the procedure :any:`CommitTransaction` you can commit all the
changes that you have made to the database since the previous call to
:any:`StartTransaction`. The function returns a value of 1 of the changes
are committed successfully, or 0 otherwise.

.. rubric:: The procedure :any:`RollbackTransaction`

With the procedure :any:`RollbackTransaction` you can roll back (i.e. undo)
all the changes that you have made to the database since the previous
call to :any:`StartTransaction`. The function returns a value of 1 of the
changes are rolled back successfully, or 0 otherwise.