# Search History Alerts

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Query historical alerts.

## Request format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=search
```

## Request parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
                                                                 

## Request parameters (Body)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|------|----------|--------------------|----|------|
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs#how-to-get-modeid-information-modeid)|
| assetIds        | false     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |
| measurepointsId     | false     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId information](/docs/api/en/latest/api_faqs#how-to-get-the-measurepoint-pointid-information-pointid)                                                                                                                                                                           |
| startOccurTime        | false     | String. See [Time Parameter Used by API](/docs/api/en/latest/api_faqs.html#id5)   | Start time for triggering alert.  |
| endOccurTime        | false     | String. See [Time Parameter Used by API](/docs/api/en/latest/api_faqs.html#id5)       |  End time for triggering alert.  |
| recoverStartTime        | false     | String. See [Time Parameter Used by API](/docs/api/en/latest/api_faqs.html#id5)       | Start time of alert recovery. If left blank, the data within the last week will be searched.  |
| recoverEndTime        | false     | String. See [Time Parameter Used by API](/docs/api/en/latest/api_faqs.html#id5)       | End time of alert recovery. If left blank, the data within the last week will be searched.
| expression         | false    | String   | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| pagination  | false  |Pagination request structure | Random pagination. The default is to sort in descending order by `occurTime`, and the user can not specify the sorting field. The default pagination size is 10 pages. See [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |


## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | HistoryAlert structure| History alert information array, including recovery time, event ID, and reason for recovery. See [HistoryAlert Structure](/docs/api/en/latest/event/search_history_alerts.html#id7)|

### HistoryAlert structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| eventId        | String                | Alert id                                                                          |
| orgId          | String                |  Organization ID which the asset belongs to|
| assetId        | String                | Asset ID|
| modelId        | String                | Model ID which the asset belongs to|
| modelIdPath    | String                | Model ID path|
| measurepointId | String                | Asset measurepoint|
| hitRuleId      | String                | Matched rule ID|
| value          | Integer/Double/Object | Measurepoint value|
| occurTime      | Long| UTC time when the alert occurs|
| localOccur     | String                | Local time when the alert occurs|
| recoverTime     | Long                | Alert recovery time|
| recoverLocaltime     | String                  | Local time of alert recovery |
| recoverReason     | String                | Recovery reason|
| createTime     | Long| UTC creation time|
| updateTime     | Long| UTC time for update|
| severityId     | String| Alert level ID|
| severityDesc   | StringI18n            | Alert level description|
| typeId        | String                | Alert type ID|
| typeDesc       | StringI18n            | Alert type description|
| subTypeId      | String                | Alert sub-type|
| subTypeDesc    | StringI18n            | Alert sub-type description|
| contentId      | String                | Alert content ID|
| contentDesc    | StringI18n            | Alert description|
| eventType      | Integer               | Event type: 0 - system recovery alert; 1 - system-triggered alert; 2 - manual recovery alert; 3 - manually-inserted alarm |
| tag            | Tag structure            | Alert tags|
| ruleDesc       | StringI18n            | Rule description|



## Input/output samples

### Request sample

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

### Return sample

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
		"orgId": "1c499110e8800000",
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

## Java SDK invocation sample

```java
public void testSearchHistoryAlerts(){  
        String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
        String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";  
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
	            SearchHistoryAlertResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchHistoryAlertResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	        }catch(Exception e){  
	            System.out.print(e);  
	        }  
	    }
```