# Cancel Command



Cancel the cached commands. If there is a `commandId`, cancel the single command, and if there is no `commandId`, cancel all the cached commands for the device.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=cancel
```

## Request Parameters (URI)

.. note:: In the following non-required fields, you must provide ``assetId`` or a combination of ``productKey`` and ``deviceKey`` to specify the device.

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId>>](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key     |
| deviceKey | Query           | False      | String       | Device Key         |
| commandId | Query         | False     | String          | Command ID          |


## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    getCommand Struct        | List of cancelled commands. See [getCommand Struct](/docs/api/en/latest/connect/get_command.html#getcommand-struct-getcommand) |




## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/commands?action=cancel&deviceKey=mqtt_01&productKey=bXuuAiku&orgId=o15541858646501
method: POST
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

