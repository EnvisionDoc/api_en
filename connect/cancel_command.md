# Cancel Command

Cancel cached commands. If a ``commandId`` is specified, the command with the ``commandId`` will be cancelled. If no ``commandId`` is specified, all the device's cached commands will be cancelled.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Control

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/commands?action=cancel
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
| deviceKey | Query           | Optional (See **Note** above)    | String       | The device key. To be used with ``productKey``.    |
| commandId | Query         | Optional     | String          | The command ID.          |


## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    Array of Command Structs        | The list of cancelled commands. For details, see [Command Struct>>](/docs/api/en/2.1.0/connect/get_command.html#command-struct-command) |




## Samples

### Request Sample

```
url: https://{apigw-address}/connect-service/v2.1/commands?action=cancel&deviceKey=yourDeviceKey&productKey=yourProductKey&orgId=yourOrgId&commandId=2278935391225618432
method: POST
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": [{
        "commandId": "2278935391225618432",
        "orgId": "yourOrgId",
        "productKey": "yourProductKey",
        "deviceKey": "yourDeviceKey",
        "assetId": "yourAssetId",
        "createTime": "1560505243577",
        "createLocalTime": "2019-06-14 17:40:23",
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
        "inputData": 222,
        "outputData": null
    }]
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.command;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.service.CancelCommandRequest;
import com.envisioniot.enos.connect_service.v2_1.service.CancelCommandResponse;

public class CancelCommand {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String productKey = "yourProductKey";
        String deviceKey = "yourDeviceKey";
        String commandId = "yourCommandId";

        CancelCommandRequest request = new CancelCommandRequest();
        request.setOrgId(orgId);
        request.setProductKey(productKey);
        request.setDeviceKey(deviceKey);
        request.setCommandId(commandId);
        CancelCommandResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, CancelCommandResponse.class);
    }
}
```
