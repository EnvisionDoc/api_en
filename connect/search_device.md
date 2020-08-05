# Search Device

Search for devices based on the search criteria.

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
POST https://{apigw-address}/connect-service/v2.1/devices?action=search
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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__


## Request Parameters (Body)


.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - expression
     - Optional
     - String
     - The query expression, which supports sql-like query. The fields that are supported for query include: ``modelId`` , ``deviceAttributes`` , ``deviceTags``, ``productKey``, ``deviceKey``, ``assetId``, ``productType``, ``deviceName``, and ``status``.

       + ``deviceAttributes``: supports arithmetic operator "=", "exists", "not exists", and "in". To use this parameter in a query, you need to use the format *deviceAttributes.attributeId* to specify an attribute. For example, "deviceAttributes.temperature"=35.5.
       + ``deviceTags``: supports arithmetic operator "=", "exists", "not exists", and "in". To use this parameter in a query, you need to use the format *deviceTags.keyName* to specify the key of a tag. For example, "deviceTags.Region" = "China"
       + ``modelId`` , ``productKey`` , ``deviceKey`` , and ``assetId`` : support arithmetic operators "=" and "in"
       + ``productType``: supports arithmetic operator "=", valid values are: "Device" and "Gateway"
       + ``deviceName``: supports fuzzy inquiry of the specified language:

         * ``deviceName like ‘xxx’``: fuzzy inquiry of the default name, Chinese name, and English name
         * ``deviceName.default like ‘xxx’``: fuzzy inquiry of the default name
         * ``deviceName.zh_CN like ‘xxx’``: fuzzy inquiry of the Chinese name. If no Chinese name exists, fuzzy inquiry of default name
         * ``deviceName.en_US like ‘xxx’``: fuzzy inquiry of the English name. If no English name exists, fuzzy inquiry of default name

       + ``status``: supports arithmetic operator "=", valid values are: "inactive", "online", "offline", and "disable"

       `How to use expression>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`__

   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. If not specified, the default pagination size is 10 pages. The maximum records per page is 200. **Note:** Does not support ``sorters`` Struct. The results will be sorted in descending order according to ``createTime``. For more details, see `Pagination Request Struct </docs/api/en/2.1.0/overview.html#pagination-request-struct>`__
   * - projection
     - Optional
     - Projection Struct
     - Enables you to crop the data result set returned in the request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see `How does projection crop the result set? </docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set>`__


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of Device Structs
     - A list of the devices returned. For the details of a device struct, see `Device Struct </docs/api/en/2.1.0/connect/search_device.html#device-struct-device>`_ .




