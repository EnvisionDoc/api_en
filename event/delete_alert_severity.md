# Delete Alert Severity

Delete an alert severity. It cannot be deleted if it is used by other rules.


## Prerequisite

Ensure that the alert severity to be deleted is not used by any other rules. 

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)             |
|severityId      | Query  |  Mandatory  |   String  |  The alert severity ID.|



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-severities?action=delete&orgId=yourOrgId&severityId=yourSeverityId
method: POST 
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
public void testDeleteAlertSeverity() {
    DeleteAlertSeverityRequest request = new DeleteAlertSeverityRequest();
    request.setOrgId(orgId);
    request.setSeverityId("yourSeverityId");
    try {
        DeleteAlertSeverityResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url(url)
            .getResponse(request, DeleteAlertSeverityResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```