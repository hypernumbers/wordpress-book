Reading Some Rows Of Cells
--------------------------

The following API call will return the json representation of some rows of cells.

=========== ======================================
Component   Details
=========== ======================================
Method      ``GET``

Headers     ``{"Accept", "json/application"}``

URL         ``http://example.com/some/page/2:3``
=========== ======================================

The json returned is identical to that returned by a whole page request, except:

* the object value is now a row range of the form ``2:3``
* only cells on those rows are returned
