Custom Converters
=================

:doc:`ORM <orm>`, :doc:`JSON <json>` & :doc:`XML <xml>` support the following types:

* primitives & wrappers
* String
* Enum
* Date
* UUID
* Uri
* JSONObject
* JSONArray
* Bitmap
* Model & Entity
* arrays & collections of the above
* Maps

If you need to support an extra type:

#. Subclass ``Converter``, implement required methods. See existing converters for an example.
#. Register it by calling ``AbstractApplication.registerConverter(Converter<?> converter);``.

For custom JSON/XML deserialization, subclass ``ModelConverter`` or ``EntityCoverter`` and override the following methods:

* ``getJSONSerializer(Class<M> valType, JSONObject src)``
* ``getXMLSerializer(Class<M> valType, Node src)``
   