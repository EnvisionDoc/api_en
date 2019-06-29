# Get Product

*Note: This documentation is in the progress of translation. Thanks for your visit!*

通过`productKey`获取product的详细信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/products?action=get
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| productKey        | Query            | true    | String    | Product Key|


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data| Product结构体                           | Product的具体信息，见[Product结构体](/docs/api/en/latest/connect/get_product.html#product-productstruc)                |


### Product结构体<productstruc>

| 名称  |  数据类型      | 描述               |
|-------|-------|---------------------------|
| orgId |  String | 资产所属的组织ID |
| productKey          | String| 产品名称                                             |
| productName         | StringI18n |  产品名称。结构请见[国际化名称结构体](/docs/api/en/latest/api_faqs.html#id3)
                                            |
| productSecret       | String                          | 产品私钥                                             |
| productDesc         | String                          | 产品描述                                             |
| productType         | Sting                           | 产品类型，Device代表普通类型，Gateway代表网关类型    |
| dataFormat         | String                          | 数据类型，Custom代表用户自定义类型，Json代表json类型 |
| productTags         | Map（key为String，value为String） | 产品标签                                             |
| modelId             | String                          | 资产所属模型ID|
| dynamicActiveEnable | Boolean                         | 是否支持动态激活                                     |
| biDirectionalAuth   | Boolean                         | 是否支持双向认证                                     |
| createTime      | Long                            | 创建时间                                             |
| createBy        | String                          | 创建人                                               |
| updateTime       | Long                            | 更新时间                                             |
| updateBy       | String                          | 更新人                                               |

## 错误码

| 代码  | 数据类型 | 描述 |
|------------|----------------|-------------------|
| 11611 |                | `productKey`不存在 |




## 示例 1

### 请求示例

```
GET: /connect-service/v2.1/products?action=get&orgId=abc&productKey=def
```

### 返回示例

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

