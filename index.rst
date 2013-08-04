==========
DroidParts
==========

.. sidebar:: `GitHub <http://github.com/yanchenko/droidparts>`_ | `StackOverflow <http://stackoverflow.com/tags/droidparts>`_ | `Maven <http://search.maven.org/#search|ga|1|g%3A%22org.droidparts%22>`_
   
   .. image:: _static/images/droidparts_logo.*
   
   http://github.com/yanchenko/droidparts

is a carefully crafted Android framework that includes:

* *DI* - injection of Views, Fragments, Services, etc.
* *ORM* - efficient persistence utilizing Cursors & fluent API.
* *EventBus* for posting event notifications.
* Simple *JSON* (de)serialization capable of handling nested objects.
* Improved *AsyncTask* & *IntentService* with Exceptions & result reporting support.
* *L*\ogger that figures out tag itself & logs any object.
* *RESTClient* for GETting, PUTting, POSTing, DELETing & InputStream-getting,
  also speaks JSON.
* *ImageFetcher* to asynchronously attach images to ImageViews, with caching,
  cross-fade & transformation support.
* Numerous *Utils*.
* *Fragments* support: native on 3.0+ and either
  pure `SupportLibrary <http://developer.android.com/tools/extras/support-library.html>`_
  or `ActionBarSherlock <https://github.com/JakeWharton/ActionBarSherlock>`_-backed on 2.2+.

All these features come in an under 300kB jar which means →0 overengineering.

.. toctree::
   :maxdepth: 2
   
   introduction
   getting_started
   di
   orm
   event_bus
   adapters
   prefs
   json
   executors
   rest
   fragments
   image_fetcher
   log
   utils
   widgets
   faq
   
More useful code: https://gist.github.com/yanchenko

