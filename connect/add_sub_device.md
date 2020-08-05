# Add Sub-Device

Add new sub-devices to the gateway device (creating a topological relationship).

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/device-topos?action=addSubDevice
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|--------------------|----------|-----------|--------------|
| gateway | Mandatory      |DeviceIdentifier Struct | The information of the gateway device to add the sub-device to. For more details, see [DeviceIdentifier Struct](/docs/api/en/2.1.0/connect/add_sub_device.html#deviceidentifier-struct-deviceidentifier). |
| subDevices           | Mandatory      | Array of DeviceIdentifier Structs | The list of the sub-devices to add to the specified gateway. For more details, see [DeviceIdentifier Struct](/docs/api/en/2.1.0/connect/add_sub_device.html#deviceidentifier-struct-deviceidentifier).  |


### DeviceIdentifier Struct <deviceidentifier>

Note: Use either the (``assetId``) or (``productKey`` + ``deviceKey``) for the following.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | String         | The product key. To be used with ``deviceKey``.      |
| deviceKey | String         | The device key. To be used with ``productKey``.      |



## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |  Not Gateway    | The device specified in ``gateway`` is not a gateway.|
| 11739 |   Exceed max device size  |This operation will cause the number of sub-devices of the gateway to exceed the limit. |
| 99400 |   Invalid arguments    | One or multiple parameters are invalid.      |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/device-topos?action=addSubDevice&orgId=yourOrgId
method: POST
requestBody: 
{
  "subDevices":[
    {
      "assetId":"mAEsF3sm"
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
  "requestId":"5246f91c-f9ce-485c-a9f2-4cd8b7e1f0df",
  "data":null
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device.topo;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.device.topo.AddSubDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.topo.AddSubDeviceResponse;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;

import java.util.ArrayList;
import java.util.List;

public class AddSubDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";
        String orgId = "yourOrgId";

        AddSubDeviceRequest request = new AddSubDeviceRequest();
        request.setOrgId(orgId);
        request.setGateway(new DeviceIdentifier("J1Rqyaqz"));
        List < DeviceIdentifier > deviceList = new ArrayList < > ();
        deviceList.add(new DeviceIdentifier("zGeKTDrw"));
        deviceList.add(new DeviceIdentifier("Fi0HQ8FO"));

        request.setSubDevices(deviceList);
        AddSubDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url(serverUrl)
            .getResponse(request, AddSubDeviceResponse.class);
    }
}
```