# Search Asset Node



Query the assets that meet the conditions under the organization.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| filter| false         |   Filter structure        | Asset query criterion. See [Filter Structure](/docs/api/en/latest/asset_tree/search_asset_node.html#filter-filterstruc) |
| pagination| false         | Pagination request structure  | Used to describe the pagination requirements in the interface request. See [Pagination Request Structure](/docs/api/en/latest/overview.html#pagination-request-structure)  |
| projection| false         | String Array          | Used to describe the object projection to be returned in the interface request. See [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|


### Filter Structure <filterstruc>

| Name | Required or Not | Data Type | Description |
|-----------|---------------|----|--------------|
| assetIds| False  | String Array  | Asset ID. Provide the list of multiple asset IDs if you want to query multiple assets. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| modelIds | False | String Array | Model ID which the asset belongs to. Provide the list of multiple model IDs if you want to query multiple models. [How to get modelId](/docs/api/en/latest/api_faqs.html#how-to-get-model-id-modelid-modelid)|
| rootModelIds | False | String Array | Root model ID which the asset belongs to. Provide multiple root model IDs list if you want to query multiple root models. |
| nameLike | False | nameLike structure | Used to describe the query criterion for internationalized names. See [nameLike Structure](/docs/api/en/latest/asset_tree/search_asset_node.html#namelike-namelikestruc) |
| attributes  | False|Map |A group of attribute values. The key is the attribute name, String type. The value is the attribute value, and the type is defined by the specific model. For details, see [attributes representation](/docs/api/en/latest/api_faqs.html#attributes-representation) |
| tags | False | Tag structure | A group of user-customized tags |
| treeId | False | String | ID of the asset tree associated to the asset |


### nameLike Structure <namelikestruc>

| Name | Data Type | Description |
|-----------|---------------------|-----------------------|
| value        | String     | Name or name fragment to be queried|
| locale         | String     | Specified locale, such as "zh_CN"|


## Response Parameters

| Name | Data Type | Description |
|-----------|------------------|------------------|
| data      | Asset Structure Array |  Asset list    |




## Sample 1

### Request Sample

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset&orgId=1c499110e8800000
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

