# Search Related Asset Node

*Note: This documentation is in the progress of translation. Thanks for your visit!*

查询指定资产树上的资产，指定相对于某个已知资产的关系作为查询条件。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchRelatedAsset
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| treeId        | Query            | true    | String    | 需要获取的资产树ID。[如何获取资产树信息ID](/docs/api/en/latest/api_faqs#id)        |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------------|---------------|-------------------|-----|
| filter| false         |   Filter结构体       | 资产的查询条件<br>所有的条件都是可选的<br>所有指定的条件之间都是“与”关系，即待查询的资产必须同时满足所有指定的条件<br>4个关系查询条件至多提供一个，见[Filter结构体](/docs/api/en/latest/asset_tree/search_related_asset_node.html#filter-filterstruc)   |
| pagination| false         | Pagination请求结构体  | 用于在接口请求中描述分页要求。默认第一页，分页大小100，见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)                               |
| projection| false         | Projection结构体          | 用于在接口请求中描述待返回的对象projection。详见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection)|


### Filter结构体<filterstruc>

| 名称      | 是否必须  | 数据类型 | 描述      |
|-----------|---------|--------|-----------------------|
| assetIds                   | String Array   | false    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)|
| modelIds            | String Array   | false    | 资产所属模型ID。[如何获取modelId信息](/docs/api/en/latest/api_faqs.html#modeid-modeid) |
| rootModelIds         | String Array   | False    | 资产所属的根模型ID。如果想查询多个根模型，就提供多个根模型ID              |
| isParentOfAssetId     | String         | false    | 待查询的资产是指定资产的直接父节点  值为指定资产的资产ID<br>[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1)  |
| isChildOfAssetId      | String         | false    | 待查询的资产是指定资产的直接子节点  值为指定资产的资产ID<br>[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1)  |
| isAncestorOfAssetId   | String         | false    | 待查询的资产是指定资产的祖先节点  值为指定资产的资产ID<br>[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1)   |
| isDescendantOfAssetId| String         | false    | 待查询的资产是指定资产的子孙节点  值为指定资产的资产ID<br>[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1)   |


## 响应参数

| 名称 |数据类型  | 描述 |
|-----------|------------------|------------------|
| data      | Asset结构体 |  asset的列表    |



## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?treeId=k6wweMTP&action=searchRelatedAsset&orgId=o15517683199241
{
 "filter": {
  "isChildOfAssetId": "4R6PbfVj"
 },
"projection": ["attributes", "assetId", "name"]
}
```

### 返回示例

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "153ad7a2-2ec1-41b0-b750-e4ea2ce2786c",
 "data": 
      [{
   "assetId": "8byS3cuc",
   "name": {
    "i18nValue": {},
    "defaultValue": "ycmdevice_1"
   },
   "attributes": {}
  }, {
   "assetId": "Fq5M1Y6E",
   "name": {
    "i18nValue": {},
    "defaultValue": "ycmdevice_3"
   },
   "attributes": {}
  }, {
   "assetId": "nPQUW0Nr",
   "name": {
    "i18nValue": {
     "en_US": "Rebecca_testSiteAPI3"
    },
    "defaultValue": "Rebecca_testSiteAPI3"
   },
   "attributes": {}
  }, {
   "assetId": "oLrrH1uz",
   "name": {
    "i18nValue": {},
    "defaultValue": "Rebecca_Service1"
   },
   "attributes": {}
  }, {
   "assetId": "vuT6x3Xl",
   "name": {
    "i18nValue": {},
    "defaultValue": "ycmdevice_2"
   },
   "attributes": {}
  }],
    “pagination” : {
      "pageNo": 1,
      "pageSize": 10，
      "totalSzie": 10,
    "sortedBy":null
} 
}
```

