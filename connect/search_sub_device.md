# Search Sub-Device

Search for sub-devices under the specified gateway.

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
POST https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevice
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
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - gateway
     - Mandatory
     - DeviceIdentfier Struct
     - Information of the gateway the sub-devices are under. For details, see `DeviceIdentfier Struct>> </docs/api/en/2.1.0/connect/search_sub_device.html#deviceidentifier-struct-di>`_
   * - expression
     - Optional
     - String
     - The query expression, which supports sql-like query. The fields that are supported for query include: ``modelId`` , ``deviceAttributes`` , ``deviceTags``, ``productKey``, ``deviceKey``, ``assetId``, ``deviceName``, and ``status``.

       + ``deviceAttributes``: supports arithmetic operator "=", "exists", "not exists", and "in". To use this parameter in a query, you need to use the format *deviceAttributes.attributeId* to specify an attribute. For example, "deviceAttributes.temperature"=35.5.
       + ``deviceTags``: supports arithmetic operator "=", "exists", "not exists", and "in". To use this parameter in a query, you need to use the format *deviceTags.keyName* to specify the key of a tag. For example, "deviceTags.Region" = "China"
       + ``modelId`` , ``productKey`` , ``deviceKey`` , and ``assetId`` : support arithmetic operators "=" and "in"
       + ``deviceName``: supports fuzzy inquiry of the specified language:

         * ``deviceName like ‘xxx’``: fuzzy inquiry of the default name, Chinese name, and English name
         * ``deviceName.default like ‘xxx’``: fuzzy inquiry of the default name
         * ``deviceName.zh_CN like ‘xxx’``: fuzzy inquiry of the Chinese name. If no Chinese name exists, fuzzy inquiry of default name
         * ``deviceName.en_US like ‘xxx’``: fuzzy inquiry of the English name. If no English name exists, fuzzy inquiry of default name

       + ``status``: supports arithmetic operator "=", valid values are: "inactive", "online", "offline", and "disable"

       `How to use expression>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`_

   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. When not specified, 10 entries are displayed per page by default. ``sorters`` is not supported to sort the response. The maximum records per page is 200. For details, see `Pagination Request Struct>> </docs/api/en/2.1.0/overview.html#pagination-request-struct>`_
   * - projection
     - Optional
     - Projection Struct
     - Enables you to crop the data result set returned in the request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see `How does projection crop the result set>> </docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set>`_



### DeviceIdentifier Struct   <di>

Note: Use either the (``assetId``) or (``productKey`` + ``deviceKey``) for the following.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | String         | The product key. To be used with ``deviceKey``. |
| deviceKey | String         | The device key. To be used with ``productKey``.  |




## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | Array of Device Structs                     | A list of the devices returned. For the details of a Device Struct, see [Device Struct](/docs/api/en/2.1.0/connect/search_sub_device.html#device-struc-device).    |


### Device Struct  <device>

| Name | Data Type | Description |
|------------------|--------------------|-------|
| orgId          | String                |  The organization ID which the asset belongs to.|
| assetId  | String         |The asset ID.|
| modelId             | String                          | The model ID which the asset belongs to.|
| modelIdPath      | String                            | The model ID path.                                                               |
| productKey       | String                            | The product key.                                                               |
| productName      | StringI18n                        | The product name.                                                                |
| productType      | String                            | The product type.                                                                  |
| dataFormat       | String                            | <ul><li>"Custom" represents the user-defined data type</li><li>"Json" represents the json data type</li></ul> |
| deviceKey        | String                            | The device key.                                                                   |
| deviceName       | StringI18n                        | The device name.                                                                 |
| deviceSecret     | String                            | The device secret identifier. |
| deviceDesc       | String                            | The device description.                      |
| timezone         | String                            | Timezone of the device's location.                                                               |
| deviceAttributes | Map | The device attributes. The Key is the attribute ID, and the Value type depends on the attribute defined in the ``ThingModel``.       |
| deviceTags       | Map  | The device tags. (The Key and Value are of String type.)        |
| createTime       | Long                              | The time when the device was created.                                                           |
| status           | String                            | The device status (online, offline, inactive, or disabled).                        |
| activeTime       | Long                              | The time when the device was activated.                |
| lastOnlineTime   | Long                              | The last online time of the device. |
| lastOfflineTime   | Long                              | The last offline time of the device.  |
| measurepointLastUpdate  | Long                              | The last time when a measurement point was updated.      |
| eventLastUpdate  | Long                              | The last time when an event was updated.                                                       |
| attributeLastUpdate  | Long                              | The last time when an attribute was updated.                                                       |
| featureLastUpdate  | Long                              | The last time when a measurement point, an event, or an attribute was updated. |



## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |  Not Gateway   | The device specified in ``gateway`` is not a gateway.               |


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevices&orgId=yourOrgId
method: POST
requestBody: {"gateway":{"assetId":"yourAssetId"}}
```

### Return Sample

```json
{
		"code": 0,
		"msg": "OK",
		"requestId": "498d1c5b-7c4f-401a-a9ff-9072931bec2e",
		"data": [{
			"orgId": "yourOrgId",
			"assetId": "mAEsF3sm",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "yourProductKey",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue":{
					"en_US":"",
					"zh_CN":""
            	}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "yourDeviceKey",
			"deviceName": {
				"defaultValue": "testforCreatedevice",
				"i18nValue":{
					"en_US":"",
					"zh_CN":""
            	}
			},
			"deviceSecret": "yourDeviceSecret",
			"deviceDesc": "test for createdevice",
			"timezone": "+08:00",
			"deviceAttributes": {
				"testatt": 111111
			},
			"deviceTags": {},
			"createTime": 1560755091998,
			"status": "inactive",
			"activeTime": 0,
			"lastOnlineTime": 0,
			"lastOfflineTime": 0,
      "measurepointLastUpdate": null,
      "eventLastUpdate": null,
      "attributeLastUpdate": null,
      "featureLastUpdate": null
		}, {
			"orgId": "yourOrgId",
			"assetId": "gVRwKQ3C",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "yourProductKey",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue":{
					"en_US":"",
					"zh_CN":""
            	}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "yourDeviceKey",
			"deviceName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue":{
					"en_US":"",
					"zh_CN":""
            	}
			},
			"deviceSecret": "yourDeviceSecret",
			"deviceDesc": null,
			"timezone": "+10:00",
			"deviceAttributes": {},
			"deviceTags": {},
			"createTime": 1560730295671,
			"status": "offline",
			"activeTime": 1560730567958,
			"lastOnlineTime": 1560743932166,
			"lastOfflineTime": 1560744112166,
      "measurepointLastUpdate": null,
      "eventLastUpdate": null,
      "attributeLastUpdate": null,
      "featureLastUpdate": null
		}],
		"pagination":{"sortedBy":null,"pageNo":1,"pageSize":2,"totalSize":2}}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device.topo;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.device.topo.SearchSubDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.topo.SearchSubDeviceResponse;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;

public class SearchSubDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        SearchSubDeviceRequest request = new SearchSubDeviceRequest();
        request.setOrgId(orgId);
        request.setGateway(new DeviceIdentifier("J1Rqyaqz"));

        SearchSubDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, SearchSubDeviceResponse.class);
    }
}
```
