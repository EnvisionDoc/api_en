# Update Active Alert Tags

Update the tags of an active alert.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=updateTags
```

## Request Parameters (URI)

| Name | Mandatory/Optional | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|------|----------|--------------------|----|------|
| eventId       | Query            | Mandatory     | String     | The alert ID.  |
| tags          | Query            | Mandatory     | Map | The user-defined tags to be modified. (The Key and Value are of String type.) For details, see [How to use tags](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag). |
| isPatchUpdate | Query            | Mandatory     | Boolean    | <ul><li>true (default) = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.</li><li>false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.</li></ul>  |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|------------------|
| data | Integer | The number of updated entries.|


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=updateTags&orgId=yourOrgId
method: POST 
requestBody: 
{
	"eventId": "yourEventId",
	"isPatchUpdate": false,
	"tags": {
		"Tag999": "999"
	},
  "action": "update"
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": 1
}
```

## Java SDK Sample

```java
public void testUpdateActiveAlertTags(){  
       String accessKey = "yourAppAccessKey";  
       String secretKey = "yourAppSecretKey";  
  
       UpdateActiveAlertTagsRequest request = new UpdateActiveAlertTagsRequest();  
       request.setOrgId("yourOrgId");  
       request.setEventId("yourEventId");  
       Map<String,String> map = new HashMap<>();  
       map.put("yourTagKey","yourTagValue");  
	   request.setTags(map);  
	   request.setIsPatchUpdate(false);  
       try {  
	       UpdateActiveAlertTagsResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                   .url("https://{apigw-address}")  
	                   .getResponse(request, UpdateActiveAlertTagsResponse.class);  
	       System.out.println(new Gson().toJson(response));  
       } catch(Exception e) {  
	       System.out.print(e);  
	   }  
}
```