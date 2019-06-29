# Disable Device

*Note: This documentation is in the progress of translation. Thanks for your visit!*

禁用设备。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=disable
```

## 请求参数（URI）

注：以下字段必须提供`assetId`或者`(productKey, deviceKey)`。

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| assetId  | Query            | String   | False         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid) |
| productKey | Query            | String  | False          | Product Key      |
| deviceKey | Query            | String   | False         | 设备key          |
    


## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11794 |                | 要禁止的设备已处于禁用状态                |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=disable&orgId=o15475450989191&assetId=9HhK0YxX
method: POST
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "b3f22f9b-d90d-4bf2-9e97-79162a3d1dff",
	"data": null
}
```

