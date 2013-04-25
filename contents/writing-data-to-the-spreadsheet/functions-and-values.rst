============================
Writing Functions And Values
============================

The following API call will write a function to a cell or range of cells.

=========== ======================================
Component   Details
=========== ======================================
Method      ``POST``

Headers     ``"{"set": {"formula": "333"}}"``

            ``"{"set": {"formula": "3.33"}}"``

            ``"{"set": {"formula": "3.33e+33"}}"``

            ``"{"set": {"formula": "'333"}}"``

            ``"{"set": {"formula": "abc"}}"``

            ``"{"set": {"formula": "ab\"c"}}"``

            ``"{"set": {"formula": "true"}}"``

            ``"{"set": {"formula": "#REF!"}}"``

            ``"{"set": {"formula": "=1+2"}}"``

            ``"{"set": {"formula": "'=1+2"}}"``

            ``"{"set": {"formula": "1/2/3"}}"``

URL         ``http://example.com/some/page/b7``

            ``http://example.com/some/page/b7:b9``
=========== ======================================

Notes
-----

All constants are passed in as a formula and all formula are strings. The formula string should appear exactly as you would type it into a cell.

If you wish to put double quotes in a string it must be escaped with a single backslash.

If you attempt to pass in integers, floats of booleans in as native data types your request will fail:

Right way:

.. code-block:: javascript

    ``"{"set": {"formula": "333"}}"``

    ``"{"set": {"formula": "3.33"}}"``

    ``"{"set": {"formula": "true"}}"``

Wrong way:

.. code-block:: javascript

    ``"{"set": {"formula": 333}}"``

    ``"{"set": {"formula": 3.33}}"``

    ``"{"set": {"formula": true}}"``

Forcing Strings
---------------

All formulas can be escaped to a string by starting them with a smart quote - exactly as in the GUI:

.. code-block:: javascript

    ``"{"set": {"formula": "'=1+2+3"}}"``

This will evaluate to the string ``=1+2+3`` and not to the value ``6``.

Strings that look like dates will resolve to dates as in the GUI.

Inputting HTML
--------------

The security model allows spreadsheet users to put arbritrary html into cells **if the formula starts with an opening** ``<``.

Consider the following:

.. code-block:: javascript

    ``"{"set": {"formula": "<h1>Hey!</h1>"}}"``

This will resolve to the HTML fragment ``<h1>Hey!</h1>``.

By contrast the following:

.. code-block:: javascript

    ``"{"set": {"formula": "Hey! <h1>Hey!</h1>"}}"``

    ``"{"set": {"formula": "'<h1>Hey!</h1>"}}"``


These will resolve to ``Hey! &lt;Hey!&gt;`` and ``'&lt;Hey!&gt;`` respectively.

.. Note::

     If a cell is made user editable on a wiki page as an input cell the input is automatically escaped - effectively the same as sharp quoting all formulae. Wiki users cannot enter either formulae or html into a cell - only string, integers, floating point numbers, booleans and errors.

Writing Arrays
--------------

Specifying a single formula on a range url will write that formula to every cell in the range.

If you wish to write a range of formulae that rewrite to offset by a row as you go down you can write the first cell using this API and then use either the **drag and drop** or the **copy** API calls. This will enable you to emulate the normal user way of entering ranged formula.

You can also write complete arrays of formulae using the array version of this API with a range formula:

=========== ===================================================================================
Component   Details
=========== ===================================================================================
Method      ``POST``

Headers     ``"{\"set\":{\"formula\":[[\"A1\", \"B1\"],[\"A2\", \"B2\"],[\"A3\", \"B3\"]]}}"``

URL         ``http://example.com/some/page/A1:B3``
=========== ===================================================================================

The array of values is laid out in rows. If the two dimensional array of values is not congruent with the range described in the URL this request will return a ``401`` error.

If the value ``""`` is passed in an array like this **it will not be written** - the cell will be considered to be unwritten (or unwritten over). The purpose of this is to enable data that behaves correctly in the ``=countblank()`` function. If you wish to clear cells use the clear API.
