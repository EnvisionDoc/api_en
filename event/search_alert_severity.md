# Search Alert Severity



Query alert level by page.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| expression         | false    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `severityId`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| pagination     | false     | Pagination request structure    | Pagination parameter. Ten entries are displayed in each page by default if this parameter is left blank. The entries are sorted in descending order by `updateTime`. User can specify a field in the `AlertSeverity` structure as the sorting criterion. See [Pagination Request Structure](/docs/api/en/latest/overview.html#pagination-request-structure) |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | AlertSeverity structure | Alert level. See [AlertSeverity structure](/docs/api/en/latest/event/search_alert_severity.html#id4)|

### AlertSeverity structure

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| severityId        | String                | Alert level ID|
| orgId          | String                |  Organization ID which the asset belongs to|
| severityDesc   | StringI18n            | Alert level description |
| tags        | Tag structure           | Tags|
| updatePerson        | String                | Updater|
| updateTime    | Long                | Update time (UTC)



## Input/output samples

### Request Sample

```json
POST  https://{apigw-address}/event-service/v2.1/alert-severities?action=search&orgId=1c499110e8800000
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "severityID",
			"order": "ASC"
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
		"totalSize": 19,
		"sortedBy": [{
			"field": "severityID",
			"order": "ASC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "bd591868-0eb1-46dc-a989-c1de33cc671e",
	"data": [{
		"severityId": "001",
		"orgId": "yourOrgId",
		"severityDesc": {
			"i18nValue": {
				"en_US": "Serious！！！" ,
				"zh_CN": "Serious！！！"
			}
		},
		"tags": {
			"111": "2222"
		},
		"updatePerson": "yj_test_customer",
		"updateTime": 1559204166000
	}]
}
```

## Java SDK Sample

```java
public void testSearchAlertSeverity() {  
    SearchAlertSeverityRequest request = new SearchAlertSeverityRequest();  
    request.setOrgId("1c499110e8800000");  
    Pagination pagination = new Pagination();  
    pagination.setPageSize(1);  
	    pagination.setPageNo(1);  
    Sorter sorter = new Sorter("severityID", Sorter.Order.ASC);  
    List<Sorter> sorterList = new ArrayList<>();  
    sorterList.add(sorter);  
	    pagination.setSorters(sorterList);  
	    request.setPagination(pagination);  
	    request.headerParams().put("apim-accesskey", "4ced4f38-1ced-476e0a446215-a602-4307");  
	    try {  
	        SearchAlertSeverityResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())  
	                .url("https://{apigw-address}")  
	                .getResponse(request, SearchAlertSeverityResponse.class);  
	        Gson gson = new Gson();  
	        System.out.println(gson.toJson(response));  
	    } catch (Exception e) {  
	        System.out.print(e);  
	    }  
}
```