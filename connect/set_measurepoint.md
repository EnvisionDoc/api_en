# Set Measurement Point

Measurement point setting interface for the device.

This interface can execute cached commands or instant commands. When executing instant commands, the interface response data is returned after the device returns the measurement point setting results. If the device does not return the results within the specified measurement point setting timeout period, the EnOS service will wait for the timeout and then return the interface response data.

When executing cached commands, the data will be returned directly after being cached.

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
POST https://{apigw-address}/connect-service/v2.1/commands?action=setMeasurepoint
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request




| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | Optional (See **Note** above)   | String         | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | Optional (See **Note** above)     | String       | The product key. To be used with ``deviceKey``.    |
| deviceKey | Query           | Optional (See **Note** above)      | String       | The device key. To be used with ``productKey``.        |
| measurepointId      | Query| Mandatory| String    | The measurement point ID. [How to get pointId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-the-measurement-point-id-pointid-pointid) |
| pendingTtl     | Query| Optional| Integer    | The cache storage time. Its unit is seconds and its range is [0 - 172800 (i.e. 48 hours)], which is 0 by default. If the pendingTtl is 0, it indicates that the commands will be executed immediately.  |
| timeout        | Query| Optional         | Integer    | The timeout period of service execution in seconds. Its range is [1-60], with a default value of 30 seconds.|

## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|-----------|---------------|-------------------|----------|
| value | Mandatory| String, Number, Array or Object | The parameter value for measurement point setting, the value data type of which will be as per defined in the thing model.  |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Command ID Struct      | The measurement point setting results. For details, see [Command ID Struct](/docs/api/en/2.1.0/connect/set_measurepoint.html#measurement-point-setting-return-struct-mp). |


### Command ID Struct <mp>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| commandId  | String| The command ID.|

## Error Codes

| Code | Description    |
|-------|------------------------------------------------------------------|
| 11904 | The command is not sent, and the instant command timed out.          |
| 11915 | The command is sent, but the response timed out.                 |
| 11902 | The number of cached commands reached the upper limit.                                   |
| 11900 | The device is offline and the instant command cannot be sent.                                     |
| 11810 | The command can not be encoded into the product-customized format when the product supports custom data formats. |
| 11888 | The device is not activated and the instant command cannot be sent.                        |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/commands?action=setMeasurepoint&deviceKey=yourDeviceKey&measurepointId=measurepoint1&&pendingTtl=1000&productKey=yourProductKey&orgId=yourOrgId&timeout=30
method: POST
requestBody: 
{
   "value":1.0
}
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": {
        "commandId": "2078724684846989312"
     }
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.command;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.connect_service.v2_1.service.SearchCommandRequest;
import com.envisioniot.enos.connect_service.v2_1.service.SearchCommandResponse;
import com.envisioniot.enos.connect_service.v2_1.service.SetMeasruepointRequest;
import com.envisioniot.enos.connect_service.v2_1.service.SetMeasruepointResponse;
import com.google.gson.GsonBuilder;

public class SetMeasurepoint {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String productKey = "yourProductKey";
        String deviceKey = "yourDeviceKey";

        SetMeasruepointRequest request = new SetMeasruepointRequest();
        request.setOrgId(orgId);
        request.setProductKey(productKey);
        request.setDeviceKey(deviceKey);
        request.setMeasurepointId("Int_value");
        request.setValue(111);
//        request.setPendingTtl(600L);
        request.setTimeout(10);
        SetMeasruepointResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, SetMeasruepointResponse.class);
        
        System.out.println(new GsonBuilder().setPrettyPrinting().create().toJson(response));
    }
}
```