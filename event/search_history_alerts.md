# Search History Alerts

Query historical alerts in the latest 3 months.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search
```

## Request Parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)


| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | Model ID which the asset belongs to. [How to get modelID>>](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)|
| assetId        | false     | String    | Asset ID. [How to get assetId>>](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| measurepointsId     | false     | String    | Asset measurement point. [How to get pointId>>](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)|
| startOccurTime        | false     | String   | Start time for triggering alert. See [Time parameters used in API>>](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api) |
| endOccurTime        | false     | String       |  End time for triggering alert. See [Time parameters used in API>>](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api) |
| recoverStartTime        | false     | String  | Start time of alert recovery. If left blank, the data within the last week will be searched. See [Time parameters used in API>>](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api) |
| recoverEndTime        | false     | String    | End time of alert recovery. If left blank, the data within the last week will be searched. See [Time parameters used in API>>](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api)  |
| expression         | false    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression>>](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| scope |  false   | Scope struct | Query the alerts in a specified asset tree or in an asset node on the asset tree, and specify whether to return the blocked derivative alerts. **This parameter cannot be applied with rootAlert**. See [Scope Struct](search_history_alerts#scope-struct-scope). |
|  rootAlert  |   false  | RootAlert struct | Query the derivative alerts which are blocked by the specified root alert. **This parameter cannot be applied with scope**.See [RootAlert Struct](search_history_alerts#rootalert-struct-rootalert).|
| pagination  | false  |Pagination request struct | Random pagination. The default is to sort in descending order by `occurTime`. When not specified, the default pagination size is 10 pages. See [Pagination Request Struct>>](/docs/api/en/latest/overview.html#pagination-request-struct) |


### Scope Struct <scope>

| Name            | Required or Not | Data Type | Description |
|------------|--------------|--------------|-----------|
| treeId            | true         | String       |  ID of the asset tree |
| fromAssetId       | false        | String       | Asset ID. Optional.<br>When it is not specified, return the alerts of all nodes in the asset tree specified by `treeId`;<br>When it is specified, returns all alerts under the asset node (and in the node).|
| includeDerivative | false        | Boolean      | Whether to return the derivative alerts, the default is false, as no derivative alert is returned.|



### RootAlert Struct <rootalert>

| Name            | Required or Not | Data Type | Description |
|-------------|--------------|--------------|------------|
| treeId      | false        | String       | ID of the asset tree   |
| rootAlertId | true         | String       | Root alert ID |




## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | HistoryAlert struct| History alert information array, including recovery time, event ID, and reason for recovery. See [HistoryAlert Struct](/docs/api/en/latest/event/search_history_alerts.html#historyalert-struct-ha).|

### HistoryAlert Struct  <ha>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| eventId        | String                | Alert id                                                                          |
| orgId          | String                |  Organization ID which the asset belongs to|
| assetId        | String                | Asset ID|
| modelId        | String                | Model ID which the asset belongs to|
| modelIdPath    | String                | Model path|
| measurepointId | String                | Asset measurement point|
| hitRuleId      | String                | Rule ID of the triggered alert |
| value          | Integer/Double/Object | Measurement point value. If ``triggeringDelayTimer`` is specified in the alert rule, this value is that when ``triggeringDelayTimer`` starts counting.|
| occurTime      | Long| UTC time when the alert occurs|
| localOccurTime     | String                | Local time when the alert occurs|
| recoverTime     | Long                | Alert recovery time|
| recoverLocalTime     | String                  | Local time of alert recovery |
| recoverReason     | String                | Recovery reason|
| createTime     | Long| UTC creation time|
| updateTime     | Long| UTC time for update|
| severityId     | String| Alert severity ID|
| severityDesc   | StringI18n            | Alert severity description|
| typeId        | String                | Alert type ID|
| typeDesc       | StringI18n            | Alert type description|
| subTypeId      | String                | Alert sub-type|
| subTypeDesc    | StringI18n            | Alert sub-type description|
| contentId      | String                | Alert content ID|
| contentDesc    | StringI18n            | Alert description|
| eventType      | Integer               | Event type: 0 - system recovery alert; 1 - system-triggered alert; 2 - manual recovery alert; 3 - manually-inserted alarm |
| tag            | Tag struct            | Alert tags|
| ruleDesc       | StringI18n            | Rule description|
| assetPaths  |  String Array     | A path list of the alert assets on the asset tree according to the scope of the alert rule.<br>The format is as: ["treeId1:/assetId1/assetId2/assetIdx", "treeId2:/assetId3/assetIdx"]|
| maskedBy  |  String Array     | If an alert is a derivative alert, return the root alert that caused the alert to be blocked.<br>The format is as: ["treeId1:eventId1", "treeId1:eventId2"]|



## Input/Output Samples

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search&orgId=1c499110e8800000 

{
	"endOccurTime": "2019-06-15T00:00:00Z",
	"expression": "eventId='20190612cf89cd96b0be4cafcc342d0dc2ac75a4' ",
	"pagination": {
		"pageNo": 1,
		"pageSize": 2
	},
	"startOccurTime": "2019-05-20T00:00:00Z"
}
```

### Return Sample

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 2,
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
	"requestId": "dac2a872-b9b7-460c-992d-0a0c14ea36e9",
	"data": [{
		"recoverTime": 1560382560000,
		"recoverLocalTime": "2019-06-13 07:36:00",
		"recoverReason": "rule-recover",
		"eventId": "20190612cf89cd96b0be4cafcc342d0dc2ac75a4",
		"orgId": "yourOrgId",
		"assetId": "rQN8IRs4",
		"modelId": "lemo2",
		"modelIdPath": "/lemo2",
		"measurepointId": "lemo_point1_raw",
		"value": "99.06250421",
		"occurTime": 1560382380000,
		"localOccurTime": "2019-06-13 07:33:00",
		"createTime": 1560382559735,
		"updateTime": 1560744923855,
		"severityId": "Urgent",
		"severityDesc": {
			"i18nValue": {
				"en_US": "Urgent alert",
				"zh_CN": "Urgent alert"
			}
		},
		"typeId": "lemo_001",
		"typeDesc": {
			"i18nValue": {
				"en_US": "lemo_001",
				"zh_CN": "Over-upper-limit alert"
			}
		},
		"contentId": "001",
		"contentDesc": {
			"i18nValue": {
				"en_US": "Alert content",
				"zh_CN": "Upper limit (50) has been reached. Please deal with it now"
			}
		},
		"eventType": 0,
		"tag": {
			"tag999": "999",
			"tag000": "000"
		}
	}]
}
```

## Java SDK Sample

```java
public void testSearchHistoryAlerts(){  
        String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
        String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
        SearchHistoryAlertRequest request = new SearchHistoryAlertRequest();  
        request.setOrgId("1c499110e8800000");  
        request.setStartOccurTime("2019-05-20T00:00:00Z");  
        request.setEndOccurTime("2019-06-15T00:00:00Z");  
        Pagination pagination = new Pagination();  
        pagination.setPageSize(2);  
	        pagination.setPageNo(1);  
	        request.setPagination(pagination);  
	        request.setExpression("eventId='20190612cf89cd96b0be4cafcc342d0dc2ac75a4' ");  
	        request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
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