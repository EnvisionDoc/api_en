# Aggregate Active Alerts

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

 Perform statistics on active alerts.

## Request format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate
```

## Request parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
                                                                 

## Request parameters (Body)
| Name            | Required or Not | Data Type | Description |
|----------------|----------|--------------------|----|
| expression         | false    | String   | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| groupByField   | true     | String             | Grouping fields: `contentId`, `assetId`, `modelId`, `measurepointId`, `severityId`, `typeId`, `subTypeId` |
| startOccurTime | false    | String| Start time for triggering alert. See [Time Parameter Used by API] (/docs/api/en/latest/api_faqs.html#id5)    |
| endOccurTime   | false    | String| End time for triggering alert. See [Time Parameter Used by API] (/docs/api/en/latest/api_faqs.html#id5) |



## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Map (Key is of String type, and the value is of Integer type) | The Key is the value of the grouping field, and the value is the number of alerts that the object has generated within the specified time range.|


## Input/output samples

### Request sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate&orgId=1c499110e8800000

{
	"groupByField": "assetId"
}

```

### Return sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "12995105-514a-4706-9749-5930fd7145f9",
	"data": {
		"uEZPYKL0": 5,
		"J123maMn": 2,
		"Gx5mj2OE": 1,
		"qu5TmJRj": 1,
		"TMET5UCK": 1,
		"IkaNsY3h": 1,
		"L03wWUoU": 1,
		"OAESlCPt": 1
	}
}

```

## Java SDK invocation sample

```java
public void testAggregateActiveAlert(){  
       String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
       String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";  
       AggregateActiveAlertRequest request = new AggregateActiveAlertRequest();  
       request.setOrgId("1c499110e8800000");  
       request.setGroupByField("assetId");  
       request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	       try {  
	           AggregateActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                   .url("https://{apigw-address}")  
	                   .getResponse(request, AggregateActiveAlertResponse.class);  
	           Gson gson = new Gson();  
	           System.out.println(gson.toJson(response));  
	       }catch(Exception e){  
	           System.out.print(e);  
	       }  
	   }
```