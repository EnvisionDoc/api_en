# Search Alert Severity

Search for alert severity based on the search criteria.


## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| expression         | Optional    | String   | The query expression, which supports sql-like query. The fields that are supported for query include: `severityId`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)|
| pagination     | Optional     | Pagination Request Struct    | Lists the paging requirements in a request. If not specified, 10 entries are displayed per page, sorted in descending order by `updateTime`. Alternatively, you can specify `severityId` as the sorting criterion. For more details, see [Pagination Request Struct](/docs/api/en/2.1.0/overview.html#pagination-request-struct). |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Array of AlertSeverity Structs | A list of the alert severities. For details of an alertSeverity struct, see [AlertSeverity Struct](/docs/api/en/2.1.0/event/search_alert_severity.html#alertseverity-struct-alertseverity).|

### AlertSeverity Struct <alertseverity>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| severityId        | String                | The alert severity ID.|
| orgId          | String                |  The organization ID which the asset belongs to. |
| severityDesc   | StringI18n            | The alert severity description. |
| tags        | Map           | User-defined tags. (The Key and Value are of String type.)|
| updatePerson        | String                | The name of the person who last updated the alert severity.|
| updateTime    | Long                | The time when the alert was last updated in UTC format. |



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-severities?action=search&orgId=yourOrgId
method: POST 
requestBody: 
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
      "defaultValue": null,
			"i18nValue": {
				"en_US": "Serious！！！",
				"zh_CN": "严重！！！"
			}
		},
		"tags": {
			"111": "2222"
		},
		"updatePerson": "yj_test_customer",
		"updateTime": 1559204166000,
    "source": null,
	}]
}
```

### Java SDK Sample

```java
public void testSearchAlertSeverity() {
    SearchAlertSeverityRequest request = new SearchAlertSeverityRequest();
    request.setOrgId("yourOrgId");
    Pagination pagination = new Pagination();
    pagination.setPageSize(1);
    pagination.setPageNo(1);
    Sorter sorter = new Sorter(field: "severityId", Sorter.Order.ASC);
    List < Sorter > sorterList = new ArrayList < > ();
    sorterList.add(sorter);
    pagination.setSorters(sorterList);
    request.setPagination(pagination);
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