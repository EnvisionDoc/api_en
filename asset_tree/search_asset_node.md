# Search Asset Node



Query the assets that meet the conditions under the OU.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| filter| false         |   Filter structure        | Asset query criterion. See [Filter Structure](/docs/api/en/latest/asset_tree/search_asset_node.html#filter-filterstruc) |
| pagination| false         | Pagination request structure  | Used to describe the pagination requirements in the interface request. See [Pagination Request Structure](/docs/api/en/latest/overview.html?highlight=pagination#pagination)  |
| projection| false         | String Array          | Used to describe the object projection to be returned in the interface request. See [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|


### Filter structure <filterstruc>

| Name | Required or Not | Data Type | Description |
|-----------|---------------|----|--------------|
| assetIds| False  | String Array  | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)|
| modelIds | False | String Array | Model ID which the asset belongs to. You should provide the list of multiple model IDs if you want to query multiple models. [How to get modelId information](/docs/api/en/latest/api_faqs.html#how-to-get-modeid-information-modeid)|
| rootModelIds | False | String Array | Model ID which the asset belongs to. You should provide multiple root model IDs if you want to query multiple root models. |
| nameLike | False | nameLike structure | Used to describe the query criterion for internationalized names. See [nameLike Structure](/docs/api/en/latest/asset_tree/search_asset_node.html#namelike-namelikestruc) |
| attributes  | False|Map |Attributes of the model which the asset belongs to. For details, see [attributes representation](/docs/api/en/latest/api_faqs.html#attributes-representation) |
| tags | False | Tag structure | A group of user-customized tags |
| treeId | False | String | ID of the asset tree associated to the asset |


### nameLike structure <namelikestruc>

| Name | Data Type | Description |
|-----------|---------------------|-----------------------|
| value        | String     | Name or name fragment to be queried|
| locale         | String     | Specified locale, such as zh_CN|


## Response parameters

| Name | Data Type | Description |
|-----------|------------------|------------------|
| data      | Asset Structure Array |  Asset list    |




## Sample 1

### Request sample

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

### Return sample

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

