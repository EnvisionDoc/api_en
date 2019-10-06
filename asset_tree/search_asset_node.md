# Search Asset Node



Query the assets that meet the conditions.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Required or Not
     - Data Type
     - Description
   * - expression
     - False
     - String
     - Query expression. The fields that are supported for query include: ``assetId``, ``modelId``, ``rootModelIds``, ``name``, ``attributes``, ``tags``, ``treeId``, ``productKey`` and ``deviceKey``.

       + ``assetId``, ``modelId``, and ``rootModelIds``: support arithmetic operators "=" and "in";
       + ``productType`` and ``deviceKey``: supports arithmetic operator "=" and fuzzy inquiry (like);
       + ``name``: supports fuzzy inquiry of specified language:

         * ``name like ‘xxx’``: fuzzy inquiry of default name, Chinese name, and English name
         * ``name.default like ‘xxx’``: fuzzy inquiry of default name
         * ``name.zh_CN like ‘xxx’``: fuzzy inquiry of Chinese name, if no Chinese name, fuzzy inquiry of default name
         * ``name.en_US like ‘xxx’``: fuzzy inquiry of English name, if no English name, fuzzy inquiry of default name

       `How to use expression </docs/api/en/latest/api_faqs.html#how-to-use-expression>`__

   * - pagination
     - False
     - pagination request struct
     - Random pagination. User can not specify the sorting field. If not provided, the default pagination size is 10 pages. `Pagination Request Struct </docs/api/zh_CN/latest/overview.html#pagination-request-struct>`__
   * - projection
     - False
     - Projection struct
     - Describe the object projection to be returned in the interface request. For details, see `How does projection crop the result set? </docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set>`__



## Response Parameters

| Name | Data Type | Description |
|-----------|------------------|------------------|
| data      | Asset Struct |  Asset list    |




## Sample 1

### Request Sample

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset&orgId=1c499110e8800000
{
 "filter": {
  "attributes": {
   "starsystem": "Solar System"
  }
 },
"projection": ["attributes", "assetId", "name"]
}
```

### Return Sample

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

