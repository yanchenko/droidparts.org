=========
Event Bus
=========

EventBus (aka message bus) comes handy when you have a set of listeners that care about events that happen somewhere else.

Like displaying an incoming message in a messenger app.

Events
======

Each event has a String name and an optional data Object.

Events can be posted from any thread, will be delivered on the main (aka UI) thread.

Ordinary Events
---------------

* ``EventBus.postEvent(String name)``
* ``EventBus.postEvent(String name, Object data)``

Sticky Events
-------------

Posting an event sticky means that it's most recent version will be delivered to the newly registered receivers.

* ``EventBus.postEventSticky(String name)``
* ``EventBus.postEventSticky(String name, Object data)``
* ``EventBus.clearStickyEvents(String... eventNames)``

Event Receivers
===============

In classes that extends base DroidParts Activities & Fragments, the simplest way to register for Events is to use annotated methods::

   @ReceiveEvents(name = { "MESSAGE_SENT", "MESSAGE_RECEIVED" })
   private void onMessageEvent(String eventName) {
      // TODO process 2 kinds of events without data
   }

   @ReceiveEvents
   private void onAnyEvent(String eventName, Object eventData) {
      // TODO process any event with optional data
   }
   
This will generate receivers that are registered in ``onResume()`` and unregistered in ``onPause()``.
   
``EventReceiver``\s created manually can be registered and must be unregistered to avoid leaks:

* ``EventBus.registerReceiver(EventReceiver<?> receiver, String... eventNames)``
* ``EventBus.unregisterReceiver(EventReceiver<?> receiver)``
