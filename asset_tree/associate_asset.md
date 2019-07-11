# Associate Asset



Associate a specified existing asset node to the asset tree. The asset to be associated can be a device asset or a logical asset. If the asset node to be associated is a device asset, it can be described by using `ProductKey` and `DeviceKey` of the device asset. If the asset node to be associated is a logical asset, it can be described by the ID of the logical asset.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=associateAsset
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree to be gotten. [How to get asset tree ID](/docs/api/en/latest/api_faqs#id)        |
| parentAssetId | Query            | true    | String    | Parent asset ID of the asset to be associated.  |
| assetId  | Query            | false    | String    | Asset ID to be associated; when there is an 'assetId`, the `assetId` will prevail, and when the `assetId` does not exist, the `productKey` and `deviceKey` will prevail. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)  |
| productKey  | Query            | false    | String    | ProductKey of the device to be associated.  |
| deviceKey  | Query            | false    | String    | DeviceKey of the device to be associated.  |



## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| String                            | AssetId associated successfully              |


## Error codes

| Code | Description    |
|-----------|-----------------------------|
| 17751 | Tree ID does not exist              |
| 17752| The parent asset does not exist in this tree          |
| 17758 | The asset already exists on the tree            |
| 17760 | The name of the asset to be created is illegal      |
| 17770| The tree exceeds the maximum number of layers (7 layers) |



## Sample 1

### Request sample

```
https://{apigw-address}/asset-tree-service/v2.1/asset- 
nodes?action=associateAsset&orgId=o15589291276361&treeId=KRAceqRA&parentAssetId=LGRCJVDc&productKey=UwXL9jmm&deviceKey=eacdsz9IGJ
```

### Return sample

```json
{ 
    "code": 0, 
    "msg": "ok", 
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f", 
    "data": "cRUdS7sJ" 
} 
```

