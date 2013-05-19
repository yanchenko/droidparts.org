===============
Getting Started
===============

General recommendation is to study the sample apps listed below to see DroidParts in action.
   
Repository Structure
====================

::

    git clone git@github.com:yanchenko/droidparts.git
    
and you'll see:

#. *droidparts* - the library.
#. *droidparts-test* - unit tests.
#. *droidparts-samples* - sample apps:
    #. ``DroidPartsGram`` - a better Instagram alternative. (:
    #. ``droidparts-sample`` - an older fragments-free sample app.
    
Obtaining
=========

The easy way is either to download the latest
`droidparts-x.y.z.jar <http://repository.sonatype.org/service/local/artifact/maven/redirect?r=central-proxy&g=org.droidparts&a=droidparts&v=LATEST>`_
and add it to ``libs`` folder or specify as a Maven dependency::

   <dependency>
     <groupId>org.droidparts</groupId>
     <artifactId>droidparts</artifactId>
     <version>${version.from.jar.above}</version>
   </dependency>
   
A slightly harder way is to use the library project + ActionBarSherlock required to compile it.

Configuration
=============

#. Subclass ``AbstractDBOpenHelper``.
#. Subclass ``AbstractDependencyProvider``.
#. Subclass ``AbstractApplication``\(optional).

:doc:`di` & :doc:`log` have options configurable via `AndroidManifest.xml`.
The first one is required.

ProGuard
========

Remember to include ``proguard-droidparts.cfg``.