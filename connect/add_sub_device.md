# Add Sub-Device



Add a new sub-device to the gateway device (creating topological relationship).

## Request Format

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=addSubDevice
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| gateway | True      |DeviceIdentfier structure | Information of the gateway that needs to be added sub-device. See [DeviceIdentfier structure](/docs/api/en/latest/connect/add_sub_device.html#deviceidentifier) |
| subDevices           | True      | DeviceIdentfier structure | List information of the sub-devices to be added into the specified getaway. See [DeviceIdentfier Structure](/docs/api/en/latest/connect/add_sub_device.html#deviceidentifier)  |


### DeviceIdentifier structure

Note: The `assetId` or `(productKey, deviceKey)` must be provided for the following fields.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | String         | Product Key identifier      |
| deviceKey | String         | Device Key identifier       |




## Response Parameters

| Name | Data Type | Description |
|-------------|--------------------|----------------|
| data | String | (null)               |


## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | The device specified by `gateway` is not a gateway|
| 11739 |                |This operation will cause the number of sub-devices of the gateway to exceed the limit. |
| 11795 |                | The provided sub-device has an existing topology or is used as a gateway.      |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=addSubDevice&orgId=o15475450989191
method:  POST
{"subDevices":[{"assetId":"mAEsF3sm"}],"gateway":{"assetId":"J1Rqyaqz"}}
```

### Return Sample

```json
{"code":0,"msg":"OK","requestId":"5246f91c-f9ce-485c-a9f2-4cd8b7e1f0df","data":null}
```

