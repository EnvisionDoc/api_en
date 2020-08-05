# Create History Alert

Create a new history alert. Except for the mandatory fields, there is no need to verify the legality of other parameters. The parameters used by users such as `contentId` would not be maintained on the EnOS platform. Alerts with the same `assetId`, `measurepointId`, and `occurTime` will be updated.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=create
```

## Request Parameters (URI)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__



## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - historyAlertList
     - Mandatory
     - HistoryAlert Struct
     - The details of the history alert. For more information, see `HistoryAlert Struct <create_history_alert#historyalert-struct-historyalert>`_




### HistoryAlert Struct<historyalert>

.. note:: You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert.


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - assetId
     - Mandatory
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - modelId
     - Mandatory
     - String
     - The model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`_
   * - modelIdPath
     - Optional
     - String
     - The model ID path.
   * - measurepointId
     - Optional
     - String
     - The measurement point ID. You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. `How to get pointId>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measuremet-point-pointid-pointid>`_
   * - deviceStatus
     - Optional
     - String
     - The device status, such as "offline". You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. For more details, see `Setting State-based Alerts>> </docs/device-connection/en/2.1.0/howto/alert/setting_state_based_alert>`__
   * - value
     - Mandatory
     - Object
     - The measurement point value.
   * - occurTime
     - Mandatory
     - Long
     - The UTC time when the alert occurs. For time formats, see `ISO8601 Standard Time Formats Used by UTC>> </docs/api/en/2.1.0/api_faqs.html#iso8601-standard-time-format-adopted-by-utc-time>`__
   * - localOccurTime
     - Optional
     - String
     - The local time when the alert occurs. For time formats, see `Data and Time Formats Used by Localtime </docs/api/en/2.1.0/api_faqs.html#date-and-time-format-adopted-by-localtime>`__
   * - recoverTime
     - Mandatory
     - Long
     - The recovery time in UTC format. For time formats, see `ISO8601 Standard Time Formats Used by UTC </docs/api/en/2.1.0/api_faqs.html#iso8601-standard-time-format-adopted-by-utc-time>`__
   * - localRecoverTime
     - Optional
     - String
     - The recovery time in local format. For time formats, see `Data and Time Formats Used by Localtime </docs/api/en/2.1.0/api_faqs.html#date-and-time-format-adopted-by-localtime>`__
   * - recoverReason
     - Optional
     - String
     - The recovery reason.
   * - severityId
     - Optional
     - String
     - The alert severity ID.
   * - severityDesc
     - Optional
     - StringI18n
     - Specify the alert severity's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - typeId
     - Optional
     - String
     - The alert type ID.
   * - typeDesc
     - Optional
     - StringI18n
     - Specify the alert type's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - subTypeId
     - Optional
     - String
     - The alert sub-type ID.
   * - subTypeDesc
     - Optional
     - StringI18n
     - Specify the alert sub-type's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - contentId
     - Optional
     - String
     - The alert content ID.
   * - contentDesc
     - Optional
     - StringI18n
     - Specify the alert content's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tags </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`__


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - eventId
     - String
     - The alert ID.


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/history-alerts?action=create&orgId=yourOrgId
method: POST 
requestBody: 
{
  "historyAlert": {
	 "assetId": "qu5TmJRj",
	 "modelId": "Inverter_Model",
	 "modelIdPath": "/Inverter_Model",
	 "measurepointId": "power",
	 "value": "3.5559796405967736",
	 "occurTime": 1559304899404,
	 "localOccurTime": "2019-06-01 02:14:59",
	 "recoverTime": 1559304900404,
	 "localRecoverTime": "2019-06-01 12:14:59",
	 "severityId": "alert_001",
	 "severityDesc": {
     "defaultValue": "Warn",
		 "i18nValue": {
			 "en_US": "alert",
			 "zh_CN": "alert"
		 }
	 },
	 "typeId": "errorType",
	 "typeDesc": {
     "defaultValue": "Warn",
		 "i18nValue": {
			 "en_US": "login failed",
			 "zh_CN": "登录失败"
		 }
	 },
	 "contentId": "planetTemperature",
	 "contentDesc": {
     "defaultValue": "the temperature is too high",
		 "i18nValue": {
			 "en_US": "the temperature is too high",
			 "zh_CN": "温度过高"
		 }
	 },
	 "tags": {
		 "Tag666": "63253w532",
		 "Tag888": "63253w532888",
		 "Tag": "1111"
	 }
  },
  "action": "create"
}
```

### Return sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"eventId": "20191101479fb7810c81a0cfe08f3552db40e546"
}
```

