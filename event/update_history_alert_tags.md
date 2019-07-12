# Update History Alert Tags



Update history alert tags.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=updateTags
```

## Request Parameters (URI)

| Name | Required or Not | Data Type | Description |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|------|----------|--------------------|----|------|
| eventId       | Query            | true     | String     | Alert id  |
| tags          | Query            | true     | Tag structure | Tag map you want to modify |
| isPatchUpdate | Query            | true     | Boolean    | Whether to update in full; false stands for full modification, while true stands for partial modification.  |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|-------|
| data | Integer | Number of updated entries|


## Input/output samples

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/history-alerts?action=updateTags&orgId=1c499110e8800000

{
	"eventId": "20190612cf89cd96b0be4cafcc342d0dc2ac75a4",
	"isPatchUpdate": true,
	"tags": {
		"tag000": "000"
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
public void testUpdateHistoryAlertTags(){  
    String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
    String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";  
    UpdateHistoryAlertTagsRequest request = new UpdateHistoryAlertTagsRequest();  
    request.setOrgId("1c499110e8800000");  
    request.setEventId("20190612cf89cd96b0be4cafcc342d0dc2ac75a4");  
    Map<String,String> map = new HashMap<>();  
    map.put("tag000","000");  
    request.setTags(map);  
	    request.setIsPatchUpdate(true);  
	    request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	    try {  
	        UpdateHistoryAlertTagsResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                .url("https://{apigw-address}")  
	                .getResponse(request, UpdateHistoryAlertTagsResponse.class);
	        System.out.println(response);  
	    }catch(Exception e){  
	        System.out.print(e);  
	    }  
}
```