# Search Alert Type

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Query alert types by page.

## Request format

```
POST https://{apigw-address}/event-service/v2.1/alert-types/search?action=search
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
                                                                 

## Request parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| expression         | false    | String   | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| pagination     | false     | Pagination request structure    | Pagination parameter. Ten entries are displayed in each page by default if this parameter is left blank. The entries are sorted in descending order by `updateTime` by default. User can use a field in the `AlertType` structure for sorting purpose. See [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |

## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data  | AlertType structure  | Alert type. See [AlertType Structure](/docs/api/en/latest/event/search_alert_type.html#id4) |

### AlertType structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| typeId        | String                | Alert type ID|
| typeDesc   | StringI18n            | Alert type description|
| orgId          | String                |  Organization ID which the asset belongs to|
| parentTypeId        | String          | Parent alert type ID. If set as null, it is the parent alert type |
| tag        | Tag structure          | Tags|
| updatePerson        | String                | Updater|
| updateTime    | Long                | Update time (UTC)



## Input/output samples

### Request sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-types/search?action=search&orgId=1c499110e8800000
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "typeId",
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
		"totalSize": 14,
		"sortedBy": [{
			"field": "typeId",
			"order": "DESC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "c1be09d8-a6f2-4647-92e1-3c545fa1b3dd",
	"data": [{
		"typeId": "dateType",
		"orgId": "1c499110e8800000",
		"typeDesc": {
			"i18nValue": {
				"en_US": "dateType desc",
				"zh_CN": ""
			}
		},
		"tags": {		
		},
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612655000
	}]
}
```

## Java SDK invocation sample

```java
public void testSearchAlertType() {  
        SearchAlertTypeRequest request = new SearchAlertTypeRequest();  
        request.setOrgId(orgId);  
        Pagination pagination = new Pagination();  
        pagination.setPageNo(1);  
        pagination.setPageSize(1);  
        List<Sorter> sorterList = new ArrayList<>();  
        sorterList.add(new Sorter("typeId", Sorter.Order.DESC));  
        pagination.setSorters(sorterList);  
	        request.setPagination(pagination);  
	        try {  
	            SearchAlertTypeResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchAlertTypeResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	        } catch (Exception e) {  
	            e.printStackTrace();  
	        }  
}
```