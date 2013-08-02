====================
Dependency Injection
====================

DroidParts injects views, fragments, services, resources etc. out-of-box.
Custom dependencies can be defined in a ``DependencyProvider`` class.

Injection occurs automatically in classes that extend Activities/Services/Fragments that come with DroidParts.

To inject manually, call ``Injector.inject(...)``.

DependencyProvider
==================

DependencyProvider is a subclass of ``AbstractDependencyProvider`` with methods
that return objects to be injected.

The supported method signatures are:

.. code-block:: java

    public CustomObject getCustomObject();
    // and
    public CustomObject getCustomObject(Context ctx);

in the latter case ``Context`` will be the one that that requested injection (e.g. an ``Acitvity``).

Setup
-----

There's one special method to be implemented:
``public abstract AbstractDBOpenHelper getDBOpenHelper();``.

The newly created class must be specified in ``AndroidManifest.xml``:

.. code-block:: xml

    <application >
            
        <meta-data
            android:name="droidparts_dependency_provider"
            android:value=".DependencyProvider" />
            
    </application>
    
Activities & Fragments
======================

Extend classes from packages ending with one of the following affixes when targeting:

* ``.stock`` - API 11+, e.g. ``org.droidparts.fragment.stock.Fragment``.
* ``.support`` - API 8+ with Android Support library, e.g. ``org.droidparts.fragment.support.Fragment``.
* ``.sherlock`` - API 8+ with ActionBarSherlock, e.g. ``org.droidparts.fragment.sherlock.Fragment``.

Annotations
===========

* *@InjectView*::

    @InjectView
    Button btn1;
    // btn1 = (Button)findViewById(R.id.btn1)
    
    @InjectView(id=R.id.view_btn, click=true)
    Button btn2;
    // btn2 = (Button)findViewById(R.id.view_btn)
    // btn2.setOnClickListener(this);
    
  For ``click=true`` to work, the class must implement ``View.OnClickListener``.
  Also works for Preferences.
* *@InjectBundleExtra*:
    * in an ``Activity`` = ``getIntent().getExtras().getXX()``.
    * in a ``Fragment`` = ``getArguments().getXX()``.
* *@InjectDependency* - custom dependency from ``DependencyProvider``.
* *@InjectResource* - String, String[], Drawable, etc. from res.
* *@InjectSystemService* = ``getSystemSerice(Context.SERVICE_NAME)``.
* *@InjectFragment* - in ``FragmentActivity``, inject ``Fragment`` specified in layout xml.
* *@InjectParentActivity* - in ``Fragment``, inject the ``Actvity`` it belongs to.
