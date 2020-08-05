# Deprecations and Removals

## Common File Service

Starting from EnOS 2.1 Release, EnOS stops providing and supporting the Common File Service APIs.

## Model Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - What's deprecated or removed
   * - `Search Thing Model <../model/searchmodel>`_
     - ``callType`` in ``ThingService`` struct in the response is deprecated and will be removed in a future version.


## Asset Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - What's deprecated or removed
   * - `Update Asset <../asset/update_asset>`_
     - ``modelId`` in ``AssetUpdate`` struct in the request parameter (body) is removed.

### Batch Processing Service

.. list-table::
   :widths: 40 20 40
   :header-rows: 1

   * - Items
     - What's deprecated or removed
     - Impact
   * - The ``appId`` field in request parameters, response parameters, request sample, and return sample
     - Removed the ``appId`` field
     - Import Flow，Export Flow，Get Flow，Load Flow For Edit，Get Flow Instance，List Flow Instances
   * - The ``alertTo`` field in request parameters, response parameters, request sample, and return sample
     - Removed the ``alertTo`` field
     - Import Flow，Export Flow，Get Flow，Load Flow For Edit，Get Flow Instance，List Flow Instances
   * - The ``waitCode`` field in request parameters, response parameters, request sample, and return sample
     - Removed the ``waitCode`` field
     - Import Flow，Export Flow

<!--end-->
