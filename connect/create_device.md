# Create Device

Create a device.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Prerequisite

- Ensure the product to create this device under exists.

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/devices?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|----------------|---------------|--------------------------|---|
|productKey    | Mandatory          | String       | The product key.     |
|timezone | Mandatory          | String         | Timezone of the device's location.     |
| deviceName | Mandatory          | StringI18n | The device name. For more details on the structure and locales supported, see [Internationalized name struct>>](/docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct)         |
| deviceAttributes | Optional         | Map       | The device attributes.    |
| deviceKey   | Optional         | String    | The device key.         |
| deviceDesc  | Optional         | String    | The device description.     |
| deviceTags  | Optional         | Map    | The device tags. (The Key and Value are of String type.) For details, see [How to use tag>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag)     |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    DeviceCreateResult struct        | The returned results of the device creation. For details, see [DeviceCreateResult Struct](/docs/api/en/2.1.0/connect/create_device.html#devicecreateresult-struct-devicecreateresult). |


### DeviceCreateResult Struct <devicecreateresult>

| Name | Data Type | Description |
|------------------|-----------------------|----------------------------|
| productKey       | String            | The product key.              |
| deviceKey       | String    | The device Key.                  |
| deviceSecret     | String     | The device connection key.                |
| assetId  | String         |The asset ID.|


## Error Codes

| Code| Data Type | Description |
|-----------|----------------|----------------------|
| 11702 |  DeviceKey existed   | The ``deviceKey`` already exists in the database (when ``deviceKey`` is provided).        |
| 11714 |  Generate deviceKey failed  | The key of the device cannot be assigned temporarily (when the ``deviceKey`` is not provided). Please try again. |
| 11739 |  Exceed max device size   | A product can have a max of 10,000 devices under it. This operation will exceed the limit. |




## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/devices?action=create&orgId=yourOrgId
method: POST
requestBody: 
{
	"deviceTags":{
		"test":"test for tags"
	},
	"timezone":"+08:00",
	"productKey":"yourProductKey",
	"deviceAttributes":{
		"testatt":111111
	},
	"deviceName":{
		"defaultValue":"testCreateDevice",
		"i18nValue":{

		}
	},
	"deviceDesc":"test for createdevice"
}
```

### Return Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"fd79d0f5-69c5-4fa8-add4-69f5ca1b635f",
    "data":{
        "assetId":"Uvmm5AXU",
        "productKey":"yourProductKey",
        "deviceKey":"yourDeviceKey",
        "deviceSecret":"Z5YtZaQpK5IWocakV7zQ"
    }
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.common.StringI18n;
import com.envisioniot.enos.connect_service.v2_1.device.CreateDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.CreateDeviceResponse;


import java.util.HashMap;
import java.util.Map;


public class CreateDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        final String serverUrl = "yourServerUrl";
        final String orgId = "yourOrgID";

        CreateDeviceRequest request = new CreateDeviceRequest();
        request.setOrgId(orgId);
        request.setDeviceDesc("yourDeviceDesc");
        request.setProductKey("yourProductKey");
        StringI18n stringI18n = new StringI18n();
        stringI18n.setDefaultValue("testDevice");
        request.setDeviceName(stringI18n);
        Map < String, Object > deviceAttributes = new HashMap < > ();
        //        deviceAttributes.put("testatt",111111);
        Map < String, String > deviceTags = new HashMap < > ();
        deviceTags.put("test", "test for tags");
        request.setDeviceAttributes(deviceAttributes);
        request.setDeviceTags(deviceTags);
        request.setTimezone("+08:00");

        CreateDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url(serverUrl)
            .getResponse(request, CreateDeviceResponse.class);

    }
}
```
