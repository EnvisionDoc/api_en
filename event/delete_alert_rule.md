# Delete Alert Rule

Delete an alert rule.


## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query| Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)           |
| ruleId      | Query| Mandatory| String| The ID of the alert rule to be deleted. |


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-rules?action=delete&orgId=yourOrgId&ruleId=yourRuleId
method: POST 
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
public void testDeleteRule() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    DeleteAlertRuleRequest request = new DeleteAlertRuleRequest();
    request.setOrgId(orgId);
    request.setRuleId("yourRuleId");
    try {
        DeleteAlertRuleResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, DeleteAlertRuleResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
