# Aggregate Active Alerts



 Perform statistics on active alerts.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate
```

## Request Parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|----------------|----------|--------------------|----|
| expression         | false    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=", "in", and "!=", and the logical operator is "and" and "or". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| groupByField   | true     | String             | Grouping fields: `contentId`, `assetId`, `modelId`, `measurepointId`, `severityId`, `typeId`, `subTypeId` |
| startOccurTime | false    | String| Start time for triggering alert. See [Time parameters used in API](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api)    |
| endOccurTime   | false    | String| End time for triggering alert. See [Time parameters used in API](/docs/api/en/latest/api_faqs.html#time-parameters-used-in-api) |



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Map (Key is of String type, and the value is of Integer type) | The Key is the value of the grouping field, and the value is the number of alerts that the object has generated within the specified time range.|


## Input/Output Samples

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate&orgId=1c499110e8800000

{
	"groupByField": "assetId"
}

```

### Return Sample

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

## Java SDK Sample

```java
public void testAggregateActiveAlert(){  
       String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
       String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
       AggregateActiveAlertRequest request = new AggregateActiveAlertRequest();  
       request.setOrgId("1c499110e8800000");  
       request.setGroupByField("assetId");  
       request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	       try {  
	           AggregateActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                   .url("https://{apigw-address}")  
	                   .getResponse(request, AggregateActiveAlertResponse.class);  
	           Gson gson = new Gson();  
	           System.out.println(gson.toJson(response));  
	       }catch(Exception e){  
	           System.out.print(e);  
	       }  
	   }
```