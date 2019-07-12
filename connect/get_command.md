# Get Command



Get a single command information.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=get
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
| data |    getCommand structure        | Information corresponding to the command. See [getCommand Structure](/docs/api/en/latest/connect/get_command.html#id3) |

### getCommand Structure

| Name | Data Type     | Description          |
|-----------------|---------------------------|----------------|
| commandId  | String| Command ID|
| orgId          | String    | Organization ID which the asset belongs to  |
| productKey | String          | Product Key      |
| deviceKey | String         | Device key          |
| assetId  | String         |Asset ID|
| createTime      | Long                            | Creation time                                             |
| createLocaltime | String| Local creation time|
| commandType     | Integer| Command type. 1.  Measurepoint setting  2. Service invocation|
| commandName     | StringI18n| Command name. Refers to the measurepoint name in case of measurepoint setting. Refers to the service name in case of service invocation. |
| timeout         | Integer| Command timeout duration. Its unit is second and its range is [1-60], which is 30 by default|
| pendingTtl      | Long| Command cache duration. Its unit is second and its range is [ 0 - 48 * 60 * 60 ], which is 0 by default, indicating instant commands|
| state           | Integer| Command status, which is represented by an integer from 1-7.  1 -  Created; 2 - Canceled; 3 - Expired; 4 - Released; 5 - Send successfully; 6 - Failed; 7 - Response timed out. |
| tslIdentifier   | String| Corresponding identifier in the thing model. Refers to the measurepoint identifier in case of measurepoint setting. Refers to the service identifier in case of service invocation. |
| inputData       | Map (Key is of String type and the Value is of String, Number, Array or Object type) | Input data. In case of measurepoint setting commands, the key is the measurepoint identifier and the value is the measurepoint value to be set. In case of service invocation commands, it is the service input parameter. The value data type should conform to the definition of thing model |
| outputData      | Map (Key is of String type and the Value is of String, Number, Array or Object type) | Output data. No return is provided for this field in case of measurepoint setting commands. This field indicates the service output results in case of service invocation commands. The value data type should conform to the definition of thing model. |




## Sample 1

### Request Sample

```
https://{apigw-address}/connect-service/v2.1/commands?action=get&deviceKey=WRJ2c1yMa5&productKey=doxkidR0&commandId= 2242591201245044736&orgId=o15541858646501
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
