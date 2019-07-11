# Create Product

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Create products.

## Request format

```
https://{apigw-address}/connect-service/v2.1/products?action=create
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| productDesc       | False     | String       | Product Description                                                         |
| biDirectionalAuth | True      | Boolean      | Dual-way authentication supported or not                                                  |
| modelId           | True      | String      | Model ID which the asset belongs to. [How to get modelId information] (/docs/api/en/latest/api_faqs#how-to-get-modeid-information-modeid)   |
| dataFormat        | True      | String      | Data Type. Enumeration; Custom represents the user-defined data type, while Json represents the json data type. |
| productName       | True      | StringI18n | Product Name                                                           |
| productType       | True      | String      | Product Type. Enumeration; Device stands for common product types, while Gateway stands for gateway types. |



## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| String                           | Key of the created product               |


## Error codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11699|                       |ModelId does not exist              |

## Sample 1

### Request sample

```
POST:  /connect-service/v2.1/products?action=create&orgId=xxx
{
	"productDesc":"openapi_sdk_create_test",
	"biDirectionalAuth":false,
	"modelId":"AlterTest0615",
	"dataFormat":"Custom",
	"productName":{
		"defaultValue":"AlterTest0615_Product",
		"i18nValue":{}
	},
	"productType":"Device"
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

