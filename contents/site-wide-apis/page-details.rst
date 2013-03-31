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

Security
--------

This API user is **NOT** required to have admin rights in the API.

Returns
-------

It returns a json structure that contains the page structure of the site.

The meaning of the json is defined below:

=============== ================================================================
Section         Meaning
=============== ================================================================
``pages``       The top level page is called ``home``

``children``    each name represnts a sub URL
=============== ================================================================

An example of the json is shown below:

.. code-block:: javascript

    {
        "pages": {
            "name": "home",
            "children": [
                {
                    "name": "some",
                    "children": [
                        {
                            "name": "other"
                        },
                        {
                           "name": "page"
                        }
                    ]
                }
            ]
        }
    }
