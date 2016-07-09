========
Adapters
========
DroidParts extends a number of Android adapters adding dependency injection & features. 

Cursor Adapters
===============

CursorAdapter
-------------

* ``LayoutInflater getLayoutInflater()``
* ``void requeryData()``

EntityCursorAdapter
-------------------

Extends *CursorAdapter* and utilizes *EntityManager* features. The one usually used.

Constructors:

* ``EntityCursorAdapter(Context ctx, Class<EntityType> entityCls)`` - for the Entity class specified.
* ``EntityCursorAdapter(Context ctx, Class<EntityType> entityCls, AbstractSelect<EntityType> select)`` - as previous, also providing the data.
* ``EntityCursorAdapter(Context ctx, EntityManager<EntityType> entityManager, AbstractSelect<EntityType> select)``, as previous, but using a custom EntityManager.

Methods:

* ``void setContent(AbstractSelect<EntityType> select)`` - change the content.
* ``void bindView(Context context, View view, EntityType item)`` - override to populate a row View from Entity. Note that foreign keys won't be filled in for performance reasons. Use ``entityManager.fillForeignKeys(EntityType item, String... columnNames)``.
* ``boolean create(EntityType item)``
* ``EntityType read(int position)``
* ``boolean update(EntityType item)``
* ``boolean delete(int position)``

Widget Adapters
===============

ArrayAdapter
------------

* ``void setContent(Collection<T> coll)``

SpinnerAdapter
--------------

* ``void setSelectedItem(T item)``
* ``T getSelectedItem()``

*StringSpinnerAdapter*

TextWatcherAdapter
------------------

*TextWatcherListener*

ViewHolders
===========

ViewHolder pattern with automatic injection.

*ViewHolder*, *Text1Holder*, *Text2Holder*, *IconText2Holder*

E.g.::

   View view = layoutInflater.inflate(android.R.layout.simple_list_item_2);
   Text2Holder holder = new Text2Holder(view);
   view.setTag(holder);
   //
   holder.text1.setText("Text 1");
   holder.text2.setText("Text 2");
