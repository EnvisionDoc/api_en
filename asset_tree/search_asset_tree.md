# Search Asset Tree

*Note: This documentation is in the progress of translation. Thanks for your visit!*

根据tags搜索符合条件的资产树。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |

## 请求参数（body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------------|---------------|-------------------|-----|
| filter| false         | Filter结构体          | 资产树需要满足的条件。支持对tags的搜索。"filter": {  "tags": { "foo": "bar", "hello": "world" }  }  缺省则返回OU下所有的资产树，见[Filter结构体](/docs/api/en/latest/asset_tree/search_asset_tree.html#filter-filterstruc)   |
| pagination| false         |  Pagination请求结构体 | 用于在接口请求中描述分页要求。默认第一页，分页大小100。[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)                               |
| projection| false         | String Array          | 详见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection)|


### Filter结构体<filterstruc>

| 名称        | 数据类型 | 描述      |
|-----------|------------------------------------|-----------------------|
| tags| Map（Key为String，Value为String）  | 用户自定义的一组标签  |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| treeId| String                            | 资产树ID                    |
| tags| Tag结构体 | 用户自定义的一组资产树标签  |
| asset| asset结构体                     | 资产树的根资产              |



## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search&orgId=o15541858646501
{
"filter": {
  "tags": {}
},
"pagination": {
  "pageNo": 1,
  "pageSize": 3
},
"action": "search",
"projection": ["asset"]
}
```

### 返回示例

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "82248518-6da4-49d2-8d07-cf7a0ff55b60",
 "data": 
[{
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
   }],
"pagination" : {
      "pageNo": 1,
      "pageSize": 10，
      "totalSzie": 10,
    "sortedBy":null
  }
}
```

