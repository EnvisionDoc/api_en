# Associate Asset


Associate a specified existing asset node to the asset tree. The asset to be associated can be a device asset or a logical asset. If the asset node to be associated is a device asset, it can be described by using "Product Key" and "Device Key" of the device asset. If the asset node to be associated is a logical asset, it can be described by the ID of the logical asset.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=associateAsset
```

## Request Parameters (URI)

.. note:: In the following non-required fields, you must provide ``assetId`` or a combination of ``productKey`` and ``deviceKey`` to specify the device.

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

.. list-table::

   * - Name
     - Location (Path/Query)
     - Required or Not
     - Data Type
     - Description
   * - orgId
     - Query
     - true
     - String
     - Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)
   * - treeId
     - Query
     - true
     - String
     - ID of the asset tree to be gotten. [How to get the ID of an asset tree>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-the-id-of-an-asset-tree)
   * - parentAssetId
     - Query
     - true
     - String
     - Parent asset ID of the asset to be associated
   * - assetId
     - Query
     - false
     - String
     - Asset ID to be associated; when there is an `assetId`, the `assetId` will prevail, and when the `assetId` does not exist, the `productKey` and `deviceKey` will prevail. [How to get assetId>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-asset-id-assetid-assetid)
   * - productKey
     - Query
     - false
     - String
     - Product Key of the device to be associated
   * - deviceKey
     - Query
     - false
     - String
     - Device Key of the device to be associated



## Response Parameters

.. list-table::

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - Asset Id that associated successfully


## Error Codes

.. list-table::

   * - Code
     - Description
   * - 17751
     - Tree ID does not exist
   * - 17752
     - The parent asset does not exist in this tree
   * - 17758
     - The asset already exists on the tree
   * - 17760
     - The name of the asset to be created is illegal
   * - 17770
     - The tree exceeds the maximum number of layers (7 layers)



## Sample 1

### Request Sample

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-
nodes?action=associateAsset&orgId=o15589291276361&treeId=KRAceqRA&parentAssetId=LGRCJVDc&productKey=UwXL9jmm&deviceKey=eacdsz9IGJ
```

### Return Sample

```json
{
    "code": 0,
    "msg": "ok",
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
    "data": "cRUdS7sJ"
}
```
