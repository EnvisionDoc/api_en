# Get Command

Get the details of a command.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Control

## Request Format

```json
GET https://{apigw-address}/connect-service/v2.1/commands?action=get
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request



| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | Optional (See **Note** above)  | String         | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | Optional (See **Note** above)      | String       | The product key. To be used with ``deviceKey``.     |
| deviceKey | Query           | Optional (See **Note** above)      | String       | The device key. To be used with ``productKey``.         |
| commandId | Query         | Mandatory     | String          | The command ID          |

## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    Command Struct        | The details of the command. See [Command Struct](/docs/api/en/2.1.0/connect/get_command.html#command-struct-command). |

### Command Struct <Command>

| Name | Data Type     | Description          |
|-----------------|---------------------------|----------------|
| commandId  | String| The command ID|
| orgId          | String    | The organization ID which the asset belongs to.  |
| productKey | String          | The product key.     |
| deviceKey | String         | The device key.         |
| assetId  | String         |The asset ID.|
| createTime      | String                            | The time when the command was invoked.                |
| createLocaltime | String| The local time when the command was invoked. |
| commandType     | Integer| The command type. <ul><li>1 = Measurement point setting</li><li>2 = Service invocation</li></ul>  |
| commandName     | StringI18n| The command name. Refers to the measurement point name for measurement point setting. Refers to the service name for service invocation. |
| timeout         | Integer| The command timeout duration. Its unit is seconds and its range is [1-60]. The default value is 30.|
| pendingTtl      | Long| The command cache duration. Its unit is seconds and its range is [ 0 - 48 * 60 * 60 ], which is 0 by default. If the pendingTtl is 0, it indicates that the commands will be executed immediately.|
| state           | Integer| The command status, which is represented by an integer from 1-7.  <ul><li>1 = Created</li><li>2 = Canceled</li><li>3 = Expired</li><li>4 = Released</li><li>5 = Send successfully</li><li>6 = Failed</li><li>7 - Response timed out</li></ul> |
| tslIdentifier   | String| The corresponding identifier in the `ThingModel`. Refers to the measurement point identifier for measurement point setting. Refers to the service identifier for service invocation. |
| inputData       | Map (Key is of String type and the Value is of String, Number, Array or Object type) | The input data. For measurement point setting commands, the key is the measurement point identifier and the value is the measurement point value to be set. For service invocation commands, the key is the service input parameter identifier. The value data type will be as per defined in the `ThingModel`. |
| outputData      | Map (Key is of String type and the Value is of String, Number, Array or Object type) | The output data. No return value is provided for this field for measurement point setting commands. For service invocation commands, this will return the service output results. The value data type will be as per defined in the `ThingModel`. |




## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/commands?action=get&deviceKey=yourDeviceKey&productKey=yourProductKey&commandId= yourCommandId&orgId=yourOrgId
method: GET
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": {
        "commandId": "2242591201245044736",
        "orgId": "yourOrgId",
        "productKey": "yourProductKey",
        "deviceKey": "yourDeviceKey",
        "assetId": "yourAssetId",
        "createTime": "15910899018",
        "createLocalTime": "2020-06-02 17:25:01",
        "commandType": 2,
        "commandName": {
            "defaultValue": "",
            "i18nValue": {
                "en_US": "test_service"
            }
        },
        "timeout": 30,
        "pendingTtl": 1000,
        "state": 2,

        "tslIdentifier": "test_service",
        "inputData": {
            "parameter_1": 1.3,
            "parameter_2": 13
        },
        "outputData": null
    }
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.command;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.service.GetCommandRequest;
import com.envisioniot.enos.connect_service.v2_1.service.GetCommandResponse;

public class GetCommand {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String productKey = "yourProductKey";
        String deviceKey = "yourDeviceKey";
        String commandId = "yourCommandId";

        GetCommandRequest request = new GetCommandRequest();
        request.setOrgId(orgId);
        request.setProductKey(productKey);
        request.setDeviceKey(deviceKey);
        request.setCommandId(commandId);
        GetCommandResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, GetCommandResponse.class);
    }
}
```
