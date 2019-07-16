# Update Active Alert Tags



Update active alert tags.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=updateTags
```

## Request Parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|------|----------|--------------------|----|------|
| eventId       | Query            | true     | String     | Alert ID  |
| tags          | Query            | true     | Tag structure | Tag map you want to modify |
| isPatchUpdate | Query            | true     | Boolean    | Whether to update in full; false stands for full modification, true stands for partial modification.  |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|------------------|
| data | Integer | Number of updated entries|


## Input/Output Samples

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=updateTags&orgId=1c499110e8800000
{
	"eventId": "20190531b83331a8549e1e956f2413552eda1ec9"
	"isPatchUpdate": false,
	"tags": {
		"Tag999": "999"
	}
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "success",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": 1
}
```

## Java SDK Sample

```java
public void testUpdateActiveAlertTags(){  
       String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
       String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
  
       UpdateActiveAlertTagsRequest request = new UpdateActiveAlertTagsRequest();  
       request.setOrgId("1c499110e8800000");  
       request.setEventId("20190531b83331a8549e1e956f2413552eda1ec9");  
       Map<String,String> map = new HashMap<>();  
       map.put("Tag999","999");  
	       request.setTags(map);  
	       request.setIsPatchUpdate(false);  
	  
	       request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	  
	  
	       try {  
	           UpdateActiveAlertTagsResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                   .url("https://{apigw-address}")  
	                   .getResponse(request, UpdateActiveAlertTagsResponse.class);  
	           System.out.println(new Gson().toJson(response));  
	       }catch(Exception e){  
	           System.out.print(e);  
	       }  
}
```