# Create Asset Tree and Associate Asset

Create an asset tree and associate an existing asset (device asset or logical asset) as the root node of the asset tree.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=associate
```

## Request Parameters (URI)

.. note:: In the following non-mandatory fields, you must provide ``assetId`` or a combination of ``productKey`` and ``deviceKey`` to specify the device.

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
     - Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)
   * - assetId
     - Query
     - false
     - String
     - ID of the asset to be associated: <br>If the ``assetId`` is specified, the asset uniquely identified by the ``assetId`` will be associated. `How to get Asset ID </docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__ <br>If the ``assetId`` is not specified, the asset uniquely identified by the combination of ``productKey`` and ``deviceKey`` will be associated.
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
     - Created asset tree ID


## Sample 1

### Request Sample

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=associate&orgId=yourOrgId&assetId=N5VpI5f9
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
    "data": "cRUdS7sJ"
}
```
