=======
Logging
=======

``L`` takes the pain away from logging.

.. code-block:: java

    L.i("DroidParts is awesome!");
    // or
    L.w(anyObject);
    // or
    L.a("WTF?! %s", str);
     
will result in ``LogCat`` output like::

     ClassName.methodName():50 DroidParts is awesome!

in development mode.
In a production build (a signed .apk) the tag will be the package name.

Configuration
=============

In debug mode all output is logged. Loglevel for production is configured in
``AndroidManifest.xml``:

.. code-block:: xml

    <application >
            
        <meta-data
            android:name="droidparts_log_level"
            android:value="warn" />
            
    </application>
    
Available loglevels:

* disable
* verbose
* debug
* info
* warn
* error
* assert

By default all log output is stripped.