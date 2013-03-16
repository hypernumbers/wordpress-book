Reading A Cell
--------------

The following API call will return the json representation of a cell

=========== ======================================
Component   Details
=========== ======================================
Method      ``GET``

Headers     ``{"Accept", "json/application"}``

URL         ``http://example.com/some/page/b7``
=========== ======================================

The json returned is identical to that returned by a whole page request, except:

* the object value is now a cell of the form ``b7``
* the cell object contains details of that cell only
* only rows that intersect with the cell are returned
* only columns that intersect with the cell are returned
