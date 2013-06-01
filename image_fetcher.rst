============
ImageFetcher
============

Downloads Images and attaches them to ImageViews.

* Disk & in-memory caching.
* Effective image decoding.
* inBitmap support.
* Cross-fade support.

Customizing
===========

See constructor, ``BitmapMemoryCache``, ``BitmapDiskCache``.

ImageReshaper
=============

Processes(resizes, rounds corners, etc.) bitmaps in background & caches the result.

ImageFetchListener
==================

Receives callbacks.

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
