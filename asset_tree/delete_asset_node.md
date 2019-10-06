# Delete Asset Node



Remove an asset node from the asset tree. The asset to be removed can be a device asset or a logical asset. If the asset node to be removed is a device asset, it can be described by using "Product Key" and "Device Key" of the device asset. If the asset node to be removed is a logical asset, it can be described by the ID of the logical asset.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=delete

```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree to be gotten. [How to get the ID of an asset tree>>](/docs/api/en/latest/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |
| assetId  | Query            | false    | String    | ID of the asset to be removed (used to identify the logical asset). When there is an `assetId`, the `assetId` will prevail, and when the `assetId` does not exist, the `productKey` and `deviceKey` will prevail. [How to get assetId>>](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)  |
| productKey  | Query            | false    | String    | Product Key of the asset to be removed (used to identify the device asset).|
| deviceKey  | Query            | false    | String    | Device Key of the asset to be removed (used to identify the device asset). |


## Error Codes

| Code | Description    |
|-----------|-----------------------------|
| 17751| Tree ID does not exist                                                 |
| 17756| This tree does not exist for this asset                                               |
| 17764| The root node cannot be deleted                                               |
| 17766| Any non-leaf node cannot be deleted                                               |
| 17762| Only one user can modify the asset tree at a time. The asset tree cannot be operated temporarily. Request later. |




## Sample 1

### Request Sample

```
POST https://apigw-address/asset-tree-service/v2.1/asset-nodes/delete?treeId=BRIt3ee3&action=delete&orgId=o15541858646501 
{"assetId":"AdqP8rZ0"} 
```

### Return Sample

```json
{ 
  "code": 0, 
  "msg": "ok", 
  "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f" ,
  "data": null
} 
```

