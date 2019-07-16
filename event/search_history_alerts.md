# Search History Alerts



Query historical alerts.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search
```

## Request Parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)


| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | Model ID which the asset belongs to. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)|
| assetId        | false     | String    | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| measurepointsId     | false     | String    | Asset measurement point. [How to get pointId](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)|
| startOccurTime        | false     | String. See [Time parameters used in API](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api)   | Start time for triggering alert.  |
| endOccurTime        | false     | String. See [Time parameters used in API](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api)       |  End time for triggering alert.  |
| recoverStartTime        | false     | String. See [Time parameters used in API](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api)       | Start time of alert recovery. If left blank, the data within the last week will be searched.  |
| recoverEndTime        | false     | String. See [Time parameters used in API](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api)       | End time of alert recovery. If left blank, the data within the last week will be searched.
| expression         | false    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| pagination  | false  |Pagination request structure | Random pagination. The default is to sort in descending order by `occurTime`, and the user can not specify the sorting field. The default pagination size is 10 pages. See [Pagination Request Structure](/docs/api/en/latest/overview.html#pagination-request-structure) |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | HistoryAlert structure| History alert information array, including recovery time, event ID, and reason for recovery. See [HistoryAlert Structure](/docs/api/en/latest/event/search_history_alerts.html#id7)|

### HistoryAlert Structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| eventId        | String                | Alert id                                                                          |
| orgId          | String                |  Organization ID which the asset belongs to|
| assetId        | String                | Asset ID|
| modelId        | String                | Model ID which the asset belongs to|
| modelIdPath    | String                | Model ID path|
| measurepointId | String                | Asset measurement point|
| hitRuleId      | String                | Matched rule ID|
| value          | Integer/Double/Object | Measurement point value|
| occurTime      | Long| UTC time when the alert occurs|
| localOccur     | String                | Local time when the alert occurs|
| recoverTime     | Long                | Alert recovery time|
| recoverLocaltime     | String                  | Local time of alert recovery |
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
| tag            | Tag structure            | Alert tags|
| ruleDesc       | StringI18n            | Rule description|



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
		"recoverLocaltime": "2019-06-13 07:36:00",
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