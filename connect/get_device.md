# Get Device

Get the information of a device.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Read

## Request Format

```json
GET https://{apigw-address}/connect-service/v2.1/devices?action=get
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
| deviceKey | Query           | Optional (See **Note** above)     | String       | The device key. To be used with ``productKey``.         |


## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data | Device Struct                          | The returned results of the device information. For details, see [Device Struct](/docs/api/en/2.1.0/connect/get_device.html#device-struct-device) |


### Device Struct <device>

| Name | Data Type | Description |
|------------------|-----------------------|----------------------------|
| orgId |  String | The organization ID which the asset belongs to. |
| assetId  | String  | The asset ID|
| modelId   | String     | The model ID which the asset belongs to. |
| modelIdPath      | String      | The model ID path.         |
| productKey       | String                            | The product key.  |
| productName      | StringI18n                        | The product name.  |
| productType      | String                            | The product type.   |
| dataFormat       | String                            | <ul><li>"Custom" represents the user-defined data type.</li><li>"Json" represents the JSON data type.</li></ul> |
| deviceKey        | String                            | The device key.    |
| deviceName       | StringI18n                        | The device name.   |
| deviceSecret     | String                            | The device secret identifier.       |
| deviceDesc       | String                            | The device description. |
| timezone         | String                            | Timezone of the device's location.     |
| deviceAttributes | Map | The device attributes. The Key is the attribute ID, and the Value type depends on the attribute defined in the ``ThingModel``.   |
| deviceTags       | Map  | The device tags. (The Key and Value are of String type.)       |
| createTime       | Long                              | The time when the device was created.                                                             |
| status           | String                            | The device status (online, offline, inactive, or disabled)                         |
| activeTime       | Long                              | The time when the device was activated.                                                             |
| lastOnlineTime   | Long                              | The last online time of the device.                                                       |
| lastOfflineTime   | Long                              | The last offline time of the device.                                                       |
| measurepointLastUpdate  | Long                              | The last time when a measurement point was updated.      |
| eventLastUpdate  | Long                              | The last time when an event was updated.                                                       |
| attributeLastUpdate  | Long                              | The last time when an attribute was updated.                                                       |
| featureLastUpdate  | Long                              | The last time when a measurement point, an event, or an attribute was updated. |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/devices?action=get&orgId=yourOrgId&assetId=yourAssetId
method: GET
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "835a5cc4-4487-4bf2-961a-55bc0ee77d02",
	"data": {
		"orgId": "yourOrgId",
		"assetId": "9HhK0YxX",
		"modelId": "abc-test",
		"modelIdPath": "/abc-test",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "abc-pk",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "testforname",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": "test for undatedevice",
		"timezone": "+08:00",
		"deviceAttributes": {
			"int11": 617
		},
		"deviceTags": {
			"test": "test for tags"
		},
		"createTime": 1557905107199,
		"status": "offline",
		"activeTime": 1557909526473,
		"lastOnlineTime": 1560743931658,
		"lastOfflineTime": 1560744111658,
		"measurepointLastUpdate":1565875705704,
		"eventLastUpdate":1565875705856,
		"attributeLastUpdate":1547793776699,
		"featureLastUpdate":1565875705856
	}
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.device.GetDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.GetDeviceResponse;

public class GetDevice {

    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String assetId = "yourAssetId";
        GetDeviceRequest request = new GetDeviceRequest();
        request.setOrgId(orgId);
        request.setAssetId(assetId);
        GetDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, GetDeviceResponse.class);
    }
}
```
