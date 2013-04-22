============
Site Details
============

Overview
------------

This is a json feed that provides core information about the Vixo site

Details
-------

Site details are provided in json format by:

.. tabularcolumns:: |l|L|

=========== ==================================
Component   Details
=========== ==================================
Method      ``GET``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/_site/``
=========== ==================================

Security
--------

This API user is **NOT** required to have admin rights in the API.

Returns
-------

It returns a json structure that describes the site.

The meaning of the json is defined below:

=============== ================================================================
Section         Meaning
=============== ================================================================
``templates``   a list of templates on the site which can be used to instantiate
                new spreadsheet pages

``maps``        a list of maps on the site which can be used to upload cvs or
                Excel files and map the data to pages, cells and templates

``is_admin``    is the current user an administrator on the site

``lang``        what language the GUI is to be displayed in

``groups``      what user groups there are on the site
=============== ================================================================

An example of the json is shown below:

.. code-block:: javascript

    {
        "templates": [
            "blank",
            "user_def_fns"
        ],
        "maps": [],
        "is_admin": true,
        "lang": "en_gb",
        "groups": [
            "admin",
            "user"
        ]
    }
