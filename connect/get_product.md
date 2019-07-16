# Get Product



Get product details via `productKey`.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/products?action=get
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| productKey        | Query            | true    | String    | Product Key identifier|


## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | Product structure | Product-specific information; see [Product Structure](/docs/api/en/latest/connect/get_product.html#product-productstruc)                |


### Product structure <productstruc>

| Name | Data Type | Description |
|-------|-------|---------------------------|
| orgId |  String | Organization ID which the asset belongs to |
| productKey          | String| Product Key identifier                                            |
| productName         | StringI18n |  Product name. For the structure, see [Internationalized name structure](/docs/api/en/latest/api_faqs.html#internationalized-name-structure)  |
| productSecret       | String                          | Product private key                                             |
| productDesc         | String                          | Product Description                                             |
| productType         | Sting                           | Product type; Device stands for common product types, while Gateway stands for gateway types.   |
| dataFormat         | String                          | Data type; Custom represents the user-defined data type, while Json represents the json data type. |
| productTags         | Map (Key is of String type and the value is of String type) | Product tags                                             |
| modelId             | String                          | Model ID which the asset belongs to|
| dynamicActiveEnable | Boolean                         | Dynamic activation supported or not                                     |
| biDirectionalAuth   | Boolean                         | Two-way authentication supported or not                                     |
| createTime      | Long                            | Creation time                                             |
| createBy        | String                          | Creator                                               |
| updateTime       | Long                            | Update time                                             |
| updateBy       | String                          | Updater                                               |

## Error Codes

| Code| Data Type | Description |
|------------|----------------|-------------------|
| 11611 |                | `productKey` does not exist




## Sample 1

### Request Sample

```
GET:  /connect-service/v2.1/products?action=get&orgId=abc&productKey=def
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"345e68bc-e98a-45b1-a931-d255a6336847",
	"data" :{
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
		"productTags":{

		},
		"modelId":"AlterTest0615",
		"dynamicActiveEnable":false,
		"biDirectionalAuth":true
	}
}
```

