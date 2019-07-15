# Search Sub-Device



Search the sub-device information under the gateway.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevice
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| gateway | True      |DeviceIdentfier structure | Gateway information that needs to add sub-device. See [DeviceIdentfier structure](/docs/api/en/latest/connect/search_sub_device.html#deviceidentifier) |
| pagination  | False      | Pagination request structure  | Paging parameter; if not specified, 10 entries are displayed per page by default. Currently, sorting is not supported (sorting fields ignored). See [Pagination Request Structure](/docs/api/en/latest/overview.html#pagination-request-structure) |


### DeviceIdentifier structure

Note: The `assetId` or `(productKey, deviceKey)` must be provided for the following fields.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | String         | Product Key      |
| deviceKey | String         | Device key          |




## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | Device structure                     | Information of a group of sub-devices of the specified page under the gateway. See [Device Structure](/docs/api/en/latest/connect/search_sub_device.html#id3)    |


### Device structure

| Name | Data Type | Description |
|------------------|--------------------|-------|
| orgId          | String                |  Organization ID which the asset belongs to|
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



## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | The parameter gateway is not a gateway device                |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevices&orgId=o15475450989191
method:  POST
requestBody:  {"gateway":{"assetId":"J1Rqyaqz"}}
```

### Return Sample

```json
responseBody:  {
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
				"i18nValue": {}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "yourDeviceKey",
			"deviceName": {
				"defaultValue": "testforCreatedevice",
				"i18nValue": {}
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
			"lastOfflineTime": 0
		}, {
			"orgId": "yourOrgId",
			"assetId": "gVRwKQ3C",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "yourProductKey",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "yourDeviceKey",
			"deviceName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
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
			"lastOfflineTime": 1560744112166
		}],
		"pagination":{"sortedBy":null,"pageNo":1,"pageSize":2,"totalSize":2}}
```

