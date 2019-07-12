# Enable Device



Enable devices.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/devices?action=enable
```

## Request Parameters (URI)

Note: In the following non-mandatory fields, you must provide a combination of `assetId` or `productKey` and `deviceKey` to specify the device.

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query          | False      | String        | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key      |
| deviceKey | Query         | False     | String          | Device key          |
    


## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11794 |                | The device to be enabled has been activated             |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=enable&orgId=o15475450989191&assetId=9HhK0YxX
method:  POST
```

### Return Sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "06dd8ea3-cb9e-4628-8f93-d36c416bcd3a",
	"data": null
}
```

