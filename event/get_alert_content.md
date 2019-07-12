# Get Alert Content



Get alert content based on organization ID and content ID.

## Request Format

```
GET https://{apigw-address}/event-service/v2.1/alert-contents action=get&orgId=1c499110e8800000
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| contentId         | Query            | true     | String    | Alert content ID.                 |
                                                                 

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | AlertContent structure | Alert content. See [AlertContent Structure](/docs/api/en/latest/event/get_alert_content.html#id3)|

### AlertContent structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| contentId| String           | Content ID                 |
| contentDesc | StringI18n | Alert content description         |
| modelId| String           | Model ID                 |
| orgId          | String                |  Organization ID which the asset belongs to|
| alertType  | AlertType structure  | Alert type. See [AlertType Structure](/docs/api/en/latest/event/search_alert_type.html#id4)               |
|subAlertType  | AlertType structure  | Sub-alert type. See [AlertType Structure](/docs/api/en/latest/event/search_alert_type.html#id4)               |
| tags| Tag structure        | User-customized alert content tags |
| updatePerson| String           | Update personnel name           |
| updateTime| Long             | Last update time       |



## Input/output samples

### Request Sample

```json
GET https://{apigw-address}/event-service/v2.1/alert-contents?action=get &contentId=doubleContentuid&orgId=1c499110e8800000
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
	}
}
```

## Java SDK Sample

```java
public void testGetAlertContent() {  
        final String contentId = "doubleContentuid";  
        GetAlertContentRequest request = new GetAlertContentRequest();  
        request.setOrgId(orgId);  
        request.setContentId(contentId);  
        try {  
            GetAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
                    .url("https://{apigw-address}")  
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