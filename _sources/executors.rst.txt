=====================
Working in Background
=====================

AsyncTask
=========

``AsyncTask`` & ``SimpleAsyncTask`` support ``AsyncTaskResultListener`` that has methods to handle either a Result or an Exception.

Subclass, overrride ``Result onExecute([Params... params]) throws Exception``;

Override the following methods for any additional processing in the background:

* ``void onPostExecuteSuccess(Result result)``
* ``void onPostExecuteFailure(Exception exception)``
   

IntentService
=============

Similarly, ``IntentService`` is extended to support ``ResultReceiver``. Has ``void removePendingIntents()`` method.

Subclass, overrride ``Bundle onExecute(String action, Bundle data) throws Exception``;