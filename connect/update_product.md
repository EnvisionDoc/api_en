# Update Product



Update products.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/products?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| productKey         | Query            | true     | String    | Product Key|


## Request Parameters (Body)

| Name            | Required or Not | Data Type | Description |
|-------------------|----------|-----------|--------------|
| productDesc       | False     | String       | Product Description                                                         |
| biDirectionalAuth | True      | Boolean      | Two-way authentication supported or not                                                  |
| dynamicActivateEnabled           | False      | String      | Dynamic activation supported or not|
| productName       | True      | StringI18n | Product name; see [Internationalized name struct>>](/docs/api/en/latest/api_faqs.html#internationalized-name-struct)                                                           |
|productTags|False|Map| Product tags |



## Response Parameters

| Name | Data Type | Description |
|-------------|---------------|------------|
| data | String                           | Key of the updated product               |


## Error Codes

| Code| Data Type | Description |
|-------------|--------------|-------------|
| 11651 |                       | `productkey` does not exist              |

## Sample 1

### Request Sample

```
POST:  /connect-service/v2.1/products?action=update&orgId=xxx&productKey=xxx
{
	"productDesc":"test_sdk_update",
	"biDirectionalAuth":true,
	"dynamicActivateEnabled":true,
	"productName": {
		"defaultValue":"AlterTest0615_Product",
		"i18nValue":{}
	}
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"522d0269-445d-4f13-be04-1424e0e2893e",
	"data":"2zp6A70r"
}
```

