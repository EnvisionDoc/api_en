# Remove Sub-Device



Remove the sub-device from the gateway (remove the topological relationship).

## Request format

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=removeSubDevice
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|--------------------|----------|-----------|--------------|
| gateway | True      |DeviceIdentfier structure | Gateway information that needs to add sub-device. See [DeviceIdentfier structure] (/docs/api/en/latest/connect/remove_sub_device.html#deviceidentifier) |
| subDevices           | True      | DeviceIdentfier structure | Information of the list of the sub-devices to be added into the specified getaway. See [DeviceIdentfier Structure](/docs/api/en/latest/connect/remove_sub_device.html#deviceidentifier) |


### DeviceIdentifier structure

Note: The `assetId` or `(productKey, deviceKey)` must be provided for the following fields.

| Name | Data Type | Description |
|----------------|----------------|------------------|
| assetId  | String        | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)|
| productKey | String         | Product Key      |
| deviceKey | String         | Device key          |




## Response parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data | String                           | (null)               |


## Error codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | The parameter gateway is not a gateway device                |
| 11795 |                | The provided sub-device has an existing topology or is used as a gateway.      |


## Sample 1

### Request sample

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=remove&orgId=o15475450989191
 method:  POST
requestBody:  {"subDevices":[{"assetId":"gVRwKQ3C"}],"gateway":{"assetId":"J1Rqyaqz"}}
```

### Return sample

```json
responseBody:{"code":0,"msg":"OK","requestId":"ea6608bb-b8cb-46f3-a836-ee24ea9a028c","data":null}
```

