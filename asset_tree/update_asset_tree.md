# Update Asset Tree

Update the asset tree information.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |

## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| treeUpdateInfo   | true     |   TreeUpdateVo struct         |  Updated details to be provided when updating an asset tree. See [TreeUpdateVo struct](update_asset_tree#treeupdatevo-struct-treeupdatevostruc).  |


### TreeUpdateVo Struct <treeupdatevostruc>

| Name | Required or Not | Data Type | Description |
|-----------|-----------------|-------------------|-----------------------|
| treeId   | true         | String       | Asset tree ID. |
| name     | true         | StringI18n   | Asset name that supports internationalization. For the structure, see [Internationalized name struct>>](/docs/api/en/latest/api_faqs.html#internationalized-name-struct) |
|tags |false|Tag struct|User-customized tags. For details, see [How to use tag>>](/docs/api/en/latest/api_faqs.html#how-to-use-tag) |



## Sample 1

### Request Sample

```
https://apigw-address/asset-tree-service/v2.1 
/asset-trees?action=update&orgId=yourOrgId
{
"treeUpdateInfo":{
    "treeId": "H4yVDl2U",
    "name": {
        "defaultValue": "aaaa"
    },
    "tags":{
        "ss":"f"
    }
}
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
  "data": null
}
```

