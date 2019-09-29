# Search Product



 Search for products that meet the criteria.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/products?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| productKey        | Query            | true    | String    | Product Key|


## Request Parameters (Body)

| Name            | Required or Not | Data Type | Description |
|-------------------|----------|-----------|--------------|
| expression         | false    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `productKey` and `modelId`. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". [How to use expression>>](/docs/api/en/2.0.9/api_faqs.html#how-to-use-expression)|
| pagination     | false     | String   | Paging parameter. When not specified, 10 entries are displayed per page by default. See [Pagination Request Struct>>](/docs/api/en/2.0.9/overview.html#pagination-request-struct) |


## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| Product struct                           | Product list from query, see [Product Struct>>](/docs/api/en/2.0.9/connect/get_product.html#product-struct-productstruc)                |




## Sample 1

### Request Sample

```
POST: /connect-service/v2.1/products?action=search&orgId=abc 
{
	"expression":"modelId=\"AlterTest0615\"",
	"pagination":{
		"pageNo":1,
		"pageSize":5
	}
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"a82752bb-9eb0-4cd5-b0c6-0c1aeb35f6d2",
	"data":[
		{
			"orgId":"yourOrgId",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"openapi_sdk_8",
				"i18nValue":{}
			},
			"productSecret":"yourProductSecret",
			"productDesc":"test_sdk_update",
			"productType":"Device",
			"dataFormat":"Custom",
			"productTags":{},
			"modelId":"AlterTest0615",
			"dynamicActiveEnabled":false,
			"biDirectionalAuth":true
		},
		{
			"orgId":"yourOrgId",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"AlterTest0615_Product",
				"i18nValue":{}
			},
			"productSecret":"yourProductSecret",
			"productDesc":"",
			"productType":"Device",
			"dataFormat":"Json",
			"productTags":{},
			"modelId":"AlterTest0615",
			"dynamicActiveEnabled":false,
			"biDirectionalAuth":false
		}
	],
	"pagination":{
		"sortedBy":null,
		"pageNo":1,
		"pageSize":5,
		"totalSize":2
	}
}
```

