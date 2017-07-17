==========
Activities
==========

DroidParts has several variants of base Activities living in the following packages:

* ``org.droidparts.activity.*`` - Android 2.2+ Activities & 3.0+ FragmentActivities.
* ``org.droidparts.activity.support.v4.*`` - Android 2.2+ with *Android Support Library* Fragments.
* ``org.droidparts.activity.support.v7.*`` - Android 2.2+ with *Android Support Library* Fragments & ActionBar.

By extending appropriate Activity, you get injection working. An alternative is calling ``Injector.inject(this);``.

You'll get an extra lifecycle method called ``onPreInject()``.
It's used to set some data that should be present at injection time. Usually a layout.

.. code-block:: java

   @InjectView
   private Button btn;

   @Override
   public void onPreInject() {
      setContentView(R.layout.activity);
   }

   @Override
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState); // <- btn is injected during this call.
      // Too late to set content view here.
   }

Activity & FragmentActivity
===========================

There are variants of this class for pre-3.0 Androids with or w/o ActionBar support & for modern Androids.
The versions with ActionBar support have the following extra methods:

* ``setActionBarReloadMenuItem(MenuItem menuItem)`` - which MenuItem triggers reload, if any.
* ``setActionBarLoadingIndicatorVisible(boolean visible)`` - show spinner for the item set on previous step.
* ``setFragmentVisible(boolean visible, Fragment... fragments)`` - a shortcut method to show/hide Fragments.

SingleFragmentActivity
======================

Base class for Activities with only one Fragment.

* ``F onCreateFragment()`` - implement to return a Fragment.

TabbedFragmentActivity
======================

ActionBar-based tabs navigation with custom animation support.

* ``addTab(ActionBar.Tab tab, Fragment... tabFragments)`` & ``addTab(int position, ActionBar.Tab tab, Fragment... tabFragments)``
* ``setCustomAnimations(int enter, int exit)``
* ``setCurrentTab(int position)`` & ``getCurrentTab()``
* ``onTabChanged(int position)``
