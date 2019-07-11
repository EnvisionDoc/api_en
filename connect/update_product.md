# Update Product

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Update products.

## Request format

```
https://{apigw-address}/connect-service/v2.1/products?action=update
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| productKey         | Query            | true     | String    | Product Key |


## Request parameters (Body)

| Name            | Required or Not | Data Type | Description |
|-------------------|----------|-----------|--------------|
| productDesc       | False     | String       | Product Description                                                         |
| biDirectionalAuth | True      | Boolean      | Dual-way authentication supported or not                                                  |
| dynamicActivateEnabled           | False      | String      | Dynamic activation supported or not|
| productName        | False      | String      | Data type. Enumeration; Custom represents the user-defined data type, while Json represents the json data type. |
| productName       | True      | StringI18n | Product name; see [Internationalized Name Structure](/docs/api/en/latest/api_faqs.html#id3)                                                           |



## Response parameters

| Name | Data Type | Description |
|-------------|---------------|------------|
| data | String                           | Key of the updated product               |


## Error codes

| Code| Data Type | Description |
|-------------|--------------|-------------|
| 11651 |                       | Productkey does not exist              |

## Sample 1

### Request sample

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

### Return sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"522d0269-445d-4f13-be04-1424e0e2893e",
	"data":"2zp6A70r"
}
```

