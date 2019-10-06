# Search Asset Tree



Search for eligible asset trees based on tags.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |

## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| filter| false         | Filter struct          | The criterion that the asset tree needs to meet. The search for tags is supported. "filter": {  "tags": { "foo": "bar", "hello": "world" }  }  By default, all the asset trees are returned. See [Filter Struct](/docs/api/en/latest/asset_tree/search_asset_tree.html#filter-struct-filterstruc)   |
| pagination| false         |  Pagination request struct | Used to describe paging requirements in an interface request. By default, it is in the first page and the pagination size is 100. [Pagination Request Struct](/docs/api/en/latest/overview.html#pagination-request-struct) |
| projection| false         | String Array          | For details, see [How does projection crop the result set>>](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|


### Filter Struct <filterstruc>

| Name | Data Type | Description |
|-----------|------------------------------------|-----------------------|
| tags| Map (Key is of String type, and the value is of String type) | A group of user-customized tags  |


## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| treeId| String                            | Asset tree ID                    |
| tags| Tag struct | A group of user-customized asset tree tags  |
| asset| asset struct                    | Root asset of the asset tree              |



## Sample 1

### Request Sample

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search&orgId=o15541858646501
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

### Return Sample

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

