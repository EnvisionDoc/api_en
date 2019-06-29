# Create Asset and Associate Node

*Note: This documentation is in the progress of translation. Thanks for your visit!*

创建一个逻辑资产，并关联到资产树上。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=createAsset
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要获取的资产树ID。[如何获取资产树信息ID](/docs/api/en/latest/api_faqs#id)        |
| parentAssetId | Query            | true    | String    | 待关联资产的父节点的资产ID。 |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|------------|---------------|----------------|--------------------------------|
| asset| true          | Asset结构体    | 创建资产时需要提供的资产详情，见[Asset结构体](/docs/api/en/latest/asset_tree/create_asset_and_associate_node.html#asset-assetstruc)   |


### Asset结构体<assetstruc>

| 名称  | 是否必须  |  数据类型      | 描述    |
|-------|-------|-------------|--------------|
|modelId|true|String|资产所属模型ID。[如何获取modelId信息](/docs/api/en/latest/api_faqs.html#modeid-modeid)|
| name |true| StringI18n |支持国际化的资产名称。结构请见[国际化名称结构体](/docs/api/en/latest/api_faqs.html#id3) |
|timezone  |true|  String  |资产所属时区。<br>使用+08:00格式表示不支持夏令时的时区。<br>使用Asia/Shanghai格式表示支持夏令时的时区。<br>详情请见[时区表示方法](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#id4) |
|description |false|String|资产描述 |
|attributes  |false  |Map（Key为String，Value为Object）  |资产所属的模型属性。详情请见 [attributes的表示方法](/docs/api/en/latest/api_faqs.html#attributes) |
|tags |false|Tag结构体|用户自定义标签，详情请见[标签的作用与表示方法](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#id6)|



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data| String                            | 创建的资产ID                   |


## 错误码

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
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?treeId=lMAXwaLX&action=createAsset&parentAssetId=fy4hxezF&orgId=1c499110e8800000
{ 
    "asset": { 
        "modelId": "STRING-INVERTER-MODEL", 
        "name": { 
            "defaultValue": "逆变器 #1", 
            "i18nValue": { 
                "en_US": "Inverter #1" 
            } 
        }, 
        "timezone": "+08:00", 
        "description": "This is a sampled asset.", 
        "attributes": { 
            "foo": 100, 
            "bar": "example" 
        }, 
        "tags": { 
            "foo": "bar", 
            "hello": "world" 
        } 
    } 
}
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

