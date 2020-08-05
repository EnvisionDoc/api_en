# Update Alert Rule

Update an alert rule. Any parameter (that is not null) included the request body can be updated. 

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)               |
|isPatchUpdate|Query|Mandatory|Boolean|<ul><li>true (default) = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.</li><li>false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.</li></ul> |


## Request Parameters (Body)

.. note:: You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert.


|Name| Mandatory/Optional | Data type | Description |
|------|-----------------|-----------|-------------|
| ruleId         | Mandatory| String| The alert rule ID. |
| ruleDesc       | Mandatory| StringI18n| Specify the alert rule's description in its respective locale's language. For more details on the structure and locales supported, see [Internationalized name struct](/docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct)|
| modelId| Mandatory| String| The model ID. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid)|
| measurepointId | Optional         | String       | The measurement point ID. You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. [How to get pointId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-the-measuremet-point-pointid-pointid) |
| deviceStatus     | Optional         | String       | The device status, such as "offline". You must specify either ``measurepointId`` or ``deviceStatus`` as the trigger of the alert. See [Setting State-based Alerts](/docs/device-connection/en/2.1.0/howto/alert/setting_state_based_alert). |
| condition      | Mandatory| String| The query expression. For example, "${temperature} = 19" indicates that the value of the measurement point "temperature" is 19. A slash "/" is used to express the hierarchical relationship, for which only one downward layer is supported now. For example, “${pointA/att1} = 18” indicates the "att1" attribute value of the measurement point "A" is 18. [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression) |
| severityId     | Mandatory| String| The alert severity ID.|
| contentId      | Mandatory| String| The alert content ID.|
| tags           | Optional| Map| The user-defined tags. (The Key and Value are of String type.) For details, see [How to use tags](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag)|
| scope          | Mandatory         | Array of Scope Structs | Uses the scope struct to indicate the scope of the asset to which the alert applies to. For details, see [AssetNode struct](search_active_alerts#scope). |
| isEnabled      | Optional| Boolean| <ul><li>true (default) = enables the alert rule</li><li>false = does not enable the alert rule</li></ul>|
| triggeringDelayTimer | Optional | Integer | The amount of time to delay triggering the alert. The unit is seconds with a range between [60 - 10800]. The alert will only be triggered when an anomaly that matches the alert rule occurs and does not return to normal within the set time. To trigger the alert immediately, set the time to 0. For more information, see [Tutorial: Setting Alert Triggering Delay Timer](/docs/device-connection/en/2.1.0/howto/alert/setting_alert_triggering_delay_timer.html).|

### AssetNode Struct <assetnode>

| Name | Required or Not | Data Type | Description |
|----------|--------------|--------------|----------|
| treeId   | true         | String       | The asset tree ID. If it is set as "all", it indicates that this is a special node, standing for the globality of the organization.  |
| assetId  | true         | String       | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid)  |



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-rules?action=update&orgId=yourOrgId&isPatchUpdate=false
method: POST 
requestBody: 
{
	"alertRule": {
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
		"scope": [{
			"treeId": "ptde66nd",
			"assetId": "FbFy8qyz"
		}],
		"isEenabled": true,
		"triggeringDelayTimer": 120
     }
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": null
}
```

### Java SDK Sample

```java
public void testUpdateAlertRule() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    UpdateAlertRuleRequest request = new UpdateAlertRuleRequest();
    request.setOrgId(orgId);
    request.setRuleId("yourRuleID");
    Map < String, String > map = new HashMap < > ();
    map.put("yourTagKey", "yourTagValue");
    request.setTags(map);
    request.setIsPatchUpdate(true);
    try {
        UpdateAlertRuleResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, UpdateAlertRuleResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
