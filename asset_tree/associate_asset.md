# Associate Asset

*Note: This documentation is in the progress of translation. Thanks for your visit!*

将指定已有资产节点关联到资产树上。待关联的资产可以是一个设备资产，也可以是一个逻辑资产。如果待关联的资产节点是一个设备资产，可使用设备资产的`ProductKey`、`DeviceKey`来描述，如果待关联的资产节点是一个逻辑资产，可使用逻辑资产的ID来描述。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=associateAsset
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要获取的资产树ID。[如何获取资产树信息ID](/docs/api/en/latest/api_faqs#id)        |
| parentAssetId | Query            | true    | String    | 待关联资产的父资产ID。 |
| assetId  | Query            | false    | String    | 待关联的资产ID，当存在`assetId`时，以`assetId`为准，当`assetId`不存在时，则看`productKey`，`deviceKey`。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)  |
| productKey  | Query            | false    | String    | 待关联的设备ProductKey。 |
| deviceKey  | Query            | false    | String    | 待关联的设备DeviceKey。 |



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data| String                            | 关联成功的资产ID              |


##错误码

| 代码 | 描述    |
|-----------|-----------------------------|
| 17751 | Tree ID 不存在              |
| 17752| 父资产不存在该树上          |
| 17758 | 资产已存在该树上            |
| 17760 | 欲创建的资产名称不合法      |
| 17770| 该树超过最高层数限制（7层） |



## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset- 
nodes?action=associateAsset&orgId=o15589291276361&treeId=KRAceqRA&parentAssetId=LGRCJVDc&productKey=UwXL9jmm&deviceKey=eacdsz9IGJ
```

### 返回示例

```json
{ 
    "code": 0, 
    "msg": "ok", 
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f", 
    "data": "cRUdS7sJ" 
} 
```

