# Delete Product

*Note: This documentation is in the progress of translation. Thanks for your visit!*

删除产品。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/products?action=delete
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| productKey         | Query            | true     | String    | Product Key |




## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|---------------------------|-----------------------------|
| data | String                           | 删除的产品的key               |


## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11651|                       |Productkey不存在              |
| 11619|                       |删除的product下存在设备             |

## 示例 1

### 请求示例

```
POST: /connect-service/v2.1/products?action=delete&orgId=xxx&productKey=xxx
```

### 返回示例

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"ef6a7fbb-0834-45fb-b1d4-6bd2dc25796f",
	"data":"atC41UIe"
}

```

