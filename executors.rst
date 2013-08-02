=====================
Working in Background
=====================

AsyncTask
=========

``AsyncTask`` & ``SimpleAsyncTask`` support ``AsyncTaskResultListener`` and return either a Result or an Exception.

IntentService
=============

Similarly, ``IntentService`` is extended to support ``ResultReceiver``. Also has ``void removePendingIntents()`` method.