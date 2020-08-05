# Changed APIs

<br />

EnOS 2.1 Release introduces the following API behavioral changes.

## Model Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Get Thing Model <../../model/getmodel>`__
     - In the following objects in ``data`` object in the response, added new fields ``isStdElement`` and ``stdElementId``.

       + ThingEvent
       + ThingService
       + ThingMeasurepoint
       + ThingAttribute
       + ThingDatapoint

   * - `Search Thing Model <../../model/searchmodel>`__
     - In the following objects in ``data`` object in the response, added new fields ``isStdElement`` and ``stdElementId``.

       + ThingEvent
       + ThingService
       + ThingMeasurepoint
       + ThingAttribute
       + ThingDatapoint

   * - `Search Thing Model <../../model/searchmodel>`__
     - The field ``tags`` in the ``expression`` supports arithmetic operators "exists" and "not exists".


## Connection Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Search Device <../../connect/search_device>`__
     - A new field ``deviceTags`` is supported in ``expression``.
   * - `Search Product <../../connect/search_product>`__
     - A new field ``deviceTags`` is supported in ``expression``.
   * - `Get Device <../../connect/get_device>`__
     - 4 new parameters are supported in Device struct to indicates the latest time when a device was updated: ``measurepointLastUpdate``, ``eventLastUpdate``, ``attributeLastUpdate`` and ``featureLastUpdate``.
   * - `Create Product <../../connect/create_product.html>`__
     - 2 new optional parameters: ``dynamicActivateEnabled`` and ``productTags`` are supported in request body.

       + ``dynamicActivateEnabled``: indicate whether to activate the product dynamically
       + ``productTags``: indicate the product tags

   * - `Update Product <../../connect/update_product.html>`__
     - A new optional parameter ``productTags`` is supported in request body, which indicates the product tags.


## Asset Tree Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Search Asset Node <../../asset_tree/search_asset_node>`__
     - In request body, use ``expression`` parameter to replace previous parameter ``filter``.

## Alert Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Create Active Alert <../../event/create_active_alert>`__
     - A new field ``deviceStatus`` is returned in ``ActiveAlert`` struct to indicate the device status.
   * - `Create Alert Rule <../../event/create_alert_rule>`__
     - A new parameter ``deviceStatus`` is supported in the request body.
   * - `Create History Alert <../../event/create_history_alert>`__
     - A new field ``deviceStatus`` is returned in ``HistoryAlert`` struct to indicate the device status.
   * - `Search Active Alert <../../event/search_active_alerts>`__
     - + New fields ``deviceStatus`` and ``assetPath`` are supported in the ``expression`` parameter of the request body.
       + The field ``tag`` in the ``expression`` supports arithmetic operators "exists" and "not exists".
       + The response parameter ``value`` in the ``ActiveAlert`` struct supports recording the measurement point value when ``triggeringDelayTimer`` starts counting.
   * - `Search Alert Rule <../../event/search_alert_rule>`__
     - + A new parameter ``deviceStatus`` is supported in the request body.
       + New field ``deviceStatus`` is supported in the ``expression`` parameter of the request body. The supported syntax is !=.
       + A new field ``deviceStatus`` is returned in the response body.
       + A new parameter ``triggeringDelayTimer`` is supported in ``AlertRule`` struct to indicate the time of delaying the alert triggering.
   * - `Search History Alert <../../event/search_history_alerts>`__
     - + New fields ``deviceStatus`` and ``assetPath`` are supported in the ``expression`` parameter of the request body.
       + A new field ``deviceStatus`` is returned in the response body.
       + The field ``tag`` in the ``expression`` supports arithmetic operators "exists" and "not exists".
       + The function is changed to query historical alarms in the **last three months**.
       + The response parameter ``value`` in the ``HistoryAlert`` struct supports recording the measurement point value when ``triggeringDelayTimer`` starts counting.
   * - `Aggregate Active Alerts <../../event/aggregate_active_alerts>`__
     - The field ``tag`` in the ``expression`` supports arithmetic operators "exists" and "not exists".
   * - `Create Alert Content <../../event/create_alert_content>`__
     - + The parameter ``source`` is removed from request body.
       + The data type of response parameter ``data`` changes to "String" from previous "null".
       + A new parameter ``source`` is supported in request body to indicate the data source to which the alert content applies.
   * - `Create Alert Rule <../../event/create_alert_rule>`__
     - + The parameter ``source`` is removed from request body.
       + The data type of response parameter ``data`` changes to "String" from previous "null".
       + The parameter ``condition`` in the request body changes to query expression-like statement from expression.
       + A new parameter ``source`` is supported in request body to indicate the data source to which the alert rule applies.
       + A new parameter ``triggeringDelayTimer`` is supported in request body to indicate the time of delaying the alert triggering.
   * - `Create Alert Severity <../../event/create_alert_severity>`__
     - + The parameter ``source`` is removed from request body.
       + The data type of response parameter ``data`` changes to "String" from previous "null".
       + A new parameter ``source`` is supported in request body to indicate the data source to which the alert severity applies.
   * - `Create Alert Type <../../event/create_alert_type>`__
     - + The parameter ``source`` is removed from request body.
       + The data type of response parameter ``data`` changes to "String" from previous "null".
       + A new parameter ``source`` is supported in request body to indicate the data source to which the alert type applies.
   * - `Delete Alert Content <../../event/delete_alert_content>`__
     - + The parameter ``source`` is removed from request URI.
       + A new parameter ``source`` is supported in request URI to indicate the data source to which the alert content applies.
   * - `Delete Alert Rule <../../event/delete_alert_rule>`__
     - + The parameter ``source`` is removed from request URI.
       + A new parameter ``source`` is supported in request URI to indicate the data source to which the alert rule applies.
   * - `Delete Alert Severity <../../event/delete_alert_severity>`__
     - + The parameter ``source`` is removed from request URI.
       + A new parameter ``source`` is supported in request URI to indicate the data source to which the alert severity applies.
   * - `Delete Alert Type <../../event/delete_alert_type>`__
     - + The parameter ``source`` is removed from request URI.
       + A new parameter ``source`` is supported in request URI to indicate the data source to which the alert type applies.
   * - `Search Active Alerts <../../event/search_active_alerts>`__
     - + New fields ``deviceStatus`` and ``assetPath`` are supported in the ``expression`` parameter of the request body.
       + 2 optional parameters: ``scope`` and ``rootAlert`` are supported in request body.
   * - `Search Alert Content <../../event/search_alert_content>`__
     - + The parameter ``source`` is removed from the ``AlertContent`` struct.
       + A new parameter ``source`` is supported in ``AlertContent`` struct to indicate the data source to which the alert content applies.
   * - `Search Alert Rule <../../event/search_alert_rule>`__
     - + The parameter ``source`` is removed from the ``AlertRule`` struct.
       + A new parameter ``triggeringDelayTimer`` is supported in ``AlertRule`` struct to indicate the time of delaying the alert triggering.
   * - `Search Alert Severity <../../event/search_alert_severity>`__
     - + The parameter ``source`` is removed from the ``AlertSeverity`` struct.
       + A new parameter ``source`` is supported in ``AlertSeverity`` struct to indicate the data source to which the alert severity applies.
   * - `Search Alert Type <../../event/search_alert_type>`__
     - + The parameter ``source`` is removed from the ``AlertType`` struct.
       + A new parameter ``source`` is supported in ``AlertType`` struct to indicate the data source to which the alert type applies.
   * - `Search History Alerts <../../event/search_history_alerts>`__
     - + New fields ``deviceStatus`` and ``assetPath`` are supported in the ``expression`` parameter of the request body.
       + 2 optional parameters: ``scope`` and ``rootAlert`` are supported in request body.
   * - `Update Alert Content <../../event/update_alert_content>`__
     - + The parameter ``source`` is removed from the ``generateContent`` struct.
       + A new parameter ``source`` is supported in ``generateContent`` struct to indicate the data source to which the alert content applies.
   * - `Update Alert Rule <../../event/update_alert_rule>`__
     - + A new parameter ``deviceStatus`` is supported in the request body.
       + Parameters in the ``alertRule`` struct are moved to the request body.
       + The parameter ``source`` is removed from the ``alertRule`` struct.
       + The parameter ``condition`` in the request body changes to query expression-like statement from expression.
       + A new parameter ``source`` is supported in ``alertRule`` struct to indicate the data source to which the alert rule applies.
       + A new parameter ``triggeringDelayTimer`` is supported in ``alertRule`` struct to indicate the time of delaying the alert triggering.
   * - `Update Alert Severity <../../event/update_alert_severity>`__
     - + The parameter ``source`` is removed from the ``generateSeverity`` struct.
       + A new parameter ``source`` is supported in ``generateSeverity`` struct to indicate the data source to which the alert severity applies.
   * - `Update Alert Type <../../event/update_alert_type>`__
     - + Added constraint: If the alert type already has a parent alert type, the ``parentTypeId`` cannot be updated.
       + The parameter ``source`` is removed from the ``generateType`` struct.
       + A new parameter ``parentTypeId`` is supported in ``generateType`` struct to indicate the alert type ID of the parent alert.


