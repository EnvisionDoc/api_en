# Get Gateway



Get the gateway information corresponding to the sub-device.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=getGateway
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |



## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| subDevices           | True      | DeviceIdentfier structure | Information used to identify sub-devices. See [DeviceIdentfier structure] (/docs/api/en/latest/connect/get_gateway.html#deviceidentifier) |


### DeviceIdentifier structure

Note: The `assetId` or `(productKey, deviceKey)` must be provided for the following fields.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | String         | Product Key      |
| deviceKey | String         | Device key          |


## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | Device structure                          | Gateway device information. See [Device Structure](/docs/api/en/latest/connect/get_gateway.html#device-devicetstruc)               |


### Device structure <devicetstruc>

| Name | Data Type | Description |
|-------|-------|---------------------------|
| orgId |  String | Organization ID which the asset belongs to|
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

### Request Sample

```
POST
https://{apigw-address}/connect-service/v2.1/device-topos?action=getGateway&orgId=o15475450989191
{
"subDevice":{"assetId":"gVRwKQ3C"}
}
```

### Return Sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "49ef6c03-02a0-449b-ab1e-92812071de80",
	"data": {
		"orgId": "yourOrgId",
		"assetId": "J1Rqyaqz",
		"modelId": "AlterTest0617",
		"modelIdPath": "/AlterTest0617",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "testtopo",
			"i18nValue": {}
		},
		"productType": "Gateway",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "testtopo",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1560759829419,
		"status": "inactive",
		"activeTime": 0,
		"lastOnlineTime": 0,
		"lastOfflineTime": 0
	}
}
```
