# Get Alert Content

*Note: This documentation is in the progress of translation. Thanks for your visit!*

Get alert content based on organization ID and content ID.

## Request format

```
GET https://{apigw-address}/event-service/v2.1/alert-contents action=get&orgId=1c499110e8800000
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| contentId         | Query            | true     | String    | Alert content ID.                 |
                                                                 

## Response parameters

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

### Request sample

```json
GET https://{apigw-address}/event-service/v2.1/alert-contents?action=get &contentId=doubleContentuid&orgId=1c499110e8800000
```

### Return sample

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
		"orgId": "1c499110e8800000",
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

## Java SDK invocation sample

```java
public void testGetAlertContent() {  
        final String contentId = "doubleContentuid";  
        GetAlertContentRequest request = new GetAlertContentRequest();  
        request.setOrgId(orgId);  
        request.setContentId(contentId);  
        try {  
            GetAlertContentResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
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
