==============================================
Deleting Cells, Ranges, Rows, Columns Or Pages
==============================================

The following api calls can be used to delete cells, ranges rows or columns from an existing spreadsheet page - or the page itself, and all its contents.

On a deletion, any cell functions that reference the deleted cells will be written and replaced with an ``#REF!`` error. This is the same behaviour as the GUI.

On a deletion, any cell functions that reference the cells that have moved will be rewritten to refer to the new location. This is the same behaviour as in the GUI.

On a page deletion, any cell functions that reference the page that has been deleted will be written. This is the same behaviour as in the GUI.

Note
----

When this API is used to delete cells, ranges, rows and columns it deletes them **from a page** but the page continues to exist.

When this API is used to delete a page **the page and the cells that were on it are deleted**.

=========== ======================================
Component   Details
=========== ======================================
Method      ``POST``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/some/page/a5``

            ``http://example.com/some/page/a5:b6``

            ``http://example.com/some/page/a:b``

            ``http://example.com/some/page/5:6``

            ``http://example.com/some/page/``

URL Types   * Cell URL
            * Range URL
            * Row URL
            * Column URL
            * Page URL
=========== ======================================

Cell And Range Deletions
-------------------------

For cell and range deletions the body can be one of the following json structures:

.. code-block:: javascript

    {"delete": "horizontal"}
    {"delete": "vertical"}

A **vertical** delete fills the space by shifting the cells that were below up, and a **horizontal** delete fills the space by shifting the cells that were to the right leftwards.


Row And Column Deletions
-------------------------

For row and column deletions the body is:

.. code-block:: javascript

    {"delete": "all"}

Obviously row deletions displace vertically and column deletions displace horizontally.

Page Deletion
-------------

For page deletions the body is:

.. code-block:: javascript

    {"delete": "all"}

When a page is deleted, not only are the cells deleted, but the page is removed from the list of pages on the website, and all functions that depend on that structure (for example html menu functions) will rewrite.
