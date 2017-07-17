============
ImageFetcher
============

Downloads Images and attaches them to ImageViews.

* Disk & in-memory caching.
* Efficient image decoding.
* inBitmap support.
* Cross-fade support.

Methods:

* ``void attachImage(String imgUrl, ImageView imageView)``
* ``void attachImage(String imgUrl, ImageView imageView, int crossFadeMillis)``
* ``void attachImage(String imgUrl, ImageView imageView, ImageReshaper reshaper, int crossFadeMillis)``
* ``void attachImage(String imgUrl, ImageView imageView, ImageReshaper reshaper, int crossFadeMillis, ImageFetchListener listener)``
* ``void attachImage(String imgUrl, ImageView imageView, ImageReshaper reshaper, int crossFadeMillis, ImageFetchListener listener, Bitmap inBitmap)``

* ``Bitmap getImage(String imgUrl) throws Exception``
* ``Bitmap getImage(String imgUrl, ImageView hintImageView, ImageReshaper reshaper) throws Exception``
* ``void clearCacheOlderThan(int hours)``

Customization
=============

See constructor, ``BitmapMemoryCache``, ``BitmapDiskCache``.

ImageReshaper
=============

Modifies (resizes, rounds corners, etc.) bitmaps in background & caches the result.

* ``String getCacheId()``
* ``Pair<CompressFormat, Integer> getCacheFormat(String mimeType)``
* ``Bitmap.Config getBitmapConfig()``
* ``int getImageWidthHint()``
* ``int getImageHeightHint()``
* ``Bitmap reshape(Bitmap bm)``

See AbstractImageReshaper for default implementation.

ImageFetchListener
==================

Receives fetch cycle callbacks.

* ``void onFetchAdded(ImageView imageView, String imgUrl)``
* ``void onFetchProgressChanged(ImageView imageView, String imgUrl, int kBTotal, int kBReceived)``
* ``void onFetchFailed(ImageView imageView, String imgUrl, Exception e)``
* ``void onFetchCompleted(ImageView imageView, String imgUrl, Bitmap bm)``

Pausing
=======

ImageFetcher can be paused while scrolling.
See ``ImageListAdapter`` from *DroidPartsGram* for an example.

.. code-block:: java
   
   @Override
   public void onScrollStateChanged(AbsListView view, int scrollState) {
      switch (scrollState) {
      case OnScrollListener.SCROLL_STATE_FLING:
         imageFetcher.pause();
         break;
      default:
         imageFetcher.resume(true);
      }
   }
