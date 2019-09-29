# Search Device



Query the device information.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/devices?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Required or Not
     - Data Type
     - Description
   * - expression
     - False
     - String
     - Query expression. The fields that are supported for query include:``productKey``, ``deviceKey``, ``assetId``, ``productType``, ``deviceName``, and ``status``.

       + ``productKey``, ``deviceKey``, and ``assetId``: support arithmetic operators "=" and "in";
       + ``productType``: supports arithmetic operator "=", valid values are: "Device" and "Gateway";
       + ``deviceName``: supports fuzzy inquiry of specified language:

         * ``deviceName like ‘xxx’``: fuzzy inquiry of default name, Chinese name, and English name;
         * ``deviceName.default like ‘xxx’``: fuzzy inquiry of default name;
         * ``deviceName.zh_CN like ‘xxx’``: fuzzy inquiry of Chinese name, if no Chinese name, fuzzy inquiry of default name;
         * ``deviceName.en_US like ‘xxx’``: fuzzy inquiry of English name, if no English name, fuzzy inquiry of default name

       + ``status``: upports arithmetic operator "=", valid values are: "inactive", "online", "offline", and "disable"

       `How to use expression </docs/api/en/2.0.9/api_faqs.html#how-to-use-expression>`__

   * - pagination
     - False
     - pagination request struct
     - Random pagination. User can not specify the sorting field. If not provided, the default pagination size is 10 pages. `Pagination Request Struct </docs/api/zh_CN/2.0.9/overview.html#pagination-request-struct>`__
   * - projection
     - False
     - Projection struct
     - Describe the object projection to be returned in the interface request. For details, see `How does projection crop the result set? </docs/api/en/2.0.9/api_faqs.html#how-does-projection-crop-the-result-set>`__


## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data | Device struct                     | Information of a group of sub-devices of the specified page under the gateway. See [Device Struct](/docs/api/en/2.0.9/connect/search_device.html#device-struct-device). |


### Device Struct  <device>

| Name | Data Type | Description |
|------------------|-----------------------|----------------------------|
| orgId |  String | Organization ID which the asset belongs to |
| assetId  | String         |Asset ID|
| modelId             | String                          | Model ID which the asset belongs to|
| modelIdPath      | String                            | Model ID path                                                               |
| productKey       | String                            | Product Key                                                               |
| productName      | StringI18n                        | Product name                                                                |
| productType      | String                            | Product type                                                                  |
| dataFormat       | String                            | Data format. Custom means that any user-customized data format is supported, while Json means that only the EnOS device protocol formats are supported. |
| deviceKey        | String                            | Device Key                                                                   |
| deviceName       | StringI18n                        | Device name                                                                   |
| deviceSecret     | String                            | Device connection key                                                             |
| deviceDesc       | String                            | Device description                                                                   |
| timezone         | String                            | Timezone where the device is located                                                               |
| deviceAttributes | Map (Key is of String type and the value is of String type) | Device attributes                                                                 |
| deviceTags       | Map (Key is of String type and the value is of String type) | Device tags                                                                 |
| createTime       | Long                              | Device creation time                                                             |
| status           | String                            | Device status (online, offline, inactive or disable)                         |
| activeTime       | Long                              | Device activation time                                                             |
| lastOnlineTime   | Long                              | Last online time of device                                                       |
| lastOnlineTime   | Long                              | Last offline time of device                                                       |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=search&orgId=o15475450989191
method:  POST
requestBody:  {
	"pagination": {
		"pageNo": 2,
		"pageSize": 5
	}
}
```

### Return Sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "59ecd409-7baa-4726-ba10-c0bde35ffb09",
	"data": [{
		"orgId": "yourOrgId",
		"assetId": "7u4bfyO0",
		"modelId": "lxctimelooker",
		"modelIdPath": "/lxctimelooker",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "lxcpro",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "time2dev11",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+09:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1558421750575,
		"status": "offline",
		"activeTime": 1558482329972,
		"lastOnlineTime": 1560743915454,
		"lastOfflineTime": 1560744095454
	}, {
		"orgId": "yourOrgId",
		"assetId": "Fi0HQ8FO",
		"modelId": "AlterTest0615",
		"modelIdPath": "/AlterTest0615",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "AlterTest0615_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "AlterTest0615",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1560564762147,
		"status": "offline",
		"activeTime": 1560564838673,
		"lastOnlineTime": 1560743931247,
		"lastOfflineTime": 1560743931712
	}, {
		"orgId": "yourOrgId",
		"assetId": "6FytqleL",
		"modelId": "AlterTest0614",
		"modelIdPath": "/AlterTest0614",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "AlterTest0614_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "AlterTest0614",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"aaa": 1,
			"76": 0
		},
		"deviceTags": {},
		"createTime": 1560493341919,
		"status": "offline",
		"activeTime": 1560493435761,
		"lastOnlineTime": 1560743930253,
		"lastOfflineTime": 1560743930346
	}, {
		"orgId": "yourOrgId",
		"assetId": "V4TjS0n4",
		"modelId": "AlertTest0613",
		"modelIdPath": "/AAA100/AlertTest0613",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "AlertTest0613_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "AlertTest0613",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"aaa": 1,
			"76": 0
		},
		"deviceTags": {},
		"createTime": 1560389949661,
		"status": "offline",
		"activeTime": 1560390227903,
		"lastOnlineTime": 1560743916848,
		"lastOfflineTime": 1560743929003
	}, {
		"orgId": "yourOrgId",
		"assetId": "wjIXsqTQ",
		"modelId": "zcmx---1",
		"modelIdPath": "/zcmx---1",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "zccp-----1",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "zccp-----222",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"timestamp1": 1,
			"float1": 1.0,
			"bool11": false,
			"int1": 1,
			"string1": "1",
			"double1": 1.0,
			"12221": false,
			"array1": [1],
			"stuct1": {
				"int11": 1
			},
			"file1": "ftp://a.com/demo.txt",
			"enum": 1,
			"dete1": "2019-05-06"
		},
		"deviceTags": {},
		"createTime": 1559294746435,
		"status": "inactive",
		"activeTime": 0,
		"lastOnlineTime": 0,
		"lastOfflineTime": 0
	}],
	"pagination": {
		"sortedBy": null,
		"pageNo": 2,
		"pageSize": 5,
		"totalSize": 6511
	}
}
```
