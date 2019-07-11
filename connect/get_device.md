# Get Device

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Get the device information.

## Request format

```
https://{apigw-address}/connect-service/v2.1/devices?action=get
```

## Request parameters (URI)

Note: In the following non-mandatory fields, you must provide a combination of `assetId` or `productKey` and `deviceKey` to specify the device.

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| assetId  | Query            | False   | String         | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device key          |
    

## Response parameters

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
| productKey       | String                            | Product Key                                                                |
| productName      | StringI18n                        | Product name                                                                |
| productType      | String                            | Product type                                                                  |
| dataFormat       | String                            | Data format. Custom means that any user-customized data format is supported, while Json means that only the EnOS device protocol formats are supported |
| deviceKey        | String                            | Device key                                                                    |
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

### Request sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=get&orgId=o15475450989191&assetId=9HhK0YxX
method:  GET
headers:  {}
requestBody:  null
```

### Return sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "835a5cc4-4487-4bf2-961a-55bc0ee77d02",
	"data": {
		"orgId": "o15475450989191",
		"assetId": "9HhK0YxX",
		"modelId": "abc-test",
		"modelIdPath": "/abc-test",
		"productKey": "mJo2gO5u",
		"productName": {
			"defaultValue": "abc-pk",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "VcwTHRvYFb",
		"deviceName": {
			"defaultValue": "testforname",
			"i18nValue": {}
		},
		"deviceSecret": "hOiv7SJAYuyVJp3CXJWJ",
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

