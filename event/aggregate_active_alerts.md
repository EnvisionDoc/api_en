# Aggregate Active Alerts

Calculate the number of active alerts.

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate
```

## Request Parameters (URI)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
                                                                 

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - expression
     - Optional
     - String
     - The query expression, which supports sql-like query. The fields that are supported for query include: ``modelId``, ``assetId``, ``measurepointId``, ``hitRuleId``, ``severityId``, ``typeId``, ``subTypeId``, ``contentId``, ``eventType``, ``eventId`` and ``tag``. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". ``tag`` also supports arithmetic operator "exists" and "not exists". `How to use expression>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`_
   * - groupByField
     - Mandatory
     - String
     - The fields to group the results by. The fields supported are: ``contentId``, ``assetId``, ``modelId``, ``measurepointId``, ``severityId``, ``typeId``, ``subTypeId`` 
   * - startOccurTime
     - Optional
     - String
     - The start time for triggering the alert. For more details, see `Time parameters used in API>> </docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api>`_
   * - endOccurTime
     - Optional
     - String
     - The end time for triggering the alert. For more details, see `Time parameters used in API>> </docs/api/en/2.1.0/api_faqs.html#time-parameters-used-in-api>`_



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Map
     - The Key (String type) is the value of the grouping field, and the value (Int type) is the number of alerts that the object has generated within the specified time range.


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate&orgId=yourOrgId
method: POST 
requestBody: 
{
	"groupByField": "assetId",
  "action": "aggregate"
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
       String accessKey = "yourAccessKey";  
       String secretKey = "yourSecretKey";  
       AggregateActiveAlertRequest request = new AggregateActiveAlertRequest();  
       request.setOrgId("yourOrgId");  
       request.setGroupByField("assetId");  
       request.headerParams().put("apim-accesskey","yourAccessKey");  
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