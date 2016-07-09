======================
JSON (de)serialization
======================

A simple way to convert Models to JSON objects & back. Conceptually similar to :doc:`ORM <orm>`.
Based on the built-in ``org.json`` parser.

Models
======

Model classes must extend ``Model`` or it's subclass (e.g. ``Entity``) and have fields annotated with ``@JSON``.

@JSON Annotation
----------------

* ``key`` - JSON key name.
* ``optional`` - if true, won't throw an exception if the key is missing and won't put a key with a null value.

Use ``JSON.SUB`` separator in ``name`` element to access nested object fields.

E.g.::

   {
     "sub_obj": {
       "str": "val"
     }
   }
   
   @JSON(key = "sub_obj" + JSON.SUB + "str")
   public String str;

JSONSerializer
==============

Has the following methods:

* ``JSONObject serialize(ModelType item)``
* ``ModelType deserialize(JSONObject obj)``
* ``JSONArray serializeAll(Collection<ModelType> items)``
* ``ArrayList<ModelType> deserializeAll(JSONArray arr)``

Customization
-------------
Override ``readFromJSON(...)`` and/or ``putToJSON(...)`` methods or create a custom :doc:`Converter <converters>`.