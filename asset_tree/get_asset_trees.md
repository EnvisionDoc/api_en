# Get Asset Trees

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Search assets tree as per a group of `assetId`. If `assetId` is not in the tree, then there is no such key in `data`.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=getAssetTree
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |

## Request parameters (Body)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| assetIds         | Query            | true     | String Array   | A group of asset ID (assetId), where at most 100 Ids are supported. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)   |
| projection         | Query            | false    | String Array   |Used to describe the object projection to be returned in the interface request. For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|


## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| Map (the Key is assetId and the Value is the AssetTree structure Array)   | List of assets and their asset trees. See [AssetTree structure](/docs/api/en/latest/asset_tree/get_asset_trees.html#id3) |


### AssetTree structure

| Name | Data Type | Description |
|-------|-------|---------------------------|
| treeId  |  String | Asset tree ID |
|tags|Map<String, String>|Root asset on the asset tree|



## Sample 1

### Request sample

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action= getAssetTree&orgId=o15541858646501
{
 "assetIds": ["BtsYmF2r", "qf1vsBQW"]
}
```

### Return sample

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

