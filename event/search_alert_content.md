# Search Alert Content

Search for alert content based on the search criteria.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
                                                                 

## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId          | Optional    | String    | The model ID. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid)|
| alertTypeId  | Optional    | String               | The alert type ID.   |
| subAlertTypeId    | Optional    | String   | The alert sub-type ID.  |                       
| expression         | Optional    | String   | The query expression, which supports sql-like query. The fields that are supported for query include: `contentId`, `modelId`, and `alertTypeId`. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)|
| pagination     | Optional     | Pagination Request Struct    | Lists the paging requirements in a request. If not specified, 10 entries are displayed per page, sorted in descending order by `updateTime`. Alternatively, you can use the following field sorting criterion: `contentId`, `modelId`, `alertTypeId`, `subAlertTypeId`. For more details, see [Pagination Request Struct](/docs/api/en/2.1.0/overview.html#pagination-request-struct). |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | Array of AlertContent Structs | A list of the alert content. For details of an alertContent struct, see [AlertContent Struct](/docs/api/en/2.1.0/event/search_alert_content.html#alertcontent-struct-alertcontent).|

### AlertContent Struct <alertcontent>

| Name | Data Type     | Description          |
|----------------|-----------------------|----------|
| contentId| String           | The alert content ID.                 |
| contentDesc | StringI18n | The alert content description.     |
| modelId| String           | The model ID.                 |
| orgId          | String| The organization ID which the asset belongs to.|
| alertType  | AlertType Struct  | The details of the alert type. For more information, see [AlertType Struct>>](/docs/api/en/2.1.0/event/search_alert_type.html#alerttype-struct-alerttype)             |
| subAlertType| AlertType Struct  | The details of the alert sub-type.  For more information, see [AlertType Struct>>](/docs/api/en/2.1.0/event/search_alert_type.html#alerttype-struct-alerttype)           |
| tags| Map        | User-defined tags. (The Key and Value are of String type.) |
| updatePerson| String           | The name of the person who last updated the alert severity.           |
| updateTime| Long             | The time when the alert was last updated in UTC format.       |



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-contents?action=search&orgId=yourOrgId
method: POST 
requestBody: 
{
	"modelId": "ssss",
	"alertTypeId": "dateType",
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "contentId",
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
      "defaultValue": null,
			"i18nValue": {
				"en_US": "dateContentid desc",
				"zh_CN": ""
			}
		},
		"modelId": "ssss",
		"orgId": "yourOrgId",
		"updatePerson": "test_user",
		"updateTime": 1546612131000,
		"alertType": {
			"typeId": "dateType",
      "orgId": "o15724268424841",
      "parentTypeId": null,
      "updatePerson": null,
      "source":null,
			"typeDesc": {
				"i18nValue": {
          "defaultValue": null,
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
          "defaultValue": null,
					"en_US": "dateType desc",
					"zh_CN": ""
				}
			},
      "orgId": "o15724268424841",
      "parentTypeId": null,
      "updatePerson": null,
      "source":null,
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
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    SearchAlertContentRequest request = new SearchAlertContentRequest();
    request.setOrgId(orgId);
    request.setModelId("ssss");
    Pagination pagination = new Pagination();
    pagination.setPageNo(1);
    pagination.setPageSize(1);
    List < Sorter > sorterList = new ArrayList < > ();
    sorterList.add(new Sorter("contentId", Sorter.Order.DESC));
    pagination.setSorters(sorterList);
    request.setPagination(pagination);
    try {
        SearchAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, SearchAlertContentResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```