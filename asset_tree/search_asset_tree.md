# Search Asset Tree



Search for eligible asset trees based on tags.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |

## Request parameters (body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| filter| false         | Filter structure          | The criterion that the asset tree needs to meet. The search for tags is supported." filter": {  "tags": { "foo": "bar", "hello": "world" }  }  By default, all the asset trees under the OU are returned. See [Filter Structure] (/docs/api/en/latest/asset_tree/search_asset_tree.html#filter-filterstruc)   |
| pagination| false         |  Pagination request structure | Used to describe paging requirements in an interface request. By default, it is in the first page and the pagination size is 100. [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |
| projection| false         | String Array          | For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|


### Filter structure <filterstruc>

| Name | Data Type | Description |
|-----------|------------------------------------|-----------------------|
| tags| Map (Key is of String type, and the value is of String type) | A group of user-customized tags  |


## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| treeId| String                            | Asset tree ID                    |
| tags| Tag structure | A group of user-customized asset tree tags  |
| asset| asset structure                    | Root asset of asset tree              |



## Sample 1

### Request sample

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

### Return sample

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

