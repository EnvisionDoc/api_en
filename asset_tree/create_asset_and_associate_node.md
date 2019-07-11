# Create Asset and Associate Node

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Create a logical asset and associate it with the asset tree.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=createAsset
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree to be gotten. [How to get asset tree ID](/docs/api/en/latest/api_faqs#id)        |
| parentAssetId | Query            | true    | String    | Asset ID of the parent node of the asset to be associated.  |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|------------|---------------|----------------|--------------------------------|
| asset| true          | Asset structure    | Asset details to be provided when creating an asset. See [Asset Structure](/docs/api/en/latest/asset_tree/create_asset_and_associate_node.html#asset-assetstruc)   |


### Asset structure <assetstruc>

| Name | Required or Not | Data Type | Description |
|-------|-------|-------------|--------------|
| modelId           | true      | String      | Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs.html#how-to-get-modeid-information-modeid)|
| name |true| StringI18n |Internationalized asset names are supported. For the structure, see [Internationalized Name Structure](/docs/api/en/latest/api_faqs.html#id3)
|timezone  |true|  String  |Timezone where the asset is located. <br> If +08:00 format is used, it indicates that the timezone for summer time is not supported. <br> If Asia/Shanghai format is used, it indicates that the timezone for summer time is supported. <br>For details, see [Timezone Representation](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#id4) |
|description |false|String|Asset description |
|attributes  |false  |Map  (Key is of String type, and the Value is of object type)  |Attributes of the model which the asset belongs to. For details, see [Attributes Representation](/docs/api/en/latest/api_faqs.html#attributes) |
|tags |false|Tag structure|User-customized tags. For details, see [Role and Representation of Tags](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#id6)|



## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| String                            | Created asset ID                   |


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
https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?treeId=lMAXwaLX&action=createAsset&parentAssetId=fy4hxezF&orgId=1c499110e8800000
{ 
    "asset": { 
        "modelId": "STRING-INVERTER-MODEL", 
        "name": { 
            "defaultValue": "inverter #1", 
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

### Return sample

```json
{ 
    "code": 0, 
    "msg": "ok", 
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f", 
    "data": "cRUdS7sJ" 
} 
```

