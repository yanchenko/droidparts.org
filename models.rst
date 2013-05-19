=================
Models & Entities
=================

`Model`\s are base classes for JSON models.

``Entity extends Model`` & adds ``long id`` for SQLite persistence.

Annotaions
----------

* Model: ``@Key``
* Entity: ``@Table``, ``@Column``

Best Practices
--------------
#. Public fields instead of `set()`\ters & `get()`\ters.