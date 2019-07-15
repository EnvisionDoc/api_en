# Create Product



Create products.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/products?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| productDesc       | False     | String       | Product Description                                                         |
| biDirectionalAuth | True      | Boolean      | Dual-way authentication supported or not                                                  |
| modelId           | True      | String      | Model ID which the asset belongs to. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)   |
| dataFormat        | True      | String      | Data Type. Enumeration; Custom represents the user-defined data type, while Json represents the json data type. |
| productName       | True      | StringI18n | Product Name                                                           |
| productType       | True      | String      | Product Type. Enumeration; Device stands for common product types, while Gateway stands for gateway types. |



## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| String                           | Key of the created product               |


## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11699|                       |ModelId does not exist              |

## Sample 1

### Request Sample

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

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"522d0269-445d-4f13-be04-1424e0e2893e",
	"data":"2zp6A70r"
}
```

