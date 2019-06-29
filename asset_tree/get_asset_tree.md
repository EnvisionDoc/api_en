# Get Asset Tree

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取指定OU下的一棵资产树。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=get
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要获取的资产树ID。[如何获取资产树信息ID](/docs/api/en/latest/api_faqs#id)        |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| treeId| String                            | 资产树ID                    |
| tags| Map（Key为String，Value为String） | 用户自定义的一组资产树标签  |
| asset| asset结构体                   | 资产树的根资产，见[asset结构体](/docs/api/en/latest/asset_tree/get_asset_tree.html#asset-assetstruc)              |

### Asset结构体<assetstruc>

| 名称  |  数据类型      | 描述               |
|-------|-------|---------------------------|
| assetId |  String | 资产ID|
|modelId|String|资产所属模型ID|
|modelIdPath|String|模型ID的路径。|
| name | StringI18n |支持国际化的资产名称|
|timezone  |  String  |资产所属时区|
| description | String | 资产描述|
| label  | String | 资产类型：“0”表示设备资产，“1”表示逻辑资产|
| inValid  | Boolean | true为无效节点，false为有效节点|
|attributes   |Map（Key为String，Value为Object）  |资产所属的模型属性|
|tags|Map<br>（Key为String, Value为String）|用户自定义标签|



## 示例 1

### 请求示例

```
GET
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?treeId=BRIt3ee3&action=get&orgId=o15541858646501
```

### 返回示例

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "f3c1ffc7-cc8e-4a50-ad40-0fa7b0c3a7ac",
 "data": {
  "treeId": "BRIt3ee3",
  "tags": {
   "user": "zm",
   "user0": "lily"
  },
  "asset": {
   "inValid": false,
   "assetId": "nlw68lR5",
   "modelId": "model_0422",
   "modelIdPath": "/model_0422",
   "name": {
    "defaultValue": "0430343",
    "i18nValue": {
     "en_US": "0430343"
    }
   },
   "timezone": "+08:00",
   "description": null,
   "label": "1",
   "attributes": {},
   "tags": {
    "tree": "0430"
   }
  }
 }
}
```

