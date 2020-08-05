# Create History Alerts in Batch

Batch create history alerts. 

.. note:: As long as one alert fails the format verification, all alerts cannot be created.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=batchCreate
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
   * - historyAlertList
     - true
     - Array of HistoryAlert Structs
     - The list of history alerts. For details of a historyAlert struct, see `HistoryAlert Struct <create_history_alerts_in_batch#historyalert-struct-historyalert>`__ 



### HistoryAlert Struct <historyalert>


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
     - The device status, such as "offline". You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. For more information, see `Setting State-based Alerts </docs/device-connection/en/2.1.0/howto/alert/setting_state_based_alert>`__
   * - value
     - Mandatory
     - Object
     - The measurement point value.
   * - occurTime
     - Mandatory
     - Long
     - The UTC time when the alert occurs. For time formats, see `ISO8601 Standard Time Formats Used by UTC </docs/api/en/2.1.0/api_faqs.html#iso8601-standard-time-format-adopted-by-utc-time>`__ 
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
   * - data
     - Array of EnosBatchEachData Structs
     - The list of success or failure messages. For the details of an enosBatchEachData struct, see the table below.



### EnosBatchEachData Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - code
     - Integer
     - Failed or succeeded to create one alert: 0: succeeded, -1: failed
   * - msg
     - String
     - The message indicating whether the format is correct or wrong.
   * - data
     - String
     -  If successful, it will return the ``eventId``, otherwise, it will return an error message.





## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/history-alerts?action=batchCreate&orgId=yourOrgId
method: POST 
requestBody:
{
    "historyAlertList": [{
        "assetId": "asset",
        "contentDesc": {
            "defaultValue": "default2",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "contentId": "content",
        "localOccurTime": "2019-11-07 15:36:32",
        "localRecoverTime": "2019-11-18 00:00:00",
        "measurepointId": "point111",
        "modelId": "model",
        "modelIdPath": "/path-path-path",
        "occurTime": 1573025793008,
        "orgId": "yourOrgId",
        "recoverTime": 1573112193008,
        "severityDesc": {
            "defaultValue": "default",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "severityId": "severity",
        "tag": {
            "key1": " v1 "
        },
        "typeDesc": {
            "defaultValue": "default1",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "typeId": "type",
        "value": 1.0
    },
    {
        "assetId": "asset",
        "contentDesc": {
            "defaultValue": "default2",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "contentId": "content",
        "localOccurTime": "2019-11-07 15:36:33",
        "localRecoverTime": "2019-11-18 00:00:00",
        "measurepointId": "point111",
        "modelId": "model",
        "modelIdPath": "/path-path-path",
        "occurTime": 1573112193008,
        "orgId": "yourOrgId",
        "severityDesc": {
            "defaultValue": "default",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "severityId": "severity",
        "tag": {
            "key2": " v2 "
        },
        "typeDesc": {
            "defaultValue": "default1",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "typeId": "type",
        "value": 1.0
    },
    {
        "assetId": "asset",
        "contentDesc": {
            "defaultValue": "default2",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "contentId": "content",
        "localOccurTime": "2019-11-07 15:36:33",
        "localRecoverTime": "2019-11-18 00:00:00",
        "measurepointId": "point111",
        "modelId": "model",
        "modelIdPath": "/path-path-path",
        "occurTime": 1573112193012,
        "orgId": "yourOrgId",
        "recoverTime": 1573112193016,
        "severityDesc": {
            "defaultValue": "default",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "severityId": "severity",
        "tag": {
            "key3": " v3 "
        },
        "typeDesc": {
            "defaultValue": "default1",
            "i18nValue": {
                "en_US": "english",
                "zh_CN": "中文"
            }
        },
        "typeId": "type",
        "value": 1.0
    }],
    "action": "batchCreate"
}
```

### Return Sample

```json
{
    "code": 99206,
    "msg": "Partial Content Success",
    "requestId": "de9281bf-3ebf-4783-97c8-4b94be384351",
    "data": [{
        "code": 0,
        "msg": "format right",
        "data": "2019110630b8cc38735e8ba9d1b3a6b5e4381e36"
    },
    {
        "code": -1,
        "msg": "format wrong",
        "data": "recoverTime  :parameter empty"
    },
    {
        "code": 0,
        "msg": "format right",
        "data": "20191107bd6ab07f9be6ab769b1e7c898b40cc83"
    }],
    "successSize": 2,
    "totalSize": 3
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

private GenerateHistoryAlert buildHistoryAlert() {
    GenerateActiveAlert activeAlert = buildActiveAlert();
    Gson gson = new Gson();
    GenerateHistoryAlert historyAlert = gson.fromJson(gson.toJson(activeAlert), GenerateHistoryAlert.class);
    historyAlert.setRecoverTime(System.currentTimeMillis());
    historyAlert.setLocalRecoverTime("2019-11-18 00:00:00");
    return historyAlert;
}

public void testBatchCreateHistoryAlert() {
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";
    String orgId = "yourOrgId";
    String url = "https://{apigw-address}";
    BatchCreateHistoryAlertsRequest request = new BatchCreateHistoryAlertsRequest();
    request.setOrgId(orgId);
    List < GenerateHistoryAlert > list = Lists.newArrayList();
    GenerateHistoryAlert historyAlert1 = buildHistoryAlert();
    historyAlert1.setOccurTime(System.currentTimeMillis() - 24L * 3600 * 1000);
    Map < String, String > tags = new HashMap < > ();
    tags.put("key1", "v1");
    historyAlert1.setTag(tags);
    list.add(historyAlert1);
    GenerateHistoryAlert historyAlert2 = buildHistoryAlert();
    tags = new HashMap < > ();
    tags.put("key2", "v2");
    historyAlert2.setTag(tags);
    list.add(historyAlert2);
    GenerateHistoryAlert historyAlert3 = buildHistoryAlert();
    tags = new HashMap < > ();
    tags.put("key3", "v3");
    historyAlert3.setTag(tags);
    list.add(historyAlert3);
    request.setHistoryAlertList(list);
    try {
        BatchCreateHistoryAlertsResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, BatchCreateHistoryAlertsResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```