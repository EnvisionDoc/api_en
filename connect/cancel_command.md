# Cancel Command



Cancel the interface to cached commands. If there is a `commandId`, the single command will be canceled, and if there is no `commandId`, all the cached commands for the device will be canceled.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=cancel
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device key          |
| deviceKey | Query         | False     | String          | Command key          |


## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    getCommand Structure        | List of cancelled commands. See [getCommand Structure](/docs/api/en/latest/connect/get_command.html#id3) |




## Sample 1

### Request Sample

```
https://{apigw-address}/connect-service/v2.1/commands?action=cancel&deviceKey=mqtt_01&productKey=bXuuAiku&orgId=o15541858646501
```

### Return Sample

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": [{
        "commandId": "2278935391225618432",
        "orgId": "yourOrgId",
        "productKey": "yourProductKey",
        "deviceKey": "yourDeviceKey",
        "assetId": "oxWwM9i5",
        "createTime": 1560505243577,
        "createLocalTime": 1560505243577,
        "commandType": 1,
        "commandName": {
            "defaultValue": "Int_value",
            "i18nValue": {
                "en_US": "Int_value"
            }
        },
        "timeout": 1,
        "pendingTtl": 6000,
        "state": 1,
        "tslIdentifier": "Int_value",
        "inputData": 222
    }]
}
```

