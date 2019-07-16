# Search Alert Content



Query alert content by page.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=search&orgId=1c499110e8800000 
{}
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | Model ID which the asset belongs to. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)|
| alertTypeId  | false    | String               | Alert type ID   |
| subAlertTypeId    | false    | String   | Alert sub-type ID  |                       
| expression         | false    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `contentId`, `modelId`, and `alertTypeId`. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| pagination     | false     | Pagination request structure    | Pagination parameter. 10 entries are displayed in each page by default if this parameter is left blank. By default, the entries are sorted by `updateTime` in descending order, and it is allowed for the user to specify the following field sorting criterion: `contentId`, `modelId`, `updatePerson`, `updateTime`. See [Pagination Request Structure](/docs/api/en/latest/overview.html#pagination-request-structure) |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | AlertContent structure | Alert content. See [AlertContent Structure](/docs/api/en/latest/event/search_alert_content.html#id4)|

### AlertContent Structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| contentId| String           | Content ID                 |
| contentDesc | StringI18n | Alert content description         |
| modelId| String           | Model ID                 |
| orgId          | String| Organization ID which the asset belongs to|
| alertType  | AlertType structure  | Alert type              |
| subAlertType| AlertType structure  | Sub-alert type             |
| tags| Tag structure        | User-customized alert content tags |
| updatePerson| String           | Update personnel name           |
| updateTime| Long             | Last update time       |



## Input/Output Samples

### Request Sample

```json
https://{apigw-address}/event-service/v2.1/alert-contents?action=search&orgId=1c499110e8800000 
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "contentId",
			"order": "DESC"
		}]
	}
}
```

### Return Sample

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"totalSize": 9,
		"sortedBy": [{
			"field": "contentId",
			"order": "DESC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "c4e28bda-8d76-4145-bc42-11bfc2c09c0d",
	"data": [{
		"contentId": "dateContentid",
		"contentDesc": {
			"i18nValue": {
				"en_US": "dateContentid desc",
				"zh_CN": ""
			}
		},
		"modelId": "ssss",
		"orgId": "yourOrgId",
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612131000,
		"alertType": {
			"typeId": "dateType",
			"typeDesc": {
				"i18nValue": {
					"en_US": "dateType desc",
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
					"en_US": "dateType desc",
					"zh_CN": ""
				}
			},
			"tags": {
			},
			"updateTime": 0
		},
		"tags": {	
		}
	}]
}
```

## Java SDK Sample

```java
public void testSearchAlertContent() {  
        SearchAlertContentRequest request = new SearchAlertContentRequest();  
        request.setOrgId(orgId);  
        request.setModelId("ssss");  
        Pagination pagination = new Pagination();  
        pagination.setPageNo(1);  
        pagination.setPageSize(1);  
        List<Sorter> sorterList = new ArrayList<>();  
        sorterList.add(new Sorter("contentId", Sorter.Order.DESC));  
	        pagination.setSorters(sorterList);  
	        request.setPagination(pagination);  
	        try {  
	            SearchAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchAlertContentResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response)); 
	        } catch (Exception e) {  
	            e.printStackTrace();  
	        }   
}
```