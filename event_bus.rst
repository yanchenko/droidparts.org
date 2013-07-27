=========
Event Bus
=========

EventBus comes handy when you have a set of listeners that care about some events that happen in the background.
Like an incoming message in a messenger app.

Events
======

An event can either consist of a single String or String + data Object.
Events are posted using ``EventBus.postEvent(...)`` or ``EventBus.postEventSticky(...)``.
Posting an event sticky means that it's most recent version will be delivered to newly registered receivers.

Events are guaranteed to be delivered on the main thread.

Event Receivers
===============

In an Activity that extends base DroidParts Activities, the simplest way to register for Events is to use annotated methods::

   @ReceiveEvents(name = { "MESSAGE_SENT", "MESSAGE_RECEIVED" })
   private void onMessageEvent(String eventName) {
      // TODO process 2 kinds of events without data
   }

   @ReceiveEvents
   private void onAnyEvent(String eventName, Object eventData) {
      // TODO process any event with optional data
   }
   
You can also register arbitrary ``EventReceiver``\s with ``EventBus.registerReceiver(...)``.
And don't forget to call ``EventBus.unregisterReceiver(...)``.
