==========
DroidParts
==========

.. sidebar:: `GitHub <http://github.com/yanchenko/droidparts>`_ | `StackOverflow <http://stackoverflow.com/tags/droidparts>`_ | `Maven <http://search.maven.org/#search|ga|1|g%3A%22org.droidparts%22>`_
   
   .. image:: _static/images/droidparts_logo.*
   
   `Changelog <https://raw.github.com/yanchenko/droidparts/master/CHANGES>`_

is a carefully crafted Android framework that includes:

* *DI* - injection of Views, Fragments, Services, anything.
* *ORM* - efficient persistence utilizing Cursors & fluent API.
* *EventBus* for subscribing to and posting events.
* Simple *JSON* (de)serialization capable of handling nested objects.
* *XML* deserialization, similar to *JSON*.
* Improved *AsyncTask* & *IntentService* with Exceptions & result reporting support.
* *L*\ogger that figures out tag itself & logs any object.
* *RESTClient* for GETting, PUTting, POSTing, DELETing & InputStream-getting,
  also speaks JSON.
* *ImageFetcher* to asynchronously attach images to ImageViews, with caching,
  cross-fade & transformation support.
* Numerous *Utils*.

These features are available on Android 2.2+ & come in an under 300kB jar (→0 overengineering).

.. toctree::
   :maxdepth: 2
   
   introduction
   getting_started
   di
   activities
   orm
   adapters
   json
   xml
   prefs
   event_bus
   executors
   rest
   image_fetcher
   log
   utils
   widgets
   support
   converters
   faq
   
More useful code: https://gist.github.com/yanchenko

