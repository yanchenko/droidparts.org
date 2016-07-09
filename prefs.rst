====================
AbstractPrefsManager
====================

Simplifies working with SharedPreferences & adds ``SQLiteOpenHelper``-style versioning support.

Subclass it and use the following methods:

* ``void onUpgrade(SharedPreferences prefs, int oldVersion, int newVersion)``
* ``SharedPreferences getPreferences()``
* ``boolean readBoolean(int keyResId, int defValueResId)``
* ``int readInt(int keyResId, int defValueResId)``
* ``String readString(int keyResId, int defValueResId)``
* ``boolean saveBoolean(String key, boolean val)``
* ``boolean saveInt(String key, int val)``
* ``boolean saveLong(String key, long val)``
* ``boolean saveString(String key, String val)``