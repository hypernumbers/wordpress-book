=================
Pages On The Site
=================

Overview
--------

This is a json feed that gives a tree of all the pages on the Vixo site.

Details
-------

Page details are provided in json format by:

.. tabularcolumns:: |l|L|

=========== ==================================
Component   Details
=========== ==================================
Method      ``GET``

Headers     ``{"Accept", "json/application"}``

URL         ``http://example.com/_pages/``
=========== ==================================

It returns a json structure that contains the page structure of the site.

An example of it within Firebug is shown below:

.. image:: /images/underscore-pages.png
   :scale: 100 %
   :align: center
   :alt:   Getting a list of pages
