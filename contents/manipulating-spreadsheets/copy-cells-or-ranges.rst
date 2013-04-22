========================================
Copying Cells, Ranges, Rows Or Columns
========================================

The following api calls can be used to copy cells, ranges rows or columns into an existing spreadsheet page.

There are three different types of copy:

* ``copy``
* ``copystyle``
* ``copyvalue``

In a ``copy`` the entire cell, including any formatting, is copied.

In a ``copystyle`` only the formatting is copied.

In a ``copyvalue`` the whole cell is copied, but the **value** of the source cell is used as the formula in the **target** cell. For instance if the source cell has a formula of ``=1+1`` and a value of ``2`` the target will have a formula of ``2`` and a value of ``2``.

The cells that are copied to are overwritten.

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

Overview
--------

In the copy api the json structure contains range or cell where the copy is to be made from, and the URL contains the range or cell of the destination.

Copying A Cell Or Range
------------------------

For cell and range insertions the body can be one of the following json structures:

.. code-block:: javascript

    {"copy": {"src": "http://example.com/some/page/A1:A1"}}
    {"copystyle": {"src": "http://example.com/some/page/A1:A5"}}
    {"copyvalue": {"src": "http://example.com/some/page/B3:D7"}}

Copy Is A Tiling Operation
--------------------------

Copy is a tiling operation. The copy operation checks if the destination is an exact multiple of the source and if it is the source is tiled.

For example if the source was a 2 by 2 range in ``A1:A2`` with the following values:

``A1``: ``1``

``A2``: ``2``


If the destination was ``A10:D11`` the values would be:

``A10``: ``1``

``A11``: ``2``

``B10``: ``1``

``B11``: ``2``

If the target is not an exact mutliple of the source the destination range will be clipped.

If the destination is smaller than the source the copy will fail.

This behaviour is the same as in the GUI.

Copy Has Formula Rewriting
--------------------------

When formulae are copied the function references are rewritten.

This is the same behaviour as in the GUI.
