==========
RESTClient
==========

*RESTClient* greatly simplifies http interactions & is designed for :doc:`executors`.

* Uses gzip|deflate compression.
* Supports in and out headers.
* Transparent cookies support.
* Http basic auth.
* ETag & If-Modified-Since support.
* Getting response as String or InputStream.
* POST multipart file.

Configuration
=============

Constructors
------------

* ``RESTClient(Context ctx)``
* ``RESTClient(Context ctx, String userAgent)``
* ``RESTClient(Context ctx, HTTPWorker worker)``

Methods
-------

* ``setCookieCacheEnabled(boolean enabled, boolean persistent)``
* ``setHeader(String key, String value)``
* ``authenticateBasic(String username, String password)``
* ``setFollowRedirects(boolean follow)``

Usage
=====

* ``get(String uri)``
* ``getInputStream(String uri)``
* ``get(String uri, long ifModifiedSince, String etag, boolean body)``
* ``post(String uri, String contentType, String data)``
* ``postMultipart(String uri, String name, String contentType, String fileName, InputStream is)``
* ``put(String uri, String contentType, String data)``
* ``delete(String uri)``

Each of these methods returns a ``HTTPResponse`` or throws a ``HTTPException``.


RESTClient2
===========

*RESTClient2* is a subclass that adds JSON support & more features.

* ``JSONObject getJSONObject(String uri)``
* ``HTTPResponse post(String uri, JSONArray data)``
* ``HTTPResponse postMultipart(String uri, String name, File file)``
* ...

Workers
================

*RESTClient* internally uses workers to get the job done.
By default, *HttpUrlConnection* worker is used (with http caching on API > 13).
On pre-2.3.3 Androids (API < 10) it falls back to *Apache HttpClient*.

It's also possible to construct RESTClient using a custom worker.