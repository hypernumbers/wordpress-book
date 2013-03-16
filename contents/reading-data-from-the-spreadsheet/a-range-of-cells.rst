Reading A Range Of Cells
------------------------

The following API call will return the json representation of a range of cells

=========== ======================================
Component   Details
=========== ======================================
Method      ``GET``

Headers     ``{"Accept", "json/application"}``

URL         ``http://example.com/some/page/a1:d8``
=========== ======================================

The json returned is identical to that returned by a whole page request, except:

* the object value is now a range of the form ``A1:D5``
* only cells that are included in the range are returned
* only rows that intersect with the range are returned
* only columns that intersect with the range are returned
