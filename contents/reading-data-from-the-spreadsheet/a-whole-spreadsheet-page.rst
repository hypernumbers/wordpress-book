================================
Reading A Whole Spreadsheet Page
================================

Here is an example page with some formatting:

.. image:: /images/some-page.png
   :scale: 100 %
   :align: center
   :alt:   a spreadsheet page

The following API call will return the json representation of this page

=========== ==================================
Component   Details
=========== ==================================
Method      ``GET``

Headers     ``{"Accept", "application/json"}``

URL         ``http://example.com/some/page/``
=========== ==================================

This returns a json description of a page - an example is shown later.

The meaning of each top level member of the json is defined below:

=============== =======================================================================
Section         Meaning
=============== =======================================================================
``styles``      A global style for the spreadsheet, identified by an index
                value. The style can include the following css attributes:

                ``color``

                ``vertical-align``

                ``background-color``

                ``font-weight``

                ``font-size``

                ``font-family``

                ``font-style``

                ``font-stretch``

                ``text-decoration``

                ``text-shadow``

                ``text-align``

                ``white-space``

``views``       The views available to the user - because the user is an api
                call this is always an empty list.

``column``      Column attributes organised in a 2 dimensional array
                representing ranges - a nested set of 1, 1 would be a column
                range ``A:A``. Normally contains width attributes in pixels.
                The GUI constrains the user to set widths in terms of 1/4
                standard cell widths - the standard cell being 80 pixels wide.

``object``      What this json represents, might be:

                ``page`` - for all the cells on a page

                ``A1:B7`` - a range value

``cell``        A 2 dimensional array identifying individual cells - the first
                index is the row index (ie ``1``, ``2`` or ``3``) and the second
                index is the column index (ie ``A``, ``B``, ``C``). Each cell
                has the following mandatory contents:

                ``formula`` - the original formula of the cell

                ``__rawvalue`` - the result of the calculation

                ``style`` - an index to the style table

                ``format`` - an Excel compatible format applied to the cell

                ``value`` - the result of applying the format to the raw value

                ``overwrite-color``

                In addition there are a number of other options that might be
                present:

                ``ghost`` if ``ghost`` is set to ``true`` the cell is a
                `ghost cell`_ that doesn't appear to people getting the web or
                wiki view.

                ``merge`` - json structure with the form
                ``{"down": 2, "right", 3}`` that describes cell merges, the
                cells covered by the merge are hidden

                ``input`` - cells marked input become input cells in the
                `wiki view`_. Input can take one of three values:

                 * ``inline``
                 * ``inlinerich``
                 * a json select structure of the form ``{"select": ["1", "2", "3"]}``

``host``        The website the spreadsheet page is from

``user``        The user who requested the page - when using the api this will
                always be the api public key used to request the page

``time``        The time in seconds from the start of the Unix epoch ie 1st
                January 1970

``path``        the path of the page being displayed

``row``         row attributed expressed as ranges in a 2 dimensional array. The
                3rd row is expressed as the range ``3:3`` in excel notation.

                The ``row`` attribute can contain the following values:

                ``fixedHeight`` - can be ``true`` or ``false``

                ``height`` - the height in pixels. The default height is 22px.
                The GUI allows heigts to be incremented in half cell (11px)
                steps.

``page``        contains the page attributes - by default an empty object.
                **Need a note about custom attributes in writing to a
                spreadsheet**

