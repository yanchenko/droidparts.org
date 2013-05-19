=========================
Object-Relational Mapping
=========================

DroidParts takes a traditional DAO approach of having `Entities` +
`EntityManagers` (as opposed to `ActiveRecord`).

DBOpenHelper
============

A subclass of ``AbstractDBOpenhelper`` that supersedes ``SQLiteOpenHelper``.
That's where table configuration for Entities is done.

Setup
-----

#. Subclass ``AbstractDBOpenhelper``.
#. Override ``onCreateTables(...)`` & call ``createTables(...)`` from there.
#. Return an instance of it in the ``DependencyProvider``.
#. Study available helpers, like ``addIndexes(...)`` or ``addMissingColumns(...)``.

CRUD Operations
===============

See ``EntityManager``.

Advanced Querying
=================

Check out ``EntityManager``'s ``select()``, ``update()``, ``delete()`` builders.

Many-to-many
============

A junction table is required for m2m:

.. code-block:: java

    @Table(name="track_to_tag")
    public class TrackToTag extends Entity {
        @Column(nullable = false)
        public Track track;
        @Column(nullable = false)
        public Tag tag;
    }