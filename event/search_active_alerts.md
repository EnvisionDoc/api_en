# Search Active Alerts

Search for active alerts based on the search criteria.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=search
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


| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | Optional    | String    | The model ID. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid)|
| assetId       | Optional     | String    | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| measurepointId     | Optional     | String    | The measurement point ID. [How to get pointId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)|
| startOccurTime | Optional    | String| The start time for triggering the alert. For more details, see [Time parameters used in API>>](/docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api)    |
| endOccurTime   | Optional    | String| The end time for triggering the alert. For more details, see [Time parameters used in API>>](/docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api) |
| expression         | Optional    | String   | The query expression, which supports sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId`, `tag`, ``deviceStatus`` and ``assetPath``. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". `tag` also supports arithmetic operator "exists" and "not exists". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)|
| scope |  Optional   | Scope Struct | Query the alerts in a specified asset tree or in an asset node on the asset tree, and specify whether to return the blocked derivative alerts. **This parameter cannot be applied with rootAlert**. For more details, see [Scope Struct](search_active_alerts#scope-struct-scope). |
|  rootAlert  |   Optional  | RootAlert Struct | Query the derivative alerts which are blocked by the specified root alert. **This parameter cannot be applied with scope**. For more details, see [RootAlert Struct](search_active_alerts#rootalert-struct-rootalert).|
| pagination  | Optional  |Pagination Request Struct | Lists the paging requirements in a request. If not specified, the pagination size is 10, sorted in descending order by `occurTime`. `sorters` is not supported to sort the response. For more details, see [Pagination Request Struct>>](/docs/api/en/2.1.0/overview.html#pagination-request-struct) |


### Scope Struct <scope>

| Name            | Mandatory/Optional | Data Type | Description |
|------------|--------------|--------------|-----------|
| treeId            | Mandatory         | String       |  The asset tree ID. |
| fromAssetId       | Optional        | String       | Return all alerts of and under the asset node of the specified asset ID. If not specified, the alerts of all the nodes in the specified ``treeID`` will be returned.|
| includeDerivative | Optional        | Boolean      | <ul><li>true = include the derivative alerts in the response</li><li>fales (default) = does not include the derivative alerts</li></ul>|



### RootAlert Struct <rootalert>

| Name            | Mandatory/Optional | Data Type | Description |
|-------------|--------------|--------------|------------|
| treeId      | Optional        | String       | The asset tree ID.   |
| rootAlertId | Mandatory         | String       | The root alert ID. |







## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Array of ActiveAlert Structs | A list of the active alerts returned. For details of an activeAlert struct, see [ActiveAlert Struct](/docs/api/en/2.1.0/event/search_active_alerts#activealert-struct-aa).|

### ActiveAlert Struct <aa>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| eventId        | String                | The alert ID.  |
| orgId          | String                | The organization ID which the asset belongs to. |
| assetId        | String                | The asset ID. |
| modelId        | String                | The model ID. |
| modelIdPath    | String                | The model ID path.|
| measurepointId | String| The measurement point ID.|
| hitRuleId      | String                | The rule ID of the triggered alert.|
| value          | Integer/Double/Object | The measurement point value. If ``triggeringDelayTimer`` is specified in the alert rule, this value will be when the ``triggeringDelayTimer`` starts counting.|
| occurTime      | Long| The UTC time when the alert occurs.|
| localOccurTime     | String| The local time when the alert occurs.|
| createTime     | Long| The UTC time when the active alert was created.|
| updateTime     | Long| The UTC time when the active alert was last updated.|
| severityId     | String| The alert severity ID.|
| severityDesc   | StringI18n            | The alert severity description.|
| typeId        | String                | The alert type ID.|
| typeDesc       | StringI18n            | The alert type description.|
| subTypeId      | String                | The alert sub-type ID.|
| subTypeDesc    | StringI18n            | The alert sub-type description.|
| contentId      | String                | The alert content ID.|
| contentDesc    | StringI18n            | The alert description.|
| eventType      | Integer               | The event type.<ul><li>0 = system-recovered alert</li><li>1 = system-triggered alert</li><li>2 = API-recovered alert</li><li>3 = API-inserted alert</li></ul> |
| tag            | Map            | User-defined tags. (The Key and Value are of String type.)|
| ruleDesc       | StringI18n            | The rule description.|
| assetPaths  |  String Array     | A path list of the alert assets on the asset tree according to the scope of the alert rule.<br>The format is: ["treeId1:/assetId1/assetId2/assetIdx", "treeId2:/assetId3/assetIdx"]|
| maskedBy  |  String Array     | If an alert is a derivative alert, return the root alert that caused the alert to be blocked.<br>The format is: ["treeId1:eventId1", "treeId1:eventId2"]|




## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=search&orgId=yourOrgId 
method: POST 
requestBody: 
{
	"expression": "eventId='20190531b83331a8549e1e956f2413552eda1ec9'",
	"pagination": {
		"pageNo": 1,
		"pageSize": 20
	},
	"action": "search"
}

```

### Return Sample

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 20,
		"totalSize": 1,
		"sortedBy": [{
			"field": "occurTime",
			"order": "DESC"
		             },
			{
			"field": "eventId",
			"order": "DESC"
			}]
	              },
	"code": 0,
	"msg": "OK",
	"requestId": "a9689b9f-0cb6-4e47-a41c-bd459b687309",
	"data": [{
		"eventId": "20190531b83331a8549e1e956f2413552eda1ec9",
		"orgId": "yourOrgId",
		"assetId": "qu5TmJRj",
		"modelId": "Inverter_Model",
		"modelIdPath": "/Inverter_Model",
		"measurepointId": "power",
		"deviceStatus": null,
        "hitRuleId": null,
		"value": "3.5559796405967736",
		"occurTime": 1559304899404,
		"localOccurTime": "2019-06-01 02:14:59",
		"createTime": 1559304899519,
		"updateTime": 1560745022684,
		"severityId": "alert_001",
		"severityDesc": {
			"i18nValue": {
				"en_US": "alert",
				"zh_CN": "alert"
			             }
		                },
		"typeId": "errorType",
		"subTypeId": null,
		"typeDesc": {
			"i18nValue": {
				"en_US": "errorType desc",
				"zh_CN": ""
			             }
		            },
		"subTypeDesc":{
				"i18nValue":{
					"en_US":"",
					"zh_CN":""
						}
				},
		"contentId": "001",
		"contentDesc": {
			"i18nValue": {
				"en_US": "001",
				"zh_CN": "001"
			             }
		               },
		"eventType": 1,
		"tag": {
			"Tag999": "999"
		       },
		"ruleDesc":{
				"i18nValue":{
					"en_US":"",
					"zh_CN":""
				}
			},
		"assetPaths": null,
		"maskedBy": null
	        }]
}
```

## Java SDK Sample

```java
public void testSearchActiveAlerts() {
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";
    SearchActiveAlertRequest request = new SearchActiveAlertRequest();
    request.setOrgId("yourOrgId");
    request.setExpression("eventId='yourEventId'");
    Pagination pagination = new Pagination();
    pagination.setPageSize(20);
    pagination.setPageNo(1);
    request.setPagination(pagination);
    try {
        SearchActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url("https://{apigw-address}")
            .getResponse(request, SearchActiveAlertResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
