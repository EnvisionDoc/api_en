# Get Asset Trees

*Note: This documentation is in the progress of translation. Thanks for your visit!*

根据一组`assetId`搜索资产所在的资产树，若`assetId`不在树上，则`data`中无该key。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=getAssetTree
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |

## 请求参数（Body）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| assetIds         | Query            | true     | String Array   | 一组资产ID （assetId），最多100个。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)   |
| projection         | Query            | false    | String Array   | 用于在接口请求中描述待返回的对象projection。详见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection) |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data| Map（Key为assetId，Value为AssetTree结构体Array）   | 资产和其所在的资产树列表，见[AssetTree结构体](/docs/api/en/latest/asset_tree/get_asset_trees.html#id3) |


### AssetTree结构体

| 名称  |  数据类型      | 描述               |
|-------|-------|---------------------------|
| treeId  |  String | 资产树ID |
|tags|Map<String, String>|资产树上的根资产|



## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action= getAssetTree&orgId=o15541858646501
{
 "assetIds": ["BtsYmF2r", "qf1vsBQW"]
}
```

### 返回示例

```json
{ 
 "code": 0, 
 "msg": "OK", 
 "requestId": "82248518-6da4-49d2-8d07-cf7a0ff55b60", 
 "data": { 
 "BtsYmF2r" : [{ 
   "treeId" : "QafeaWe", 
   "tags" : { }, 
   "asset": { 
    "modelId": "NULLMODEL", 
    "assetId": "qf1vsBQW", 
    "timezone": "+08:00", 
    "name": { 
     "i18nValue": { 
      "en_US": "zmTree604111zzz" 
     }, 
     "defaultValue": "zmTree604" 
    }, 
    "description": "", 
    "attributes": {}, 
    "inValid": false, 
    "label": "1", 
    "modelIdPath": "/NULLMODEL", 
    "tags": {}  
   }]
 }
```

