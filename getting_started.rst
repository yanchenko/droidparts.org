===============
Getting Started
===============

My recommendation is to read this guide for an overview,
then study the sample apps to see DroidParts in action.
   
Repository Structure
====================

::

    git clone https://github.com/yanchenko/droidparts.git
    
and you'll see:

#. *droidparts* - the library.
#. *droidparts-samples* - sample apps:
    * ``DroidPartsGram`` - a better Instagram alternative. (:
    * ``droidparts-sample`` - an older fragment-free app.
#. *droidparts-test* - unit tests.
    
Obtaining
=========

You can download the latest
`droidparts-x.y.z.jar <http://repository.sonatype.org/service/local/artifact/maven/redirect?r=central-proxy&g=org.droidparts&a=droidparts&v=LATEST>`_
and add it to the ``libs`` folder.

Specify as a Maven dependency::

   <dependency>
     <groupId>org.droidparts</groupId>
     <artifactId>droidparts</artifactId>
     <version>${version.from.jar.above}</version>
   </dependency>
   
Use the library project + ActionBarSherlock required to compile it.

Configuration
=============

Even though DroidParts can be used as a set of libraries, it's full pontential is revealed in framework mode.

For that you'll need to subclass:

* ``AbstractDBOpenHelper`` for ORM.
* ``AbstractDependencyProvider`` and specify the subclass in `AndroidManifest.xml`: :doc:`di`.
* ``AbstractApplication``\(optional).

:doc:`log` is also configurable via `AndroidManifest.xml`.

ProGuard
========

Remember to include ``proguard-droidparts.cfg``.