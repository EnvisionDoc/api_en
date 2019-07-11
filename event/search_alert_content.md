# Search Alert Content

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Query alert content by page.

## Request format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=search&orgId=1c499110e8800000 
{}
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
                                                                 

## Request parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | false    | String    | Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs#how-to-get-modeid-information-modeid)|
| alertTypeId  | false    | String               | Alert type ID   |
| subAlertTypeId    | false    | String   | Alert sub-type ID  |                       
| expression         | false    | String   | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| pagination     | false     | Pagination request structure    | Pagination parameter. Ten entries are displayed in each page by default if this parameter is left blank. By default, the entries are sorted by `updateTime` in descending order, and it is allowed for the user to specify the following field sorting criterion: `contentId`, `modelId`, `updatePerson`, `updateTime`. See [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |

## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | AlertContent structure | Alert content. See [AlertContent Structure](/docs/api/en/latest/event/search_alert_content.html#id4)|

### AlertContent structure

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



## Input/output samples

### Request sample

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

### Return sample

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
		"orgId": "1c499110e8800000",
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

## Java SDK invocation sample

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
	            SearchAlertContentResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchAlertContentResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response)); 
	        } catch (Exception e) {  
	            e.printStackTrace();  
	        }   
}
```