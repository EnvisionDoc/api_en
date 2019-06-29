# Update Product

*Note: This documentation is in the progress of translation. Thanks for your visit!*

更新产品。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/products?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| productKey         | Query            | true     | String    | Product Key |


## 请求参数（Body）

| 名称         | 是否必须 | 数据类型 | 描述      |
|-------------------|----------|-----------|--------------|
| productDesc       | False     | String       | 产品的描述                                                         |
| biDirectionalAuth | True      | Boolean      | 是否支持双向认证                                                   |
| dynamicActivateEnabled           | False      | String      | 是否支持动态激活|
| productName        | False      | String      | 数据类型。枚举，Custom代表用户自定义数据类型，Json代表json数据类型。|
| productName       | True      | StringI18n | 产品名称，见[国际化名称结构体](/docs/api/en/latest/api_faqs.html#id3)                                                           |



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|---------------|------------|
| data | String                           | 更新的产品的key               |


## 错误码

| 代码| 数据类型 | 描述         |
|-------------|--------------|-------------|
| 11651 |                       | Productkey不存在              |

## 示例 1

### 请求示例

```
POST: /connect-service/v2.1/products?action=update&orgId=xxx&productKey=xxx
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

### 返回示例

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"522d0269-445d-4f13-be04-1424e0e2893e",
	"data":"2zp6A70r"
}
```

