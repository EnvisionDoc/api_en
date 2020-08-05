# Update Device

Update a device. The `IsPatchUpdate` is taken as true in the update mode. The `assetId` (or `productKey` + `deviceKey`) parameter is to be specified in the request url, and other parameters are to be specified in the request body.

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
POST https://{apigw-address}/connect-service/v2.1/devices?action=update
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device to be updated:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request



| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query          | Optional (See **Note** above)     | String        | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query         | Optional (See **Note** above)      | String         | The product key. To be used with ``deviceKey``.     |
| deviceKey | Query         | Optional (See **Note** above)    | String          | The device key. To be used with ``productKey``.          |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|----------------|---------------|--------------------------|---|
|timezone | Mandatory          | String         |Timezone of the device's location.     |
| deviceName | Mandatory          | StringI18n | The device name. For more details on the structure and locales supported, see [Internationalized name struct>>](/docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct)         |
| deviceAttributes | Optional         | Map       | The device attributes.         |
| deviceTags   | Optional         | Map    | The device tags. (The Key and Value are of String type.) For details, see [How to use tag>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag) |
| deviceDesc  | Optional         | String    |The device description.     |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/devices?action=update&orgId=yourOrgId&assetId=yourAssetId
method: POST
requestBody:  
{
	"deviceTags": {
		"test": "test_value"
	},
	"deviceAttributes": {
		"int11": 617
	},
	"deviceName": {
		"defaultValue": "Device Name",
		"i18nValue":{
            "en_US":"Device Name",
            "zh_CN":"设备"
        }
	},
	"deviceDesc": "Description Update Device"
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "0d61752e-0633-4846-abb1-b6fb39801a5f",
	"data": null
}
```


### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.common.StringI18n;
import com.envisioniot.enos.connect_service.v2_1.device.UpdateDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.UpdateDeviceResponse;

import java.util.HashMap;
import java.util.Map;

public class UpdateDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String assetId = "yourAssetId";
        UpdateDeviceRequest request=new UpdateDeviceRequest();
        request.setOrgId(orgId);
        request.setAssetId(assetId);
        request.setDeviceDesc("yourDeviceDesc");
        request.setTimezone("yourTimeZone");
        Map<String, Object> deviceAttributes=new HashMap<>();
        deviceAttributes.put("yourAttributeId",yourAttributeValue);
        Map<String, String> deviceTags=new HashMap<>();
        deviceTags.put("yourTagKey","yourTagValue");
        request.setDeviceAttributes(deviceAttributes);
        request.setDeviceTags(deviceTags);

        StringI18n stringI18n=new StringI18n();
        stringI18n.setDefaultValue("testforname");
        request.setDeviceName(stringI18n);
        UpdateDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, UpdateDeviceResponse.class);

    }
}
```