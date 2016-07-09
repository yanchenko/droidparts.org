===============
Getting Started
===============

I suggest to read this guide for an overview,
then study the sample apps to see DroidParts in action.
   
Repository Structure
====================

::

    git clone https://github.com/yanchenko/droidparts.git
    
and you'll see:

#. *droidparts* - the library.
#. *droidparts-support* - :doc:`support`.
#. *droidparts-samples* - sample apps:
    * ``DroidPartsGram`` - a better Instagram alternative. (:
    * ``droidparts-sample`` - an older fragment-free app.
#. *droidparts-test* - unit tests.
    
Integration
===========

There are several options:

* Download the latest `droidparts-x.y.z.jar <http://repository.sonatype.org/service/local/artifact/maven/redirect?r=central-proxy&g=org.droidparts&a=droidparts&v=LATEST>`_ and put it to the ``libs`` folder.

* Specify as a Gradle or Maven dependency::

.. code-block:: groovy

    dependencies {
        compile 'org.droidparts:droidparts:${version.from.jar.above}'
    }

.. code-block:: xml

    <dependency>
      <groupId>org.droidparts</groupId>
      <artifactId>droidparts</artifactId>
      <version>${version.from.jar.above}</version>
    </dependency>

Example: `build.gradle <https://github.com/yanchenko/droidparts/blob/master/droidparts-samples/DroidPartsGram/build.gradle>`_ from DroidPartsGram.

Dependencies
============

Optional dependencies:

* *Android Support library* - if using classes in ``*.support.*`` packages (part of *droidparts-support*).
  Also required by ``ImageFetcher`` for in-memory cache to work on pre-3.0 Androids.
* *Apache HttpMime* required by ``RESTClient`` if POSTing multipart files on pre-3.0 Androids.

Configuration
=============

Even though DroidParts can be used as a set of libraries, it's full pontential is revealed in framework mode.

For that you'll need to subclass:

* ``AbstractDBOpenHelper`` for ORM.
* ``AbstractDependencyProvider`` and specify the subclass in `AndroidManifest.xml`: :doc:`di`.
* ``AbstractApplication`` (optional).

:doc:`log` is also configurable via `AndroidManifest.xml`.

ProGuard
========

If using ProGuard, remember to include *proguard-droidparts.cfg*::

   proguard.config=${sdk.dir}/tools/proguard/proguard-android-optimize.txt:../droidparts/proguard-droidparts.cfg
