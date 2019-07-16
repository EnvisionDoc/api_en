# Get Device



Get the device information.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/devices?action=get
```

## Request Parameters (URI)

.. note:: In the following non-required fields, you must provide `assetId` or a combination of `productKey` and `deviceKey` to specify the device.

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key identifier     |
| deviceKey | Query           | False      | String       | Device Key identifier         |
    

## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data | Device structure                          | Gateway device information. See [Device Structure](/docs/api/en/latest/connect/get_device.html#id3) |


### Device structure

| Name | Data Type | Description |
|------------------|-----------------------|----------------------------|
| orgId |  String | Organization ID which the asset belongs to |
| assetId  | String         |Asset ID|
| modelId             | String                          | Model ID which the asset belongs to|
| modelIdPath      | String                            | Model ID path                                                               |
| productKey       | String                            | Product Key identifier                                                               |
| productName      | StringI18n                        | Product name                                                                |
| productType      | String                            | Product type                                                                  |
| dataFormat       | String                            | Data format. Custom means that any user-customized data format is supported, while Json means that only the EnOS device protocol formats are supported |
| deviceKey        | String                            | Device Key identifier                                                                   |
| deviceName       | StringI18n                        | Device name                                                                   |
| deviceSecret     | String                            | Device connection key                                                             |
| deviceDesc       | String                            | Device description                                                                   |
| timezone         | String                            | Timezone where the device is located                                                               |
| deviceAttributes | Map (Key is of String type and the value is of String type) | Device attributes                                                                 |
| deviceTags       | Map (Key is of String type and the value is of String type) | Device marks                                                                 |
| createTime       | Long                              | Device creation time                                                             |
| status           | String                            | Device status (online, offline, inactive or disable)                         |
| activeTime       | Long                              | Device activation time                                                             |
| lastOnlineTime   | Long                              | Last online time of device                                                       |
| lastOnlineTime   | Long                              | Last offline time of device                                                       |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=get&orgId=o15475450989191&assetId=9HhK0YxX
method:  GET
headers:  {}
requestBody:  null
```

### Return Sample

```json
responseBody:  {
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
		"lastOfflineTime": 1560744111658
	}
}
```

