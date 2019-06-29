# Delete Asset Node

*Note: This documentation is in the progress of translation. Thanks for your visit!*

从资产树上移除一个资产节点。待移除的资产可以是一个设备资产，也可以是一个逻辑资产。如果待移除的资产节点是一个设备资产，可使用设备资产的`ProductKey`、`DeviceKey`来描述。如果待移除的资产节点是一个逻辑资产，可使用逻辑资产的ID来描述。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=delete

```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要获取的资产树ID。[如何获取资产树信息ID](/docs/api/en/latest/api_faqs#id)        |
| assetId  | Query            | false    | String    | 待移除的资产ID（用于识别逻辑资产）。当存在`assetId`时，以`assetId`为准，当`assetId`不存在时，则看`productKey`，`deviceKey`。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)  |
| productKey  | Query            | false    | String    | 待移除的设备ProductKey（用于识别设备资产）。 |
| deviceKey  | Query            | false    | String    | 待移除的设备DeviceKey（用于识别设备资产）。 |


##错误码

| 代码 | 描述    |
|-----------|-----------------------------|
| 17751| Tree ID 不存在                                                 |
| 17756| 资产不存在该树上                                               |
| 17764| 根节点不能被删除                                               |
| 17766| 非叶子节点不能被删除                                           |
| 17762| 一次只允许一个用户修改资产树，暂时不能操作该资产树，请再次请求 |




## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?treeId=BRIt3ee3&assetId=AdqP8rZ0&action=delete&orgId=o15541858646501
```

### 返回示例

```json
{ 
    "code": 0, 
    "msg": "ok", 
"requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f" ,
  "data": null
} 
```

