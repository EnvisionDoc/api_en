# Update Alert Content

Update an alert content. 

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)              |
|isPatchUpdate|Query|Mandatory|Boolean|<ul><li>true (default) = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.</li><li>false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.</li></ul> |


## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| alertContent          | Mandatory    | GenerateContent Struct    | The details of the alert content. For more information, see [GenerateContent Struct](update_alert_content#generatecontent-struct-generatecontent).|



### GenerateContent Struct <generatecontent>

| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
|contentId|Mandatory|String|The alert content ID.|
|contentDesc|Mandatory|String|The alert content description.|
| modelId          | Mandatory    | String    | The model ID. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid)  |
| alertTypeId   | Mandatory        | String       | The alert type ID.        |
|tags|Optional|Map|User-defined tags. (The Key and Value are of String type.) For details, see [How to use tags](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag).|


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-contents?action=update&orgId=yourOrgId&isPatchUpdate=false
method: POST 
requestBody: 
{
	"alertContent": {
		"contentId": "planetTemperature",
		"contentDesc": {
			"defaultValue": "Grid is connected from converter",
			"i18nValue": {
				"en_US": "Grid is connected from converter",
				"zh_CN": "风机已并网"
			}
		},
		"modelId": "WindDev-E0",
		"alertTypeId": "9001",
		"tags": {
			"year": "2000",
			"author": "cshan"
		}
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
	"data": null
}
```

### Java SDK Sample

```java
public void testUpdateAlertContent() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    UpdateAlertContentRequest request = new UpdateAlertContentRequest();
    request.setOrgId(orgId);
    GenerateContent generateContent = new GenerateContent();
    generateContent.setContentId("yourContentId");
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文");
    map.put("en_US", "english");
    desc.setI18nValue(map);
    generateContent.setContentDesc(desc);
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    generateContent.setTags(tags);
    request.setAlertContent(generateContent);
    request.setIsPatchUpdate(true);
    try {
        UpdateAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, UpdateAlertContentResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```