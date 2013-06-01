=========================
Object-Relational Mapping
=========================

DroidParts takes a traditional DAO approach of having *Entities* + *EntityManagers* (as opposed to *ActiveRecord*).

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

Entities
========

Mapping classes must extend ``Entity`` or it's subclass.
``Entity`` already has a ``public long id;`` field that is mapped to ``_id`` column.
It will be automatically populated once once an entity is saved or read.

@Table Annotation
-----------------

* ``name``

@Column Annotation
------------------

* ``name``
* ``nullable``
* ``unique``
* ``eager`` - when ``read()`` or ``fillEagerForeignKeys()``.

EntityManager
=============

An ``EntityManager`` for interactions.
You'll usually have an EntityManager subclass for each Entity type and add helper methods there.
Like so:

.. code-block:: java
    
   public class PostEntityManager extends EntityManager<Post> {
   
      public PostEntityManager(Context ctx) {
         super(Post.class, ctx);
      }
      
      public Select<Post> selectPostsAfterYear(int year) {
         return select().where("year", Is.GREATER, year);
      }
      
   }

CRUD Operations
---------------

``EntityManager`` contains the following methods:

* ``boolean create(EntityType item)``
* ``EntityType read(long id)``
* ``boolean update(EntityType item)``
* ``boolean delete(long id)``
* ``boolean createOrUpdate(EntityType item)``

There are also create, update, delete methods that accept ``Collection<EntityType>``
to run multiple operations in a transaction.

Advanced Operations
-------------------

``EntityManager`` contains ``select()``, ``update()``, ``delete()`` builders.

.. code-block:: java

    // Select is used to provide data to EntityCursorAdapter
   Select<EntityType> select = select().columns("_id", "name").where("external_id", Is.EQUAL, 10);
   
   // alternatively, call execute() to get the underlying Cursor
   Cursor cursor = select().where("name", Is.LIKE, "%%alex%%").execute();
   
   // use Where object for complex queries
   Where haveCoordinaltes = new Where("latitude", Is.NOT_EQUAL, 0).or("longitude", Is.NOT_EQUAL, 0);
   select().where("country", Is.EQUAL, "us").where(haveCoordinates);
   
*  ``void fillEagerForeignKeys(EntityType item)``
*  ``fillForeignKeys(EntityType item, String... columnNames)``

Many-to-many
------------

A junction table is required for m2m:

.. code-block:: java

    @Table(name="track_to_tag")
    public class TrackToTag extends Entity {
        @Column(nullable = false)
        public Track track;
        @Column(nullable = false)
        public Tag tag;
    }