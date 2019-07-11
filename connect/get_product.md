# Get Product



Get product details via `productKey`.

## Request format

```
https://{apigw-address}/connect-service/v2.1/products?action=get
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| productKey        | Query            | true    | String    | Product Key|


## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | Product structure | Product-specific information; see [Product Structure] (/docs/api/en/latest/connect/get_product.html#product-productstruc)                |


### Product structure <productstruc>

| Name | Data Type | Description |
|-------|-------|---------------------------|
| orgId |  String | Organization ID which the asset belongs to |
| productKey          | String| Product name                                            |
| productName         | StringI18n |  Product name. For the structure, see [Internationalized name structure](/docs/api/en/latest/api_faqs.html#internationalized-name-structure)
                                            |
| productSecret       | String                          | Product private key                                             |
| productDesc         | String                          | Product Description                                             |
| productType         | Sting                           | Product type; Device stands for common product types, while Gateway stands for gateway types.   |
| dataFormat         | String                          | Data type; Custom represents the user-defined data type, while Json represents the json data type. |
| productTags         | Map (Key is of String type and the value is of String type) | Product tags                                             |
| modelId             | String                          | Model ID which the asset belongs to|
| dynamicActiveEnable | Boolean                         | Dynamic activation supported or not                                     |
| biDirectionalAuth   | Boolean                         | Dual-way authentication supported or not                                     |
| createTime      | Long                            | Creation time                                             |
| createBy        | String                          | Creator                                               |
| updateTime       | Long                            | Update time                                             |
| updateBy       | String                          | Updater                                               |

## Error codes

| Code| Data Type | Description |
|------------|----------------|-------------------|
| 11611 |                | `productKey` does not exist




## Sample 1

### Request sample

```
GET:  /connect-service/v2.1/products?action=get&orgId=abc&productKey=def
```

### Return sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"345e68bc-e98a-45b1-a931-d255a6336847",
	"data" :{
		"orgId":"o15475450989191",
		"productKey":"atC41UIe",
		"productName":{
			"defaultValue":"openapi_sdk_8",
			"i18nValue":{}
		},
		"productSecret":"1uhl4Gwx9X8",
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

