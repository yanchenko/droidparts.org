======================
JSON (de)serialization
======================

``JSONSerializer`` converts Models to JSON objects & back.

Models
======

Mapping classes must extend ``Model`` or it's subclass.

@Key Annotation
---------------

* ``name``
* ``optional``

Nested JSON Objects
-------------------

Use ``JSONSerializer.__`` separator in ``name`` element to access nested objects.
