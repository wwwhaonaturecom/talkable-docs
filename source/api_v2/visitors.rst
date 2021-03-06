.. _api_v2/visitors:
.. include:: /partials/common.rst

Visitors
========

This API allows you to create visitors. See examples below.

|br|

.. code-block:: text

   POST /visitors

.. container:: ptable

   ================= ========================================================
   Parameter         Description
   ================= ========================================================
   data              Hash or JSON object with following properties:

                     * uuid - UUID of new visitor that will be created
   ================= ========================================================

Example
-------

Create a visitor
................

.. code-block:: javascript

   {
     "data": {
       "uuid": "b3967d36-4e7f-46bc-92b3-57344347cd6a"
     }
   }
