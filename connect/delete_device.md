# Delete Device

*Note: This documentation is in the progress of translation. Thanks for your visit!*

删除设备。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=delete
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | 设备key          |




## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=delete&orgId=o15475450989191&assetId=mAEsF3sm
method: POST
headers: {}
requestBody: null
```

### 返回示例

```json
responseBody:{
"code":0,
"msg":"OK",
"requestId":"12d7e3be-6bac-43de-8733-7e02a4eb8a88",
"data":null
}
```

