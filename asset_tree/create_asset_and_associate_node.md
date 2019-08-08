# Create Asset and Associate Node



Create a logical asset and associate it with the asset tree.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=createAsset
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree [How to get the ID of an asset tree](/docs/api/en/latest/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |
| parentAssetId | Query            | true    | String    | Asset ID of the parent node of the asset to be associated  |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|------------|---------------|----------------|--------------------------------|
| asset| true          | Asset struct    | Asset details to be provided when creating an asset. See [Asset Struct](/docs/api/en/latest/asset_tree/create_asset_and_associate_node.html#asset-struct-assetstruc)   |


### Asset Struct <assetstruc>

| Name | Required or Not | Data Type | Description |
|-------|-------|-------------|--------------|
| modelId           | true      | String      | Model ID which the asset belongs to. [How to get modelId](/docs/api/en/latest/api_faqs.html#how-to-get-model-id-modelid-modelid)|
| name |true| StringI18n |Asset name that supports internationalization. For the structure, see [Internationalized name struct](/docs/api/en/latest/api_faqs.html#internationalized-name-struct)
|timezone  |true|  String  |Timezone where the asset is located.<br>Use the "+08:00" format to indicate time zones that do not support daylight saving time.<br>Use the Asia/Shanghai" format to indicate time zones that support daylight saving time<br>For details, see [Timezone representation](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#timezone-representation) |
|description |false|String|Asset description |
|attributes  |false  |Map  (Key is of String type, and the Value is of object type)  |Attributes of the model which the asset belongs to. For details, see [attributes representation](/docs/api/en/latest/api_faqs.html#attributes-representation) |
|tags |false|Tag struct|User-customized tags. For details, see [How to use tag](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#how-to-use-tag)|



## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| String                            | Created asset ID                   |


## Error Codes

| Code | Description    |
|-----------|-----------------------------|
| 17751 | Tree ID does not exist              |
| 17752| The parent asset does not exist in this tree          |
| 17758 | The asset already exists on the tree            |
| 17760 | The name of the asset to be created is illegal      |
| 17770| The tree exceeds the maximum number of layers (7 layers) |



## Sample 1

### Request Sample

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?treeId=lMAXwaLX&action=createAsset&parentAssetId=fy4hxezF&orgId=1c499110e8800000
{ 
    "asset": { 
        "modelId": "STRING-INVERTER-MODEL", 
        "name": { 
            "defaultValue": "逆变器 #1", 
            "i18nValue": { 
                "en_US": "Inverter #1" 
            } 
        }, 
        "timezone": "+08:00", 
        "description": "This is a sampled asset.", 
        "attributes": { 
            "foo": 100, 
            "bar": "example" 
        }, 
        "tags": { 
            "foo": "bar", 
            "hello": "world" 
        } 
    } 
}
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

