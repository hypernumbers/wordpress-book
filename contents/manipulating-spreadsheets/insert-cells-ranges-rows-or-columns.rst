========================================
Inserting Cells, Ranges, Rows Or Columns
========================================

The following api calls can be used to insert cells, ranges rows or columns into an existing spreadsheet page.

Any cell functions that reference cells that are moved by insertions will be written to point to the new cell location. This behaviour is the same as in the GUI.

=========== ======================================
Component   Details
=========== ======================================
Method      ``POST``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/some/page/a5``

            ``http://example.com/some/page/a5:b6``

            ``http://example.com/some/page/a:b``

            ``http://example.com/some/page/5:6``

URL Types   * Cell URL
            * Range URL
            * Row URL
            * Column URL
=========== ======================================

Cell And Range Insertions
-------------------------

For cell and range insertions the body can be one of the following json structures:

.. code-block:: javascript

    {"insert": "after"}
    {"insert": "before"}

A **before** insert puts the new cells before the URL you post the insertion to and an **after** insert puts the new cells after.

By default, cell and range inserts displace vertically. So if you insert **before** ``a5`` the existing ``a5`` will become ``a6``.

You can specify the direction of displacement:

.. code-block:: javascript

    {"insert": "horizontal"}
    {"insert": "vertical"}

In both these cases the insertion is a **before** insertion.

For example a **vertical** insertion on ``a5`` will make that cell ``a6`` and a horizontal one will make it ``b5``.

Row And Column Insertions
-------------------------

For row and column insertions the body can be one of the following json structures:

.. code-block:: javascript

    {"insert": "after"}
    {"insert": "before"}

A **before** insert puts the new cells before the URL you post the insertion to and an **after** insert puts the new cells after.

Obviously row insertions displace vertically and column insertions displace horizontally.

