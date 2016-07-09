===================
XML deserialization
===================

A simple way to convert Models to JSON objects & back. Similar to :doc:`JSON <json>`.
Based on the built-in ``org.w3c.dom`` parser.

Models
======

Model classes must extend ``Model`` or it's subclass (e.g. ``Entity``) and have fields annotated with ``@XML``.

@XML Annotation
---------------

* ``tag`` - XML tag name.
* ``attribute`` - XML tag attribute or nested tag names when deserializing a NodeList.
* ``optional`` - if true, won't throw an exception if the tag/attribute is missing.

Use ``XML.SUB`` separator in ``tag`` element to access nested object fields.

See ``XMLTestCase`` for an example.

XMLSerializer
==============

Has the following methods:

* ``static Document parseDocument(String xml)``
* ``ModelType deserialize(Node node)``
* ``ArrayList<ModelType> deserializeAll(NodeList nodeList)``