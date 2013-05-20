=================
Models & Entities
=================

*Model*\s are base classes for JSON models.

``Entity extends Model`` & adds ``long id`` for SQLite persistence.

The general rule is to use public fields instead of *set()*\ters & *get()*\ters.

Annotaions
==========

* Model: ``@Key``
* Entity: ``@Table``, ``@Column``