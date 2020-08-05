# Search History Alerts

Search for the past 3 months' historical alerts.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search
```

## Request Parameters (URI)

| Name | Mandatory/Optional | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)


| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | Optional    | String    | The model ID. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid)|
| assetId        | Optional     | String    | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| measurepointsId     | Optional     | String    | The measurement point ID. [How to get pointId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)|
| startOccurTime        | Mandatory     | String   | The start time for triggering alert. For more information, see [Time parameters used in API](/docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api). |
| endOccurTime        | Mandatory     | String       |  The end time for triggering alert. For more information, see [Time parameters used in API](/docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api). |
| recoverStartTime        | Optional     | String  | The start time of the alert recovery. If left blank, the data within the last week will be searched. For more information, see [Time parameters used in API](/docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api). |
| recoverEndTime        | Optional     | String    | The end time of the alert recovery. If left blank, the data within the last week will be searched. For more information, see [Time parameters used in API](/docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api).  |
| expression         | Optional    | String   | The query expression, which supports sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId`, `tag`, `deviceStatus` and `assetPath`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". ``tag`` also supports arithmetic operator "exists" and "not exists". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)|
| scope |  Optional   | Scope Struct | Query the alerts in a specified asset tree or in an asset node on the asset tree, and specify whether to return the blocked derivative alerts. **This parameter cannot be applied with rootAlert**. For more details, see [Scope Struct](search_history_alerts#scope-struct-scope). |
|  rootAlert  |   Optional  | RootAlert Struct | Query the derivative alerts which are blocked by the specified root alert. **This parameter cannot be applied with scope**. For more details, see [RootAlert Struct](search_history_alerts#rootalert-struct-rootalert).|
| pagination  | Optional  |Pagination Request Struct | Lists the paging requirements in a request. If not specified, the pagination size is 10, sorted in descending order by `occurTime`. `sorters` is not supported to sort the response. For more details, see [Pagination Request Struct>>](/docs/api/en/2.1.0/overview.html#pagination-request-struct) |


### Scope Struct <scope>

| Name            | Mandatory/Optional | Data Type | Description |
|------------|--------------|--------------|-----------|
| treeId            | Mandatory         | String       |  The asset tree ID. |
| fromAssetId       | Optional        | String       | Return all alerts of and under the asset node of the specified asset ID. If not specified, the alerts of all the nodes in the specified ``treeID`` will be returned.|
| includeDerivative | Optional        | Boolean      | <ul><li>true = include the derivative alerts in the response</li><li>false (default) = does not include the derivative alerts</li></ul>|



### RootAlert Struct <rootalert>

| Name            | Mandatory/Optional | Data Type | Description |
|-------------|--------------|--------------|------------|
| treeId      | Optional        | String       | The asset tree ID.   |
| rootAlertId | Mandatory         | String       | The root alert ID. |




## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Array of HistoryAlert Structs| A list of the history alerts returned. For details of a historyAlert struct, see [HistoryAlert Struct](search_history_alerts#historyalert-struct-ha). |

### HistoryAlert Struct<ha>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| eventId        | String                | The alert ID. |
| orgId          | String                |  The organization ID which the asset belongs to.|
| assetId        | String                | The asset ID.|
| modelId        | String                | The model ID.|
| modelIdPath    | String                | The model ID path.|
| measurepointId | String                | The measurement point ID.|
| deviceStatus     | String   | The device status. |
| hitRuleId      | String                | The rule ID of the triggered alert. |
| value          | Integer/Double/Object | The measurement point value. If ``triggeringDelayTimer`` is specified in the alert rule, this value will be when the ``triggeringDelayTimer`` starts counting.|
| occurTime      | Long| The UTC time when the alert occurs.|
| localOccurTime     | String                | The local time when the alert occurs.|
| recoverTime     | Long                | The recovery time in UTC format.|
| localRecoverTime     | String                  | The recovery time in local format.  |
| recoverReason     | String                | The recovery reason.|
| createTime     | Long| The UTC time when the history alert was created.|
| updateTime     | Long| The UTC time when the history alert was last updated.|
| severityId     | String| The alert severity ID.|
| severityDesc   | StringI18n            | The alert severity description.|
| typeId        | String                | The alert type ID.|
| typeDesc       | StringI18n            | The alert type description.|
| subTypeId      | String                | The alert sub-type.|
| subTypeDesc    | StringI18n            | The alert sub-type description.|
| contentId      | String                | The alert content ID.|
| contentDesc    | StringI18n            | The alert description.|
| eventType      | Integer               | The event type.<ul><li>0 = system-recovered alert</li><li>1 = system-triggered alert</li><li>2 = API-recovered alert</li><li>3 = API-inserted alert</li></ul> |
| tag            | Map            | User-defined tags. (The Key and Value are of String type.)|
| ruleDesc       | StringI18n            |The rule description.|
| assetPaths  |  String Array     | A path list of the alert assets on the asset tree according to the scope of the alert rule.<br>The format is: ["treeId1:/assetId1/assetId2/assetIdx", "treeId2:/assetId3/assetIdx"]|
| maskedBy  |  String Array     | If an alert is a derivative alert, return the root alert that caused the alert to be blocked.<br>The format is: ["treeId1:eventId1", "treeId1:eventId2"]|



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/history-alerts?action=search&orgId=yourOrgId
method: POST 
requestBody:
{
	"endOccurTime": "2019-06-15T00:00:00Z",
	"expression": "eventId='20190612cf89cd96b0be4cafcc342d0dc2ac75a4'",
	"pagination": {
		"pageNo": 1,
		"pageSize": 2
	},
	"startOccurTime": "2019-05-20T00:00:00Z",
  "action": "search"
}
```

### Return Sample

```json
{
	"pagination":{
		"pageNo":1,
		"pageSize":2,
		"totalSize":1,
		"sortedBy":[
			{
				"field":"occurTime",
				"order":"DESC"
			},
			{
				"field":"eventId",
				"order":"DESC"
			}
		]
	},
	"code":0,
	"msg":"OK",
	"requestId":"dac2a872-b9b7-460c-992d-0a0c14ea36e9",
	"data":[
		{
			"recoverTime":1560382560000,
			"recoverLocalTime":"2019-06-13 07:36:00",
			"recoverReason":"rule-recover",
			"eventId":"20190612cf89cd96b0be4cafcc342d0dc2ac75a4",
			"orgId":"yourOrgId",
			"assetId":"rQN8IRs4",
			"modelId":"lemo2",
			"modelIdPath":"/lemo2",
			"measurepointId":"lemo_point1_raw",
			"value":"99.06250421",
			"occurTime":1560382380000,
			"localOccurTime":"2019-06-13 07:33:00",
			"createTime":1560382559735,
			"updateTime":1560744923855,
			"severityId":"Urgent",
      "deviceStatus":null,
      "subTypeId":null,
      "subTypeDesc":null,
      "ruleDesc":null,
      "assetPath":null,
      "maskedBy":null,
			"severityDesc":{
				"i18nValue":{
					"en_US":"紧急告警",
					"zh_CN":"紧急告警"
				}
			},
			"typeId":"yourTypeId",
			"typeDesc":{
				"i18nValue":{
					"en_US":"yourAlertType",
					"zh_CN":"yourAlertTypeInChinese"
				}
			},
			"contentId":"001",
			"contentDesc":{
				"i18nValue":{
					"en_US":"yourAlertContent",
					"zh_CN":"yourAlertContentInChinese"
				}
			},
			"eventType":0,
			"tag":{
				"yourTag1":"yourValue1",
				"yourTag2":"yourValue2"
			}
		}
	]
}
```

## Java SDK Sample

```java
public void testSearchHistoryAlerts(){  
    String accessKey = "yourAppAccessKey";  
    String secretKey = "yourAppSecretKey";  
    SearchHistoryAlertRequest request = new SearchHistoryAlertRequest();  
    request.setOrgId("yourOrgId");  
    request.setStartOccurTime("2019-05-20T00:00:00Z");  
    request.setEndOccurTime("2019-06-15T00:00:00Z");  
    Pagination pagination = new Pagination();  
    pagination.setPageSize(2);  
	    pagination.setPageNo(1);  
	    request.setPagination(pagination);  
	    request.setExpression("eventId='yourEventId'");  
	    try {  
	        SearchHistoryAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                .url("https://{apigw-address}")  
	                .getResponse(request, SearchHistoryAlertResponse.class);  
	        Gson gson = new Gson();  
	        System.out.println(gson.toJson(response));  
	    }catch(Exception e){  
	        System.out.print(e);  
	    }  
}
```