## TSDB Data Service

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - API
     - Description
   * - `Filter Asset Latest Data <../../tsdb_service/filter_asset_latest_data>`__
     - Added support of the POST method.
   * - `Get Asset AI Data with Aggregation Logic <../../tsdb_service/get_asset_ai_data_with_aggregation_logic>`__
     - Added support of the POST method.
   * - `Get Asset AI Raw Data <../../tsdb_service/get_asset_ai_raw_data>`__
     - + Added support of the POST method.
       + A new parameter ``withQuality`` is supported in request URI to get the quality indicator.
   * - `Get Asset Current Day Electric Power <../../tsdb_service/get_asset_current_day_electric_power>`__
     - Added support of the POST method.
   * - `Get Asset DI Data <../../tsdb_service/get_asset_di_data>`__
     - + Added support of the POST method.
       + Interpolation is supported in getting the asset status (DI) data.
   * - `Get Asset DI Data Duration <../../tsdb_service/get_asset_di_data_durations>`__
     - Added support of the POST method.
   * - `Get Asset Electric Power Data <../../tsdb_service/get_asset_electric_power_data>`__
     - Added support of the POST method.
   * - `Get Asset Generic Data <../../tsdb_service/get_asset_generic_data>`__
     - + Added support of the POST method.
       + A new parameter ``withQuality`` is supported in request URI to get the quality indicator.
   * - `Get Asset Latest Data <../../tsdb_service/get_asset_latest_data>`__
     - Added support of the POST method.
   * - `Get Asset Raw Data By Time Range <../../tsdb_service/get_asset_raw_data_by_time_range>`__
     - + Added support of the POST method.
       + A new parameter ``orderBy`` is supported in the request URL, which can be used to sort the response results by a certain field.
       + A new parameter ``withQuality`` is supported in request URI to get the quality indicator.

## Other

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Item
     - Description
   * - `Token Authentication <../../token/index>`__
     - Added support of the token authentication function, which supports the security encryption of API calls with the mechanism of access token.

<!--end-->
