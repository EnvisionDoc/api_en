# Search Alert Type

Search for alert types based on the search criteria.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-types/search?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| expression         | Optional    | String   | The query expression, which supports sql-like query. The fields that are supported for query include: `typeId` and `parentTypeId`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)|
| pagination     | Optional     | Pagination Request Struct    | Lists the paging requirements in a request. If not specified, 10 entries are displayed per page, sorted in descending order by `updateTime` by default. Alternatively, you can specify `typeId` or `parentTypeId` as the sorting criterion. For more details, see [Pagination Request Struct>>](/docs/api/en/2.1.0/overview.html#pagination-request-struct) |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data  | Array of AlertType Struct  | A list of the alert types. For details of an alertType struct, see [AlertType Struct](/docs/api/en/2.1.0/event/search_alert_type.html#alerttype-struct-alerttype). |

### AlertType Struct <alerttype>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| typeId        | String                | The alert severity ID.|
| typeDesc   | StringI18n            | The alert type description. |
| orgId          | String                |  The rganization ID which the asset belongs to.|
| parentTypeId        | String          | The alert type ID of the parent alert. |
| tags        | Map          | User-defined tags. (The Key and Value are of String type.)|
| updatePerson        | String                | The name of the person who last updated the alert severity.|
| updateTime    | Long                | The time when the alert was last updated in UTC format.



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-types?action=search&orgId=yourOrgId
method: POST 
requestBody:
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "typeId",
			"order": "DESC"
		}]
	},
  "action": "search"
}
```

### Return Sample

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
		"orgId": "yourOrgId",
		"typeDesc": {
			"i18nValue": {
        "defaultValue": null,
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

## Java SDK Sample

```java
public void testSearchAlertType() {
    SearchAlertTypeRequest request = new SearchAlertTypeRequest();
    request.setOrgId(orgId);
    Pagination pagination = new Pagination();
    pagination.setPageNo(1);
    pagination.setPageSize(1);
    List < Sorter > sorterList = new ArrayList < > ();
    sorterList.add(new Sorter("typeId", Sorter.Order.DESC));
    pagination.setSorters(sorterList);
    request.setPagination(pagination);
    try {
        SearchAlertTypeResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url("https://{apigw-address}")
            .getResponse(request, SearchAlertTypeResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```