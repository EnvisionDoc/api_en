# Search Asset Node

*Note: This documentation is in the progress of translation. Thanks for your visit!*

查询OU下满足条件的资产。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)  |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------------|---------------|-------------------|-----|
| filter| false         |   Filter结构体        | 资产的查询条件，见[Filter结构体](/docs/api/en/latest/asset_tree/search_asset_node.html#filter-filterstruc) |
| pagination| false         | Pagination请求结构体  | 用于在接口请求中描述分页要求，见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)  |
| projection| false         | String Array          | 用于在接口请求中描述待返回的对象projection，见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection)|


### Filter结构体<filterstruc>

| 名称      | 是否必须  | 数据类型 | 描述      |
|-----------|---------------|----|--------------|
| assetIds| False | String Array | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)|
| modelIds | False | String Array | 资产所属模型ID。如果想查询多个模型，就提供多个模型ID组成的List。[如何获取modelId信息](/docs/api/en/latest/api_faqs.html#modeid-modeid) |
| rootModelIds | False | String Array | 资产所属的根模型ID。如果想查询多个根模型，就提供多个根模型ID。|
| nameLike | False | nameLike结构体 | 用于描述对国际化名称的查询条件，见[nameLike结构体](/docs/api/en/latest/asset_tree/search_asset_node.html#namelike-namelikestruc) |
| attributes  | False|Map |资产所属的模型属性。详情请见 [attributes的表示方法](/docs/api/en/latest/api_faqs.html#attributes) |
| tags | False | Tag结构体 | 用户自定义的一组标签 |
| treeId | False | String | 资产关联的资产树ID |


### nameLike结构体<namelikestruc>

| 名称        | 数据类型 | 描述      |
|-----------|---------------------|-----------------------|
| value        | String     | 待查询的名称或名称片段|
| locale         | String     | 指定的locale，如zh_CN|


## 响应参数

| 名称 |数据类型  | 描述 |
|-----------|------------------|------------------|
| data      | Asset结构体Array |  asset的列表    |




## 示例 1

### 请求示例

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset&orgId=1c499110e8800000
{
 "filter": {
  "attributes": {
   "starsystem": "Solar System"
  }
 },
"projection": ["attributes", "assetId", "name"]
}
```

### 返回示例

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "cf08e75c-325a-429f-bdb9-ec5d6a1250d7",
    "pagination": {
       "pageNo": 1,
       "pageSize": 10,
       "totalSzie": 10,
       "sortedBy": null
    },
    "data": [{
       "assetId": "f1Y6KiOr",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "WHIFQDEZ",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "TdqGOisO",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "T9VewFFA",
       "name": {
           "i18nValue": {},
           "defaultValue": "venus"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "NU3EbpXK",
       "name": {
           "i18nValue": {},
           "defaultValue": "1559140566137"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "9AE1XYBl",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "ZPuCIbDw",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }]
}
```