``permissions`` a json structure that describes the permissions of the page.
                The ``champion`` view is the one shown on the undecorated url
                (ie ``http://example.com/some/page``) whereas the other view
                need decorated URL's
                (ie ``http://example.com/some/page/?view=webpage``). The
                champion can also be accessed via the appropriate decorated
                URL.

                Each view has two sets of permissions:

                ``everyone`` - if this is ``true`` the view is accessible to
                anonymous unauthenticated visitors.

                ``groups`` - a list of groups who have access to this view

                Groups should normally be used for user access. However
                usernames are email addresses - and every user is a member of
                a special group whose name is their email address.

=============== =======================================================================

The json that is returned has the following structure:

.. code-block:: javascript

    {
        "styles": {
            "1363370537898099": "text-align:right;",
            "1363370570251910": "font-weight:bold;font-size:180%;text-align:center;",
            "1363370522172244": "text-align:left;",
            "1363370555762121": "font-weight:bold;text-align:right;",
            "1363370565184572": "font-weight:bold;text-align:center;",
            "1363370564006424": "text-align:center;",
            "1363370575746143": "font-weight:bold;text-align:left;",
            "1363370590083320": "color:#FF050D;font-weight:bold;text-align:right;",
            "1363370578236282": "font-weight:bold;font-style:italic;text-align:left;",
            "1363370590083418": "color:#FF050D;background-color:#FFF;font-weight:bold;text-align:right;"
        },
        "views": [],
        "column": {
            "1": {
                "1": {
                    "width": 100
                }
            }
        },
        "object": "page",
        "cell": {
            "1": {
                "3": {
                    "__rawvalue": "bleh",
                    "style": 1363370570251910,
                    "overwrite-color": "auto",
                    "value": "Feb",
                    "formula": "Feb"
                },
                "2": {
                    "__rawvalue": "bleh",
                    "style": 1363370570251910,
                    "overwrite-color": "auto",
                    "value": "Jan",
                    "formula": "Jan"
                }
            },
            "3": {
                "1": {
                    "__rawvalue": "bleh",
                    "style": 1363370575746143,
                    "overwrite-color": "auto",
                    "value": "Expenditure",
                    "formula": "Expenditure"
                },
                "3": {
                    "__rawvalue": "bleh",
                    "style": 1363370537898099,
                    "format": "###,0;(#,##0,0)",
                    "value": "1,300",
                    "formula": "1300",
                    "overwrite-color": "auto"
                },
                "2": {
                    "__rawvalue": "bleh",
                    "style": 1363370537898099,
                    "format": "###,0;(#,##0,0)",
                    "value": "900",
                    "formula": "900",
                    "overwrite-color": "auto"
                }
            },
            "2": {
                "1": {
                    "__rawvalue": "bleh",
                    "style": 1363370575746143,
                    "overwrite-color": "auto",
                    "value": "Income",
                    "formula": "Income"
                },
                "3": {
                    "__rawvalue": "bleh",
                    "style": 1363370537898099,
                    "format": "###,0;(#,##0,0)",
                    "value": "1,200",
                    "formula": "1200",
                    "overwrite-color": "auto"
                },
                "2": {
                    "__rawvalue": "bleh",
                    "style": 1363370537898099,
                    "format": "###,0;(#,##0,0)",
                    "value": "1,200",
                    "formula": "1200",
                    "overwrite-color": "auto"
                }
            },
            "4": {
                "1": {
                    "__rawvalue": "bleh",
                    "style": 1363370578236282,
                    "overwrite-color": "auto",
                    "value": "Difference",
                    "formula": "Difference"
                },
                "3": {
                    "__rawvalue": "bleh",
                    "style": 1363370590083418,
                    "format": "###,0;(#,##0,0)",
                    "value": "(100)",
                    "formula": "=C2-C3",
                    "overwrite-color": "auto"
                },
                "2": {
                    "__rawvalue": "bleh",
                    "style": 1363370555762121,
                    "format": "###,0;(#,##0,0)",
                    "value": "300",
                    "formula": "=B2-B3",
                    "overwrite-color": "auto"
                }
            },
        },
        "host": "http://example.com",
        "user": "api public key: Y2345678123456781234567812345678",
        "time": 1363377914027330,
        "path": "/some/page/",
        "row": {
            "1": {
                "1": {
                    "fixedHeight": true,
                    "height": 33
                }
            }
        },
        "page": {},
        "permissions": {
            "challenger": [],
            "champion": "spreadsheet",
            "views": {
                "webpage": {
                    "everyone": false,
                    "groups": [
                        "admin"
                    ]
                },
                "table": {
                    "everyone": false,
                    "groups": [
                        "admin"
                    ]
                },
                "spreadsheet": {
                    "everyone": false,
                    "groups": [
                        "admin"
                    ]
                },
                "wikipage": {
                    "everyone": false,
                    "groups": [
                        "admin"
                    ]
                }
            }
        }
    }


.. _ghost cell: http://documentation.vixo.com/contents/vixo-overview/making-forms.html

.. _wiki view: http://documentation.vixo.com/contents/vixo-overview/web-and-wikipages.html
