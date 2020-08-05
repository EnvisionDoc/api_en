# Update Alert Severity

Update an alert severity.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid) |
|isPatchUpdate|Query|Mandatory|Boolean|<ul><li>true (default) = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.</li><li>false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.</li></ul> |


## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| severity |  Mandatory  |  GenerateSeverity Struct  |  The details of the alert severity. For more information, see [GenerateSeverity Struct](update_alert_severity#generateseverity-struct-generateseverity). |


### GenerateSeverity Struct <generateseverity>

| Name | Mandatory/Optional | Data Type | Description                         |
|--------------|--------------|--------------|-------------------------------------|
| severityId   | Mandatory         | String       | The alert severity ID.                        |
| severityDesc | Mandatory         | StringI18n   | Specify the alert severity's description in its respective locale's language. For more details on the structure and locales supported, see [Internationalized name struct](/docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct). |
| tags         | Optional        | Map | User-defined tags. (The Key and Value are of String type.) For details, see [How to use tags](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag). |



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-severities?action=update&orgId=yourOrgId&isPatchUpdate=false
method: POST 
requestBody: 
{
	"severity": {
		"severityId": "planetTemperature",
		"severityDesc": {
			"defaultValue": "Error",
			"i18nValue": {
				"en_US": "Error",
				"zh_CN": "错误"
			}
		},
		"tags": {
			"year": "2000",
			"author": "cshan"
		}
	}
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
public void testUpdateAlertSeverity() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    UpdateAlertSeverityRequest request = new UpdateAlertSeverityRequest();
    GenerateSeverity severity = new GenerateSeverity();
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文1");
    map.put("en_US", "english1");
    desc.setI18nValue(map);
    severity.setSeverityDesc(desc);
    severity.setSeverityId("yourSeverityId");
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    severity.setTags(tags);
    request.setSeverity(severity);
    request.setOrgId(orgId);
    request.setIsPatchUpdate(false);
    try {
        UpdateAlertSeverityResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, UpdateAlertSeverityResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```