### Device Struct <device>

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
     - 
       + "Custom" represents the user-defined data type.
       + "Json" represents the JSON data type.
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
url: https://{apigw-address}/connect-service/v2.1/devices?action=search&orgId=yourOrgId
method: POST
requestBody:  
{
	"pagination": {
		"pageNo": 2,
		"pageSize": 5
	}
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"59ecd409-7baa-4726-ba10-c0bde35ffb09",
	"data":[
		{
			"orgId":"yourOrgId",
			"assetId":"yourAssetId",
			"modelId":"lxctimelooker",
			"modelIdPath":"/lxctimelooker",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"lxcpro",
				"i18nValue":{

				}
			},
			"productType":"Device",
			"dataFormat":"Json",
			"deviceKey":"yourDeviceKey",
			"deviceName":{
				"defaultValue":"time2dev11",
				"i18nValue":{

				}
			},
			"deviceSecret":"yourDeviceSecret",
			"deviceDesc":null,
			"timezone":"+09:00",
			"deviceAttributes":{

			},
			"deviceTags":{

			},
			"createTime":1558421750575,
			"status":"offline",
			"activeTime":1558482329972,
			"lastOnlineTime":1560743915454,
			"lastOfflineTime":1560744095454,
			"measurepointLastUpdate":null,
			"eventLastUpdate":null,
			"attributeLastUpdate":null,
			"featureLastUpdate":null
		},
		{
			"orgId":"yourOrgId",
			"assetId":"Fi0HQ8FO",
			"modelId":"AlterTest0615",
			"modelIdPath":"/AlterTest0615",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"AlterTest0615_Product",
				"i18nValue":{

				}
			},
			"productType":"Device",
			"dataFormat":"Json",
			"deviceKey":"yourDeviceKey",
			"deviceName":{
				"defaultValue":"AlterTest0615",
				"i18nValue":{

				}
			},
			"deviceSecret":"yourDeviceSecret",
			"deviceDesc":null,
			"timezone":"+08:00",
			"deviceAttributes":{

			},
			"deviceTags":{

			},
			"createTime":1560564762147,
			"status":"offline",
			"activeTime":1560564838673,
			"lastOnlineTime":1560743931247,
			"lastOfflineTime":1560743931712,
			"measurepointLastUpdate":null,
			"eventLastUpdate":null,
			"attributeLastUpdate":null,
			"featureLastUpdate":null
		},
		{
			"orgId":"yourOrgId",
			"assetId":"6FytqleL",
			"modelId":"AlterTest0614",
			"modelIdPath":"/AlterTest0614",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"AlterTest0614_Product",
				"i18nValue":{

				}
			},
			"productType":"Device",
			"dataFormat":"Json",
			"deviceKey":"yourDeviceKey",
			"deviceName":{
				"defaultValue":"AlterTest0614",
				"i18nValue":{

				}
			},
			"deviceSecret":"yourDeviceSecret",
			"deviceDesc":null,
			"timezone":"+08:00",
			"deviceAttributes":{
				"aaa":1,
				"76":0
			},
			"deviceTags":{

			},
			"createTime":1560493341919,
			"status":"offline",
			"activeTime":1560493435761,
			"lastOnlineTime":1560743930253,
			"lastOfflineTime":1560743930346,
			"measurepointLastUpdate":null,
			"eventLastUpdate":null,
			"attributeLastUpdate":null,
			"featureLastUpdate":null
		},
		{
			"orgId":"yourOrgId",
			"assetId":"yourAssetId",
			"modelId":"yourModelId",
			"modelIdPath":"yourModelIdPath",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"AlertTest0613_Product",
				"i18nValue":{

				}
			},
			"productType":"Device",
			"dataFormat":"Json",
			"deviceKey":"yourDeviceKey",
			"deviceName":{
				"defaultValue":"AlertTest0613",
				"i18nValue":{

				}
			},
			"deviceSecret":"yourDeviceSecret",
			"deviceDesc":null,
			"timezone":"+08:00",
			"deviceAttributes":{
				"aaa":1,
				"76":0
			},
			"deviceTags":{

			},
			"createTime":1560389949661,
			"status":"offline",
			"activeTime":1560390227903,
			"lastOnlineTime":1560743916848,
			"lastOfflineTime":1560743929003,
			"measurepointLastUpdate":null,
			"eventLastUpdate":null,
			"attributeLastUpdate":null,
			"featureLastUpdate":null
		},
		{
			"orgId":"yourOrgId",
			"assetId":"yourAssetId",
			"modelId":"yourModelId",
			"modelIdPath":"yourModelIdPath",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"zccp-----1",
				"i18nValue":{

				}
			},
			"productType":"Device",
			"dataFormat":"Json",
			"deviceKey":"yourDeviceKey",
			"deviceName":{
				"defaultValue":"zccp-----222",
				"i18nValue":{

				}
			},
			"deviceSecret":"yourDeviceSecret",
			"deviceDesc":null,
			"timezone":"+08:00",
			"deviceAttributes":{
				"timestamp1":1,
				"float1":1.0,
				"bool11":false,
				"int1":1,
				"string1":"1",
				"double1":1.0,
				"12221":false,
				"array1":[
					1
				],
				"stuct1":{
					"int11":1
				},
				"file1":"ftp://a.com/demo.txt",
				"enum":1,
				"dete1":"2019-05-06"
			},
			"deviceTags":{

			},
			"createTime":1559294746435,
			"status":"inactive",
			"activeTime":0,
			"lastOnlineTime":0,
			"lastOfflineTime":0,
			"measurepointLastUpdate":null,
			"eventLastUpdate":null,
			"attributeLastUpdate":null,
			"featureLastUpdate":null
		}
	],
	"pagination":{
		"sortedBy":null,
		"pageNo":2,
		"pageSize":5,
		"totalSize":6511
	}
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.api.common.constant.request.Projection;
import com.envisioniot.enos.connect_service.v2_1.device.SearchDeviceRequest;
import com.envisioniot.enos.connect_service.v2_1.device.SearchDeviceResponse;


public class SearchDevice {
    public static void main(String[] args) {
        final String appKey = "yourAppKey";
        final String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String assetId = "yourAssetId";
        SearchDeviceRequest request = new SearchDeviceRequest();
        request.setOrgId(orgId);
        String expression = "productKey='yourProductKey'";
        request.setExpression(expression);
        Pagination pagination = new Pagination();
        pagination.setPageSize(5);
        pagination.setPageNo(2);
        Projection projection = new Projection();
        projection.add(assetId);
        projection.add("productName");
        request.setPagination(pagination);
        request.setProjection(projection);
        SearchDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url(serverUrl)
            .getResponse(request, SearchDeviceResponse.class);
    }
}
```