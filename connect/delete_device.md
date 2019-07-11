# Delete Device



Delete devices.

## Request format

```
https://{apigw-address}/connect-service/v2.1/devices?action=delete
```

## Request parameters (URI)

Note: In the following non-mandatory fields, you must provide a combination of `assetId` or `productKey` and `deviceKey` to specify the device.

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| assetId  | Query            | False   | String         | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device key          |




## Sample 1

### Request sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=delete&orgId=o15475450989191&assetId=mAEsF3sm
method:  POST
headers:  {}
requestBody:  null
```

### Return sample

```json
responseBody:{
"code":0,
"msg":"OK",
"requestId":"12d7e3be-6bac-43de-8733-7e02a4eb8a88",
"data":null
}
```

