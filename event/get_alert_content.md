# Get Alert Content

Get an alert content based on ``orgId`` and ``contentId``.


## Request Format

```
GET https://{apigw-address}/event-service/v2.1/alert-contents?action=get
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| contentId         | Query            | Mandatory     | String    | The alert content ID.                 |
                                                                 

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | AlertContent Struct | The details of the alert content. For more information, see [AlertContent Struct](/docs/api/en/2.1.0/event/get_alert_content.html#alertcontent-struct-alertcontent).|

### AlertContent Struct <alertcontent>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| contentId| String           | The alert content ID.                 |
| contentDesc | StringI18n | The alert content description.         |
| modelId| String           | The model ID.                 |
| orgId          | String                |  The organization ID which the asset belongs to.|
| alertType  | AlertType Struct  | The details of the alert type. For more information, see [AlertType Struct>>](/docs/api/en/2.1.0/event/search_alert_type.html#alerttype-struct-alerttype).               |
|subAlertType  | AlertType Struct  | The details of the alert sub-type. For more information, see [AlertType Struct](/docs/api/en/2.1.0/event/search_alert_type.html#alerttype-struct-alerttype).   |
| tags| Map        | The user-defined tags. (The Key and Value are of String type.) |
| updatePerson| String           | The name of the person who last updated the alert severity.           |
| updateTime| Long             | The time when the alert was last updated in UTC format.       |



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-contents?action=get&contentId=yourContentId&orgId=yourOrgId
method: GET 
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "f40fbb09-ce20-463f-bb18-6659a8bd6926",
	"data": {
		"contentId": "doubleContentuid",
		"contentDesc": {
			"i18nValue": {
				"en_US": "doubleContentuid desc",
				"zh_CN": ""
			}
		},
		"modelId": "ssss",
		"orgId": "yourOrgId",
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612131000,
		"alertType": {
			"typeId": "doubleType",
			"typeDesc": {
				"i18nValue": {
					"en_US": "doubleType desc",
					"zh_CN": ""
				}
			},
			"tags": {	
			},
			"updateTime": 0
		},
		"subAlertType": {
			"typeDesc": {
				"i18nValue": {
					"en_US": "doubleType desc",
					"zh_CN": ""
				}
			},
			"tags": {	
			},
			"updateTime": 0
		},
		"tags": {	
		}
	},
	"action": "get"
}
```

## Java SDK Sample

```java
public void testGetAlertContent() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    final String contentId = "yourContentId";
    GetAlertContentRequest request = new GetAlertContentRequest();
    request.setOrgId(orgId);
    request.setContentId(contentId);
    try {
        GetAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, GetAlertContentResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
        if (response.getCode() == 0) {
            System.out.println(response.getData());
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
