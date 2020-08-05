# Enable Device

Activate a device.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.1/devices?action=enable
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device to be activated:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request



| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query          | Optional (See **Note** above)      | String        | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query         | Optional (See **Note** above)     | String         | The product key. To be used with ``deviceKey``.     |
| deviceKey | Query         | Optional (See **Note** above)    | String          | The device key. To be used with ``productKey``.         |



## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11794 |   Device status is invalid   | The device has already been activated.             |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/devices?action=enable&orgId=yourOrgId&assetId=yourAssetId
method: POST
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "06dd8ea3-cb9e-4628-8f93-d36c416bcd3a",
	"data": null
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.device.*;


public class EnableDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String assetId = "yourAssetId";
        EnableDeviceRequest request = new EnableDeviceRequest();
        request.setOrgId(orgId);
        request.setAssetId(assetId);
        EnableDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, EnableDeviceResponse.class);

    }
}
```
