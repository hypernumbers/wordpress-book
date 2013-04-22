===============================
Reading A Some Columns Of Cells
===============================

The following API call will return the json representation of some columns of cells

=========== ======================================
Component   Details
=========== ======================================
Method      ``GET``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/some/page/c:d``
=========== ======================================

The json returned is identical to that returned by a whole page request, except:

* the object value is now a column range of the form ``C:D``
* only cells that are in the columns
