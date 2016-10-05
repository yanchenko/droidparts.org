=========================
Object-Relational Mapping
=========================

DroidParts takes a traditional DAO approach of having simple *Entity* classes + *EntityManagers*.

DBOpenHelper
============

``AbstractDBOpenhelper`` extends ``SQLiteOpenHelper`` and replaces it for *DroidParts*.
It contains helpers that create & update tables based on *Entity* classes.
Of course, you still can alter the schema manually.

Setup
-----

#. Subclass ``AbstractDBOpenhelper``.
#. Return an instance of it in the ``DependencyProvider`` (see :doc:`di`).
#. Override ``onCreateTables(...)`` method & call ``createTables(...)`` inside it.
#. See available helpers below.

Helper Methods
--------------

* ``createTables(SQLiteDatabase db, Class<? extends Entity>... entityClasses)``
* ``createIndex(SQLiteDatabase db, String table, boolean unique, String firstColumn, String... otherColumns)``
* ``addMissingColumns(SQLiteDatabase db, Class<? extends Entity>... entityClasses)`` - adds new columns for model, in ``onUpgrade(...)``.
* ``dropTables(SQLiteDatabase db, String... optionalTableNames)``
* ``executeStatements(SQLiteDatabase db, ArrayList<String> statements)`` - in a transaction.

Entities
========

Model classes must extend ``Entity`` or it's subclass.

``Entity`` already has a ``public long id`` field that is mapped to ``_id`` column.
It will be automatically populated once once an entity is saved or read.

@Table Annotation
-----------------

* ``name`` - table name.

@Column Annotation
------------------

* ``name`` - column name.
* ``nullable`` - null is ok? SQL constraint.
* ``unique`` - should be unique? SQL constraint.
* ``eager`` - for foreign keys, whether should be prefilled at read time.

EntityManager
=============

You'll typically have an EntityManager subclass for each Entity type and any custom helper methods there.
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
   
CRUD methods
------------
   
``EntityManager`` comes with a number of data manipulation methods:

* ``boolean create(EntityType item)``, ``int create(Collection<EntityType> items)``
* ``EntityType read(long id)``
* ``boolean update(EntityType item)``, ``int update(Collection<EntityType> items)``
* ``boolean delete(long id)``, ``int delete(Collection<EntityType> items)``
* ``boolean createOrUpdate(EntityType item)``

Select, Update, Delete Builders
-------------------------------

There are ``select()``, ``update()``, ``delete()`` builders to query or manipulate miltiple items.

.. code-block:: java

    // Select is used to provide data to EntityCursorAdapter
   Select<EntityType> select = select().columns("_id", "name").where("external_id", Is.EQUAL, 10);
   
   // alternatively, call execute() to get the underlying Cursor
   Cursor cursor = select().where("name", Is.LIKE, "%%alex%%").execute();
   
   // use Where object for complex queries
   Where haveCoordinaltes = new Where("latitude", Is.NOT_EQUAL, 0).or("longitude", Is.NOT_EQUAL, 0);
   select().where("country", Is.EQUAL, "us").where(haveCoordinates);

Misc. methods
-------------

Methods that operate on a ``Select`` object:

*  ``long[] readIds(Select<EntityType> select)``
*  ``EntityType readFirst(Select<EntityType> select)``
*  ``ArrayList<EntityType> readAll(Select<EntityType> select)``

Methods that operate on an ``EntityType`` object:

*  ``void fillForeignKeys(EntityType item, String... columnNames)``


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
    
If column name is not specified via annotation, it will be ``field_name + _id``, e.g. ``track_id``.