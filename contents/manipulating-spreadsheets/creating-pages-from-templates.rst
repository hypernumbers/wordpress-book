=============================
Creating Pages From Templates
=============================

The following api call will create a new page from a template

=========== ======================================
Component   Details
=========== ======================================
Method      ``POST``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/some/page/``

URL Type    Page URL
=========== ======================================

The body is a the following json structure:

.. code-block:: javascript

        {"load_template": {"name": "sometemplate"}}
