=============
Drag And Drop
=============

The following api call can be used to drag and drop an existing cell onto a destination range.

=========== ======================================
Component   Details
=========== ======================================
Method      ``POST``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/some/page/a5``

URL Type    Cell URL
=========== ======================================

Overview
--------

In drag and drop the cell in the URL is the one that is being dragged and it is dropped into the range that is specified by the json structure.

Drag And Drop
-------------

The body is a the following json structure:

.. code-block:: javascript

        {"drag": {"range": "A6:A6"}}

Notes
-----

The destination range **MUST** be a either 1 column-wide or 1-row high. The following are valid ranges to drag to:

* ``d5:d17``
* ``d5:j5``

Other types of ranges will result in an error, for example:

* ``d5:e6``

The destination range need not be on the same page, for example the following destination range is valid:

* ``../different/page/d5:d17``
