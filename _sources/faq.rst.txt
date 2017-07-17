===
FAQ
===

Annotations Performance
=======================

Processing annotations on Android is known to be slow.

In DroidParts each annotation has a wrapper class.
The first time injection is performed on an object, annotations for it's class are read, wrapped and cached.

I've ran a `micro benchmark <https://gist.github.com/yanchenko/6151266>`_
on an ``Activity`` with 10 ``TextViews`` in it's ``layout.xml``.
Note that logging has to be silenced, otherwise you'll be benchmarking LogCat.

+------------------------------------+------------------+------------------+
| Benchmark, 10 000 iterations       | HTC Desire 2.3.7 | Galaxy Nexus 4.3 |
+====================================+==================+==================+
| ``findViewById()``                 | 1069ms           | 524ms            |
+------------------------------------+------------------+------------------+
| ``Injector.inject()``              | 1538ms           | 690ms            |
+------------------------------------+------------------+------------------+
| ``Injector.inject()``, caching off | 107447ms         | 43705ms          |
+------------------------------------+------------------+------------------+

The performance drop with annotations wrapped & cached is negligible.

Also check out this `blog post <http://eclipsesource.com/blogs/2012/09/28/mythbuster-android-annotation-performance-unravelled/>`_.

Crash after Layout Changes
==========================

Sometimes Eclipse doesn't update ids after Views get rearranged in a layout xml file.
This results in a strange startup crash.

To fix it, run *Project => Clean*.