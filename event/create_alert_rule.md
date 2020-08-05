# Create Alert Rule

Create an alert rule.


## Prerequisites

- Ensure that the specified model (``modelId``) is available under the organization.
- Ensure that the specified measuring point (``measurepointId``) is valid.
- Ensure that the specified alert severity (``severityId``) exists.
- Ensure that the specified alert content (``contentId``) exists.
- Ensure that the specified scope (``scope``) of asset nodes where the rule takes effect exists.  

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=create
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

.. note:: You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert.

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - ruleId
     - Mandatory
     - String
     - The alert rule ID.
   * - ruleDesc
     - Mandatory
     - StringI18n
     - Specify the alert rule's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - modelId
     - Mandatory
     - String
     - The model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`_
   * - measurepointId
     - Optional
     - String
     - The measurement point ID. You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. `How to get pointId>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`_
   * - deviceStatus
     - Optional
     - String
     - The device status, such as "offline". You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. For more details, see `Setting State-based Alerts>> </docs/device-connection/en/2.1.0/howto/alert/setting_state_based_alert>`_
   * - condition
     - Mandatory
     - String
     - The query expression. For example, "${temperature} = 19" indicates that the value of the measurement point "temperature" is 19. A slash "/" is used to express the hierarchical relationship, for which only one downward layer is supported for now. For example, “${pointA/att1} = 18” indicates the "att1" attribute value of the measurement point "A" is 18. `How to use expression>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`_
   * - severityId
     - Mandatory
     - String
     - The alert severity ID.
   * - contentId
     - Mandatory
     - String
     - The alert content ID.
   * - tags
     - Optional
     - Map
     - The user-defined tags. (The Key and Value are of String type.) For details, see [How to use tags](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag).
   * - isEnabled
     - Optional
     - Boolean
     - + true (default) = enables the alert rule
       + false = does not enable the alert rule
   * - isRoot
     - Optional
     - Boolean
     - + true = a root alert
       + false (default) = not a root alert
   * - scope
     - Mandatory
     - Array of Scope Structs
     - Uses the AssetNode struct to indicate the scope of the asset to which the alert applies to. For details, see `Scope Struct>> <search_active_alerts#scope>`_
   * - triggeringDelayTimer
     - Optional
     - Integer
     - The amount of time to delay triggering the alert. The unit is seconds with a range between [60 - 10800]. The alert will only be triggered when an anomaly that matches the alert rule occurs and does not return to normal within the set time. To trigger the alert immediately, set the time to 0. For more information, see `Tutorial: Setting Alert Triggering Delay Timer>> </docs/device-connection/en/2.1.0/howto/alert/setting_alert_triggering_delay_timer.html>`_



### AssetNode Struct<assetnode>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - treeId
     - Mandatory
     - String
     - The asset tree ID. Alternatively, you can set it as "all" to include all the asset trees in the specified ``orgID``.
   * - assetId
     - Mandatory
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_




## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - The rule ID.


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-rules?action=create&orgId=yourOrgId
method: POST 
requestBody: 
{
    "ruleId": "user BID",
    "ruleDesc": {
        "defaultValue": "Grid is connected from converter",
        "i18nValue": {
            "en_US": "Grid is connected from converter",
            "zh_CN": "电网由变频器连接"
        }
    },
    "modelId": "EnOS_Solar_CombinerBox",
    "measurepointId": "CBX.BranchStateAttr",
    "condition": "${CBX.BranchStateAttr} = 18",
    "severityId": "WARN",
    "contentId": "planetTemperature",
    "tags": {
        "key1": "v1"
    },
    "orgId": "yourOrgId",
    "scope": [{
        "treeId": "ptde66nd",
        "assetId": "FbFy8qyz"
    }],
    "isEnabled": true,
    "isRoot": true,
    "triggeringDelayTimer": 120
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
    "data": "user BID"
}
```

### Java SDK Sample

```java
public void testCreateAlertRule() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    CreateAlertRuleRequest request = new CreateAlertRuleRequest();
    request.setOrgId(orgId);
    request.setRuleId("yourRuleId");
    request.setTriggeringDelayTimer(86400);
    request.setSeverityId("yourSeverityId");
    request.setContentId("yourContentId");
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("hah");
    Map < String, String > mapString = new HashMap < > ();
    mapString.put("zh_CN", "中文");
    mapString.put("en_US", "english");
    desc.setI18nValue(mapString);
    request.setRuleDesc(desc);
    request.setModelId("yourModelId");
    request.setMeasurepointId("int1");
    request.setCondition("(${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117) and  (${int1} = 1117)");
    Map < String, String > map = new HashMap < > ();
    map.put("yourTagKey", "yourTagValue");
    request.setTags(map);
    request.setIsEnabled(true);
    request.setIsRoot(false);
    AssetNode assetNode = new AssetNode();
    assetNode.setAssetId("all");
    assetNode.setTreeId("all");
    List < AssetNode > list = new LinkedList < > ();
    list.add(assetNode);
    request.setScope(list);
    try {
        CreateAlertRuleResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url(url)
            .getResponse(request, CreateAlertRuleResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```