# Search Related Asset Node



Query assets on the specified asset tree, and specify the relationship with a known asset as the query criterion.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchRelatedAsset
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree to be gotten. [How to get asset tree ID](/docs/api/en/latest/api_faqs#id)        |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| filter| false         |   Filter structure       | Asset query criteria. <br>All criteria are optional. <br>All the specified criteria are related with each other under the "and" relationship, that is, the assets to be queried must satisfy all the specified criteria at the same time. <br>At most one out of the 4 relational query criteria is allowed. See [Filter Structure](/docs/api/en/latest/asset_tree/search_related_asset_node.html#filter-filterstruc)   |
| pagination| false         |  Pagination request structure | Used to describe paging requirements in an interface request. By default, it is in the first page and the pagination size is 100. See [Pagination Request Structure](/docs/api/en/latest/overview.html?highlight=pagination#pagination)                               |
| projection| false         | Projection structure          | Used to describe the object projection to be returned in the interface request. For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|


### Filter structure <filterstruc>

| Name | Required or Not | Data Type | Description |
|-----------|---------|--------|-----------------------|
| assetIds                   | String Array   | false    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)|
| modelIds            | String Array   | false    | Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs.html#how-to-get-modeid-information-modeid)|
| rootModelIds         | String Array   | False    | Model ID which the asset belongs to. You should provide multiple root model IDs if you want to query multiple root models |
| isParentOfAssetId     | String         | false    | The asset to be queried is the immediate parent node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)  |
| isChildOfAssetId     | String         | false    | The asset to be queried is the immediate child node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)  |
| isAncestorOfAssetId     | String         | false    | The asset to be queried is the immediate ancestor node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)  |
| isDescendantOfAssetId | String         | false    | The asset to be queried is the immediate descendant node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)  |


## Response parameters

| Name | Data Type | Description |
|-----------|------------------|------------------|
| data      | Asset structure|  asset list    |



## Sample 1

### Request sample

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?treeId=k6wweMTP&action=searchRelatedAsset&orgId=o15517683199241
{
 "filter": {
  "isChildOfAssetId": "4R6PbfVj"
 },
"projection": ["attributes", "assetId", "name"]
}
```

### Return sample

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

