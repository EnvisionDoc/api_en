# Delete Asset Tree

Delete an asset tree.

## Request Format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=delete

```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | true    | String    | ID of the asset tree to be deleted. [How to get asset tree ID>>](/docs/api/en/latest/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |



## Error Codes

| Code | Description    |
|-----------|-----------------------------|
| 99800| There is child node under the root node of the asset tree. So, the asset tree can not be deleted.  |




## Sample 1

### Request Sample

```
https://apigw-address/asset-tree-service/v2.1 
/asset-trees?action=delete&orgId=yourOrgId&treeId=H4yVDl2U
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

