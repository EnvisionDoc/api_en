# Get Asset Tree



Get an asset tree under the specified OU.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=get
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree to be gotten. [How to get the ID of an asset tree>>](/docs/api/en/latest/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |


## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| treeId| String                            | Asset tree ID                    |
| tags| Map (Key is of String type, and the value is of String type) | A group of user-customized asset tree tags  |
| asset| asset struct | Root asset of asset tree. See [asset Struct](/docs/api/en/latest/asset_tree/get_asset_tree.html#asset-struct-assetstruc)              |

### Asset Struct <assetstruc>

| Name | Data Type | Description |
|-------|-------|---------------------------|
| assetId |  String | Asset ID|
|modelId|String|Model ID which the asset belongs to|
|modelIdPath|String|Model ID path |
| name | StringI18n |Asset name that supports internationalization|
|timezone  |  String  |Timezone where the asset is located.<br>Use the "+08:00" format to indicate time zones that do not support daylight saving time.<br>Use the Asia/Shanghai" format to indicate time zones that support daylight saving time|
| description | String | Asset description|
| label  | String | Asset type: "0" - device assets; "1" - logical assets|
| inValid  | Boolean | true stands for invalid nodes while false stands for valid nodes|
|attributes   |Map  (Key is of String type, and the Value is of object type)  |Attributes of the model which the asset belongs to|
|tags|Map<br>(Key is of String type, and the value is of String type)|User-customized tags|



## Sample 1

### Request Sample

```
GET
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?treeId=BRIt3ee3&action=get&orgId=o15541858646501
```

### Return Sample

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "f3c1ffc7-cc8e-4a50-ad40-0fa7b0c3a7ac",
 "data": {
  "treeId": "BRIt3ee3",
  "tags": {
   "user": "zm",
   "user0": "lily"
  },
  "asset": {
   "inValid": false,
   "assetId": "nlw68lR5",
   "modelId": "model_0422",
   "modelIdPath": "/model_0422",
   "name": {
    "defaultValue": "0430343",
    "i18nValue": {
     "en_US": "0430343"
    }
   },
   "timezone": "+08:00",
   "description": null,
   "label": "1",
   "attributes": {},
   "tags": {
    "tree": "0430"
   }
  }
 }
}
```

