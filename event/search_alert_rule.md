# Search Alert Rule

Search for alert rules based on the search criteria.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)         |


## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId        | Optional         | String                | The model ID. |
| measurepointId | Optional         | String       | The measurement point ID. [How to get pointId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-the-measurement-point-id-pointid-pointid) |
| expression      | Optional         | String | The query expression, which supports sql-like query. The fields that are supported for query include: `ruleId`, `modelId`, `measurepointId`, and `deviceStatus`. The supported arithmetic operators are "=", "in", and "!=", and the logical operator is "and" and "or". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression) |
| pagination  | Optional  |Pagination Request Struct | Lists the paging requirements in a request. If not specified, the pagination size is 10. You can use `sorters` to sort the response based on `ruleId`, `modelId`, `measurepointId`, `deviceStatus`, and `orgId`. For more details, see [Pagination Request Struct](/docs/api/en/2.1.0/overview.html#pagination-request-struct). |



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Array of AlertRule Struct | The list of alert rule details. For more information, see [AlertRule Struct](search_alert_rule#alertrule-struct-alertrule). |


### AlertRule Struct <alertrule>

| Name |  Data Type | Description |
|----------------|--------------|-----------------------|
| orgId          | String    | The organization ID which the asset belongs to. |
| ruleId         | String                | The alert rule ID.|
| ruleDesc        | StringI18n            | The alert rule description.|
| modelId           | String                | The model ID.|
| measurepointId   | String                | The measurement point ID.|
| deviceStatus     | String       | The device status.|
| condition         | String                | The query expression. For example, "${temperature} = 19" indicates that the value of the measurement point "temperature" is 19. A slash "/" is used to express the hierarchical relationship, for which only one downward layer is supported now. For example, “${pointA/att1} = 18” indicates the "att1" attribute value of the measurement point "A" is 18. |
| isEnabled      | Boolean               | <ul><li>true = the alert rule is enabled</li><li>false = the alert rule is not enabled</li></ul> |
| severityId         | String                | The alert severity ID.|
| severityDesc     | StringI18n | The alert severity description.|
| contentId      | String                | The alert content ID.|
| contentDesc  |  StringI18n | The alert content description. |
| tags           | Map            | User-defined tags. (The Key and Value are of String type.)|
| isRoot           | Boolean| <ul><li>true = a root alert</li><li>false (default) = not a root alert</li></ul>|
| scope            | AssetNode struct | Uses the assetNode struct to indicate the scope of the asset to which the alert applies to. For more information, see [AssetNode Struct](search_alert_rule#assetnode-struct-assetnode).  |
| triggeringDelayTimer |Integer | The amount of time to delay triggering the alert. The unit is seconds with a range between [60 - 10800]. The alert will only be triggered when an anomaly that matches the alert rule occurs and does not return to normal within the set time. To trigger the alert immediately, set the time to 0. |


### AssetNode Struct <assetnode>

| Name | Required or Not | Data Type | Description |
|----------|--------------|--------------|----------|
| treeId   | true         | String       | The asset tree ID. When the response is "all", it includes all the asset trees in the specified ``orgID``. |
| assetId  | true         | String       | The asset ID.  |


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-rules?action=search&orgId=yourOrgId
method: POST 
requestBody: 
{
    "modelId": "EnOS_Solar_CombinerBox",
    "measurepointId": "CBX.BranchStateAttr"
}
```

### Return Sample

```json
{
    "pagination": {
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 2,
        "sortedBy": [{
            "field": "update_time",
            "order": "DESC"
        }]
    },
}

```

### Return Sample

```json
{    
    "code": 0,
    "msg": "OK",
    "requestId": "a9689b9f-0cb6-4e47-a41c-bd459b687309",
    "data": [{
        "orgId": "yourOrgId",
        "ruleId": "zh_model_struct",
        "ruleDesc": {
            "defaultValue": "Grid is connected from converter",
            "i18nValue": {
                "en_US": "Grid is connected from converter",
                "zh_CN": "电网由变频器连接"
            }
        },
        "modelId": "zh_model",
        "measurepointId": "aa",
        "condition": "aa = 18",
        "isEnabled": true,
        "severityId": "WARN",
        "severityDesc": {
            "defaultValue": "WARN"
        },
        "contentId": "planetTemperature",
        "contentDesc": {
            "defaultValue": "连接"
        },
        "typeId": "warning_Type",
        "typeDesc": {
            "defaultValue": "connected"
        },
        "tags": {
            "key1": "v1"
        },
        "isRoot": false,
        "scope": [{
            "treeId": "ptde66nd",
            "assetId": "FbFy8qyz"
        }]
    },{
        "orgId": "yourOrgId",
        "ruleId": "zh_model_struct2",
        "ruleDesc": {
            "defaultValue": "Grid is connected from converter",
            "i18nValue": {
                "en_US": "Grid is connected from converter",
                "zh_CN": "电网由变频器连接"
            }
        },
        "modelId": "zh_model",
        "measurepointId": "aa",
        "condition": "aa = 18",
        "isEnabled": true,
        "severityId": "WARN",
        "severityDesc": {
            "defaultValue": "WARN"
        },
        "contentId": "planetTemperature",
        "contentDesc": {
            "defaultValue": "连接"
        },
        "typeId": "warning_Type",
        "typeDesc": {
            "defaultValue": "connected"
        },
        "tags": {
            "key1": "v1"
        },
        "isRoot": false,
        "scope": [{
            "treeId": "ptde66nd",
            "assetId": "FbFy8qyz"
        }]
    }]
}
```

### Java SDK Sample

```java
public void testSearchAlertRule() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    SearchAlertRuleRequest request = new SearchAlertRuleRequest();
    request.setOrgId(orgId);
    request.setExpression("deviceStatus = 'offline'");
    try {
        SearchAlertRuleResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, SearchAlertRuleResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
