# Delete Alert Content

Delete an alert content. It cannot be deleted if it is used by other rules. 


## Prerequisite

Ensure that the alert content to be deleted is not used by any other rules. 

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)            |
|alertContentId | Query      | Mandatory | String | The alert content ID. |


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-contents?action=delete&orgId=yourOrgId&alertContentId=planetTemperature
method: POST 
requestBody:
{
  "action": "delete"
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": ""
}
```

### Java SDK Sample

```java
public void testDeleteAlertContent() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    DeleteAlertContentRequest request = new DeleteAlertContentRequest();
    request.setOrgId(orgId);
    request.setAlertContentId("yourContentId");
    request.setSource("box1");
    try {
        DeleteAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, DeleteAlertContentResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