### Java SDK Sample

```java
private GenerateActiveAlert buildActiveAlert() {
    GenerateActiveAlert activeAlert = new GenerateActiveAlert();
    activeAlert.setAssetId("asset");
    activeAlert.setModelId("model");
    activeAlert.setModelIdPath("/path-path-path");
    activeAlert.setMeasurepointId("point111");
    activeAlert.setValue(1);
    long now = System.currentTimeMillis();
    activeAlert.setOccurTime(now);
    DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    String localTime = df.format(now);
    activeAlert.setLocalOccurTime(localTime);
    activeAlert.setSeverityId("severity");

    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文");
    map.put("en_US", "english");
    desc.setI18nValue(map);

    activeAlert.setSeverityDesc(desc);

    activeAlert.setTypeId("type");
    StringI18n desc1 = new StringI18n();
    desc1.setDefaultValue("default1");
    Map < String, String > map1 = new HashMap < > ();
    map1.put("zh_CN", "中文");
    map1.put("en_US", "english");
    desc1.setI18nValue(map1);

    activeAlert.setTypeDesc(desc1);

    activeAlert.setContentId("content");

    StringI18n desc2 = new StringI18n();
    desc2.setDefaultValue("default2");
    Map < String, String > map2 = new HashMap < > ();
    map2.put("zh_CN", "中文");
    map2.put("en_US", "english");
    desc2.setI18nValue(map2);
    activeAlert.setContentDesc(desc2);
    return activeAlert;
}
private GenerateHistoryAlert buildHistoryAlert() {
    GenerateActiveAlert activeAlert = buildActiveAlert();
    Gson gson = new Gson();
    GenerateHistoryAlert historyAlert = gson.fromJson(gson.toJson(activeAlert), GenerateHistoryAlert.class);
    historyAlert.setRecoverTime(System.currentTimeMillis());
    historyAlert.setLocalRecoverTime("2019-11-18 00:00:00");
    return historyAlert;
}

public void testCreateHistoryAlert() {
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";
    String orgId = "yourOrgId";
    String url = "https://{apigw-address}";
    CreateHistoryAlertRequest request = new CreateHistoryAlertRequest();
    GenerateHistoryAlert historyAlert = new GenerateHistoryAlert();
    historyAlert.setAssetId("yourAssetId");
    historyAlert.setModelId("yourModelId");
    historyAlert.setModelIdPath("yourModelIdPath");
    historyAlert.setMeasurepointId("yourMeasurementPointId");
    historyAlert.setValue(1);
    historyAlert.setOccurTime(System.currentTimeMillis());
    historyAlert.setLocalOccurTime("2019-08-08 00:00:00");
    historyAlert.setSeverityId("yourSeverityId");
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文");
    map.put("en_US", "english");
    desc.setI18nValue(map);
    historyAlert.setSeverityDesc(desc);
    historyAlert.setTypeId("yourTypeId");
    StringI18n desc1 = new StringI18n();
    desc1.setDefaultValue("default1");
    Map < String, String > map1 = new HashMap < > ();
    map1.put("zh_CN", "中文");
    map1.put("en_US", "english");
    desc1.setI18nValue(map1);
    historyAlert.setTypeDesc(desc1);
    historyAlert.setContentId("yourContentId");
    StringI18n desc2 = new StringI18n();
    desc2.setDefaultValue("default2");
    Map < String, String > map2 = new HashMap < > ();
    map2.put("zh_CN", "中文");
    map2.put("en_US", "english");
    desc2.setI18nValue(map2);
    historyAlert.setContentDesc(desc2);
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    historyAlert.setTag(tags);
    historyAlert.setRecoverTime(System.currentTimeMillis());
    historyAlert.setRecoverReason("reason");
    historyAlert.setLocalRecoverTime("2019-07-18 00:00:00");
    request.setHistoryAlert(historyAlert);
    request.setOrgId(orgId);
    try {
        CreateHistoryAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, CreateHistoryAlertResponse.class);

        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```