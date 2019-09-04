# Get Command



Get a single command information.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=get
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
| commandId | Query         | True     | String          | Command ID          |

## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    Command struct        | Information corresponding to the command. See [Command Struct](/docs/api/en/latest/connect/get_command.html#command-struct-command) |

### Command Struct <Command>

| Name | Data Type     | Description          |
|-----------------|---------------------------|----------------|
| commandId  | String| Command ID|
| orgId          | String    | Organization ID which the asset belongs to  |
| productKey | String          | Product Key     |
| deviceKey | String         | Device Key         |
| assetId  | String         |Asset ID|
| createTime      | Long                            | Creation time                                             |
| createLocaltime | String| Local creation time|
| commandType     | Integer| Command type. 1.  Measurement point setting  2. Service invocation|
| commandName     | StringI18n| Command name. Refers to the measurement point name in case of measurement point setting. Refers to the service name in case of service invocation. |
| timeout         | Integer| Command timeout duration. Its unit is second and its range is [1-60], which is 30 by default|
| pendingTtl      | Long| Command cache duration. Its unit is second and its range is [ 0 - 48 * 60 * 60 ], which is 0 by default, indicating instant commands|
| state           | Integer| Command status, which is represented by an integer from 1-7.  1 -  Created; 2 - Canceled; 3 - Expired; 4 - Released; 5 - Send successfully; 6 - Failed; 7 - Response timed out. |
| tslIdentifier   | String| Corresponding identifier in the thing model. Refers to the measurement point identifier in case of measurement point setting. Refers to the service identifier in case of service invocation. |
| inputData       | Map (Key is of String type and the Value is of String, Number, Array or Object type) | Input data. In case of measurement point setting commands, the key is the measurement point identifier and the value is the measurement point value to be set. In case of service invocation commands, it is the service input parameter. The value data type should conform to the definition of thing model |
| outputData      | Map (Key is of String type and the Value is of String, Number, Array or Object type) | Output data. No return is provided for this field in case of measurement point setting commands. This field indicates the service output results in case of service invocation commands. The value data type should conform to the definition of thing model. |




## Sample 1

### Request Sample

```
https://{apigw-address}/connect-service/v2.1/commands?action=get&deviceKey=yourDeviceKey&productKey=yourProductKey&commandId= 2242591201245044736&orgId=yourOrgId
```

### Return Sample

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": {
        "commandId": "2242591201245044736",
        "orgId": "yourOrgId",
        "productKey": "yourProductKey",
        "deviceKey": "yourDeviceKey",
        "assetId": "KmItYUh4",
        "createTime": 1556172678510,
        "createLocalTime": 1556172678510,
        "commandType": 2,
        "commandName": {
            "defaultValue": "",
            "i18nValue": {
                "en_US": "test_fu_wu"
            }
        },
        "timeout": 30,
        "pendingTtl": 1000,
        "state": 2,
       
        "tslIdentifier": "test_fu_wu",
        "inputData": {
            "can_shu2": 1.3,
            "can_shu": 13
        },
        "outputData": {}
    }
}
```

