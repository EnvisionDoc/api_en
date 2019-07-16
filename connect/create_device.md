# Create Device



Create devices.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/devices?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|----------------|---------------|--------------------------|---|
|productKey    | True          | String       | Product Key identifier     |
|timezone | True          | String         | Timezone where the device is located     |
| deviceName | True          | StringI18n | Device name         |
| deviceAttributes | False         | Map       | Device attributes         |
| deviceKey   | False         | String    | Device Key identifier         |
| deviceDesc  | False         | String    | Device description     |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    DeviceCreateResult structure        | Returned results for device creation. See [DeviceCreateResult Structure](/docs/api/en/latest/connect/create_device.html#id3) |


### DeviceCreateResult structure

| Name | Data Type | Description |
|------------------|-----------------------|----------------------------|
| productKey       | String                            | Product Key identifier                                                               |
| deviceName       | StringI18n                        | Device name                                                                   |
| deviceSecret     | String                            | Device connection key                                                             |
| assetId  | String         |Asset ID|


## Error Codes

| Code| Data Type | Description |
|-----------|----------------|----------------------|
| 11702 |                | `deviceKey` already exists in the database (when `deviceKey` is provided)        |
| 11714 |                | The key of the device cannot be assigned temporarily (when the `deviceKey` is not provided). Try again. |
| 11739 |                | This operation will cause that the defined number of devices under the product exceeds the limit |




## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=create&orgId=o15475450989191
method:  POST
requestBody:  {
    "deviceTags":{
        "test":"test for tags"
    },
    "timezone":"+08:00",
    "source":0,
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
responseBody:  {
    "code":0,
    "msg":"OK",
    "requestId":"fd79d0f5-69c5-4fa8-add4-69f5ca1b635f",
    "data":{
        "assetId":"Uvmm5AXU",
        "productKey":"yourProductKey",
        "deviceKey":"yourDeviceKey",
        "deviceSecrete":"Z5YtZaQpK5IWocakV7zQ"
    }
}
```

