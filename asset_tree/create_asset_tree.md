# Create Asset Tree

Create an asset tree as well as its root node.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=create
```

## Request Parameters (URI)

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
     - Organization ID which the asset belongs to. `How to get orgId </docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid>`__




## Request Parameters (Body)

.. list-table::

   * - Name
     - Required or Not
     - Data Type
     - Description
   * - asset
     - true
     - Asset struct
     - Details required when creating an root node asset. See `Asset Struct <create_asset_tree.html#asset-struct-assetstruc>`__

### Asset Struct <assetstruc>

.. list-table::

   * - Name
     - Required or Not
     - Data Type
     - Description
   * - name
     - true
     - StringI18n
     - Asset name that supports internationalization. For the structure, see `Internationalized name struct </docs/api/en/2.0.9/api_faqs.html#internationalized-name-struct>`__
   * - timezone
     - true
     - String
     - Timezone where the asset is located. <br>Use the "+08:00" format to indicate time zones that do not support daylight saving time. <br>Use the Asia/Shanghai" format to indicate time zones that support daylight saving time. <br>For details, see `Timezone representation </docs/api/en/2.0.9/api_faqs.html#timezone-representation>`__
   * - description
     - false
     - String
     - Asset description
   * - attributes
     - false
     - Map  (Key is of String type, and the Value is of object type)
     - Attributes of the model which the asset belongs to. For details, see `attributes representation </docs/api/en/2.0.9/api_faqs.html#attributes-representation>`__
   * - tags
     - false
     - Tag struct
     - User-customized tags. For details, see `How to use tag </docs/api/en/2.0.9/api_faqs.html#how-to-use-tag>`__



## Response Parameters

.. list-table::

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - Created asset tree ID.



## Sample 1

### Request Sample

```
POST
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=create&orgId=yourOrgId

{"asset":{
    "modelId": "eeeewqqw",
    "name": {
        "defaultValue": "hahah"
    },
    "timezone": "+12:00",
    "attributes":{},
    "description": "test example by tj"
}
}
```

### Return Sample

```json
{
  "msg":  "OK",
  "code": 0,
  "data": "HfzFPn1H",
  "requestId": "bb4f8c40-604a-451e-83bd-99cfba6bd53e"
}
```
