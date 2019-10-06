# Remove Sub-Device



Remove the sub-device from the gateway (remove the topological relationship).

## Request Format

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=removeSubDevice
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| gateway | True      |DeviceIdentfier struct | Information of the gateway that needs to remove the sub-device. See [DeviceIdentfier Struct](/docs/api/en/latest/connect/remove_sub_device.html#deviceidentifier-struct-di). |
| subDevices           | True      | DeviceIdentfier struct | List information of the sub-devices to be remved from the specified getaway. See [DeviceIdentfier Struct](/docs/api/en/latest/connect/remove_sub_device.html#deviceidentifier-struct-di). |


### DeviceIdentifier Struct  <di>

Note: The `assetId` or `(productKey, deviceKey)` must be provided for the following fields.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | Asset ID. [How to get assetId>>](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| productKey | String         | Product Key     |
| deviceKey | String         | Device Key          |




## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | String                           | (null)               |


## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | The device specified by `gateway` is not a gateway |
| 11795 |                | At least one provided sub-device is not under the specified gateway      |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=remove&orgId=o15475450989191
 method:  POST
requestBody:  {"subDevices":[{"assetId":"gVRwKQ3C"}],"gateway":{"assetId":"J1Rqyaqz"}}
```

### Return Sample

```json
responseBody:{"code":0,"msg":"OK","requestId":"ea6608bb-b8cb-46f3-a836-ee24ea9a028c","data":null}
```

