# Remove Sub-Device

Remove sub-devices from the gateway (remove the topological relationship).

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Request Format

```JSON
POST https://{apigw-address}/connect-service/v2.1/device-topos?action=removeSubDevice
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|--------------------|----------|-----------|--------------|
| gateway | Mandatory      |DeviceIdentfier Struct | Information of the gateway to remove the sub-device from. For details, see [DeviceIdentfier Struct](/docs/api/en/2.1.0/connect/remove_sub_device.html#deviceidentifier-struct-di). |
| subDevices           | Mandatory      | Array of DeviceIdentfier Structs | The list of the sub-devices to be removed from the specified getaway. For details, see [DeviceIdentfier Struct](/docs/api/en/2.1.0/connect/remove_sub_device.html#deviceidentifier-struct-di). |


### DeviceIdentifier Struct  <di>

Note: Use either the (``assetId``) or (``productKey`` + ``deviceKey``) for the following.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| productKey | String        | The product key. To be used with `deviceKey` .   |
| deviceKey | String         | The device key. To be used with `productKey` .   |



## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |  Not Gateway     | The device specified in ``gateway`` is not a gateway. |
| 11795 |   Invalid arguments   | One or multiple parameters are invalid.      |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/device-topos?action=remove&orgId=yourOrgId
method: POST
requestBody:  
{
  "subDevices":[
    {
      "assetId":"gVRwKQ3C"
    }
  ],
  "gateway":{
    "assetId":"J1Rqyaqz"
  }
}
```

### Return Sample

```json
{
  "code":0,
  "msg":"OK",
  "requestId":"ea6608bb-b8cb-46f3-a836-ee24ea9a028c",
  "data":null
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device.topo;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.device.topo.RemoveSubDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.topo.RemoveSubDeviceResponse;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;

import java.util.ArrayList;
import java.util.List;


public class RemoveSubDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        RemoveSubDeviceRequest request = new RemoveSubDeviceRequest();
        request.setOrgId(orgId);
        request.setGateway(new DeviceIdentifier("J1Rqyaqz"));

        List<DeviceIdentifier> deviceList = new ArrayList<>();
        deviceList.add(new DeviceIdentifier("zGeKTDrw"));
        deviceList.add(new DeviceIdentifier("Fi0HQ8FO"));
        request.setSubDevices(deviceList);

        RemoveSubDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, RemoveSubDeviceResponse.class);
    }
}
```
