# Get Gateway

Get the gateway information based on the specified sub-device.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Read

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/device-topos?action=getGateway
```

## Request Parameters (URI)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_





## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - subDevice
     - Mandatory
     - DeviceIdentifier Struct
     - The information of the sub-device. For more details, see `DeviceIdentifier Struct </docs/api/en/2.1.0/connect/get_gateway.html#deviceidentifier-struct-deviceidentifier>`_




### DeviceIdentifier Struct <deviceidentifier>

Note: Use either the (``assetId``) or (``productKey`` + ``deviceKey``) for the following.

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - assetId
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - String
     - The product key. To be used with ``deviceKey`` .
   * - deviceKey
     - String
     - The device key. To be used with ``productKey`` .



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Device Struct
     - The information of the gateway device. For more details, see `Device Struct </docs/api/en/2.1.0/connect/get_gateway.html#device-struct-devicetstruc>`_




### Device Struct <devicetstruc>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - orgId
     - String
     - The organization ID which the asset belongs to.
   * - assetId
     - String
     - The asset ID.
   * - modelId
     - String
     - The model ID which the asset belongs to.
   * - modelIdPath
     - String
     - The model ID path.
   * - productKey
     - String
     - The product key.
   * - productName
     - StringI18n
     - The product name.
   * - productType
     - String
     - The product type.
   * - dataFormat
     - String
     - + "Custom" represents the user-defined data type
	   + "Json" represents the json data type
   * - deviceKey
     - String
     - The device key.
   * - deviceName
     - StringI18n
     - The device name.
   * - deviceSecret
     - String
     - The device secret identifier.
   * - deviceDesc
     - String
     - The device description.
   * - timezone
     - String
     - Timezone of the device's location.
   * - deviceAttributes
     - Map
     - The device attributes. The Key is the attribute ID, and the Value type depends on the attribute defined in the ``ThingModel``.
   * - deviceTags
     - Map
     - The device tags. (The Key and Value are of String type.)
   * - createTime
     - Long
     - The time when the device was created.
   * - status
     - String
     - The device status (online, offline, inactive, or disabled)
   * - activeTime
     - Long
     - The time when the device was activated.
   * - lastOnlineTime
     - Long
     - The last online time of the device.
   * - lastOfflineTime
     - Long
     - The last offline time of the device.
   * - measurepointLastUpdate
     - Long
     - The last time when a measurement point was updated.
   * - eventLastUpdate
     - Long
     - The last time when an event was updated.
   * - attributeLastUpdate
     - Long
     - The last time when an attribute was updated.
   * - featureLastUpdate
     - Long
     - The last time when a measurement point, an event, or an attribute was updated.




## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/device-topos?action=getGateway&orgId=yourOrgId
method: POST
requestBody:
{
	"subDevice":{
		"assetId":"yourAssetId"
	}
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "49ef6c03-02a0-449b-ab1e-92812071de80",
	"data": {
		"orgId": "yourOrgId",
		"assetId": "J1Rqyaqz",
		"modelId": "AlterTest0617",
		"modelIdPath": "/AlterTest0617",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "testtopo",
			"i18nValue": {}
		},
		"productType": "Gateway",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "testtopo",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1560759829419,
		"status": "inactive",
		"activeTime": 0,
		"lastOnlineTime": 0,
		"lastOfflineTime": 0,
		"lastOfflineTime": 0,
    	"measurepointLastUpate": null,
    	"eventLastUpdate": null,
    	"attributeLastUpdate": 1561447707379,
    	"featureLastUpdate": 1561447707379
	}
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device.topo;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.device.topo.GetGatewayRequest;
import com.envisioniot.enos.connect_service.v2_1.device.topo.GetGatewayResponse;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;


public class GetGateWay {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourSeverUrl";

        String orgId = "yourOrgId";
        GetGatewayRequest request = new GetGatewayRequest();
        request.setOrgId(orgId);
        request.setSubDevice(new DeviceIdentifier("zGeKTDrw"));


        GetGatewayResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, GetGatewayResponse.class);
    }}
```