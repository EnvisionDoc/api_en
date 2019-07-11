# Search Active Alerts

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Query the active alerts.

## Request format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=search
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
                                                                 

## Request parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs#how-to-get-modeid-information-modeid)|
| assetIds        | false     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |
| measurepointsId     | false     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId information](/docs/api/en/latest/api_faqs#how-to-get-the-measurepoint-pointid-information-pointid)                                                                                                                                                                           |
| startOccurTime | false    | String| Start time for triggering alert. See [Time Parameter Used by API] (/docs/api/en/latest/api_faqs.html#id5)    |
| endOccurTime   | false    | String| End time for triggering alert. See [Time Parameter Used by API] (/docs/api/en/latest/api_faqs.html#id5) |
| expression         | false    | String   | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| pagination  | false  |Pagination request structure | Random pagination. The default is to sort in descending order by `occurTime`, and the user can not specify the sorting field. The default pagination size is 10 pages. See [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |

## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | ActiveAlert structure | List of active alerts. For details, see [ActiveAlert Structure](/docs/api/en/latest/event/search_active_alerts#id5)|

### ActiveAlert structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| eventId        | String                | Alert id                                                                          |
| orgId          | String                | Organization ID which the asset belongs to. |
| assetId        | String                | Asset ID. |
| modelId        | String                | Model ID which the asset belongs to. |
| modelIdPath    | String                | Model ID path|
| measurepointId | String| Asset measurepoint|
| hitRuleId      | String                | Matched rule ID|
| value          | Integer/Double/Object | Measurepoint value|
| occurTime      | Long| UTC time when the alert occurs|
| localOccur     | String| Local time when the alert occurs|
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
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=search &orgId=1c499110e8800000 
{
	"expression": "eventId='20190531b83331a8549e1e956f2413552eda1ec9'",
	"pagination": {
		"pageNo": 1,
		"pageSize": 20
	              }
}

```

### Return sample

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
		"orgId": "1c499110e8800000",
		"assetId": "qu5TmJRj",
		"modelId": "Inverter_Model",
		"modelIdPath": "/Inverter_Model",
		"measurepointId": "power",
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
		"typeDesc": {
			"i18nValue": {
				"en_US": "errorType desc",
				"zh_CN": ""
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
		       }
	        }]
}
```

## Java SDK invocation sample

```java
public void testSearchActiveAlerts(){  
        String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
        String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";  
        SearchActiveAlertRequest request = new SearchActiveAlertRequest();  
        request.setOrgId("1c499110e8800000");  
        request.setExpression("eventId='20190531b83331a8549e1e956f2413552eda1ec9'");  
        Pagination pagination = new Pagination();  
        pagination.setPageSize(20);  
        pagination.setPageNo(1);  
	        request.setPagination(pagination);  
	        request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	        try {  
	            SearchActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchActiveAlertResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	        }catch(Exception e){  
	            System.out.print(e);  
	        }  
}
```