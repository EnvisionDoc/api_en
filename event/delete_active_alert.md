# Delete Active Alert

Delete an active alert.

## Prerequisite

Ensure that the active alert to be deleted exists. 

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)    |
|  eventId  | Query  | Mandatory  |  String  |  The alert ID. |



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=delete&orgId=yourOrgId&eventId=yourEventId
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
	"data": null
}
```

### Java SDK Sample

```java
public void testDeleteActiveAlert() {
    String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
    DeleteActiveAlertRequest request = new DeleteActiveAlertRequest();
    request.setOrgId("1c499110e8800000");
    request.setEventId("20190709d32b8269b75dc52229dfa467b60ee9a0");
    try {
        DeleteActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url("http://10.27.20.193:8000")
            .getResponse(request, DeleteActiveAlertResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```