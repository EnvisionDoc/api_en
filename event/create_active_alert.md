# Create Active Alert

Create an active alert. Except for the mandatory fields, there is no need to verify the legality of other parameters. The parameters used by users such as `contentId` will not be maintained on the EnOS platform.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=create
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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_


## Request Parameters (Body)


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - activeAlert
     - Mandatory
     - ActiveAlert Struct
     - The details of an active alert. For more information of an activeAlert struct, see `ActiveAlert Struct>> <create_active_alert#activealert-struct-activelert>`__


### ActiveAlert Struct<activealert>

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
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__
   * - modelId
     - Mandatory
     - String
     - The model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - modelIdPath
     - Optional
     - String
     - The model ID path.
   * - measurepointId
     - Optional
     - String
     - The measurement point ID. You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. `How to get pointId>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measuremet-point-pointid-pointid>`__
   * - deviceStatus
     - Optional
     - String
     - The device status, such as "offline". You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. For more information, see `Setting State-based Alerts>> </docs/device-connection/en/2.1.0/howto/alert/setting_state_based_alert>`__
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
     - The local time when the alert occurs. For time formats, see `Data and Time Formats Used by Localtime>> </docs/api/en/2.1.0/api_faqs.html#date-and-time-format-adopted-by-localtime>`__
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
     - Specify the alert type's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__.
   * - subTypeId
     - Optional
     - String
     - The alert sub-type ID.
   * - subTypeDesc
     - Optional
     - StringI18n
     - Specify the alert sub-type's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__.
   * - contentId
     - Optional
     - String
     - The alert content ID.
   * - contentDesc
     - Optional
     - StringI18n
     - Specify the alert content's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__.
   * - tags
     - Optional
     - Map
     - The user-defined tags. (The Key and Value are of String type.) For details, see `How to use tags </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`__.


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
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=create&orgId=yourOrgId
method: POST 
requestBody: 
{
  "activeAlert": {
	 "assetId": "qu5TmJRj",
	 "modelId": "Inverter_Model",
	 "modelIdPath": "/Inverter_Model",
	 "measurepointId": "power",
	 "value": "3.5559796405967736",
	 "occurTime": 1559304899404,
	 "localOccurTime": "2019-06-01 02:14:59",
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

### Return Sample

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
package com.envisioniot.enos.event_service;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.event_service.v2_1.*;
import com.envisioniot.enos.event_service.vo.*;
import com.google.common.collect.Lists;
import com.google.gson.Gson;
import org.junit.Test;


import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;

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

public void testCreateActiveAlert() {
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";
    String orgId = "yourOrgId";
    String url = "https://{apigw-address}";
    CreateActiveAlertRequest request = new CreateActiveAlertRequest();
    request.setOrgId(orgId);
    GenerateActiveAlert activeAlert = buildActiveAlert();
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    activeAlert.setTag(tags);
    request.setActiveAlert(activeAlert);
    try {
        CreateActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, CreateActiveAlertResponse.class);

        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
