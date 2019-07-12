# Set Measurepoint



Measurepoint setting interface.

This interface is used to execute cached commands or instant commands. When an instant command is executed, the interface response data is returned after the device returns the measurepoint setting results. If the device does not return the measurepoint setting results within the specified measurepoint setting timeout period, the EnOS measurepoint setting will wait for the timeout period and then return the interface timeout response data.

In case of a cached command, it will be returned to the user directly after being cached.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=setMeasurepoint
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device key          |
| measurepointId      | Query| True | String    | Asset measurepoint. [How to get pointId](/docs/api/en/latest/api_faqs.html#how-to-get-the-measuremet-point-pointid-pointid) |
| pendingTtl     | Query| False| Integer    | Cache storage time. Its unit is second and its range is [0 - 172800 (i.e. 48 hours)], which is 0 by default. If the pendingTtl is 0, it indicates that the commands will be executed immediately.  |
| timeout        | Query| False         | Integer    | Service execution timeout time in seconds. Its range is [1-60], which is set as 30 seconds by default|

## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------|---------------|-------------------|----------|
| value | True| String, Number, Array or Object | Parameter value for measurepoint setting, which needs to conform to the definition of `ThingModel`.  |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Measurepoint setting return structure      | Measurepoint setting results. See [Measurepoint Setting Return Structure](/docs/api/en/latest/connect/set_measurepoint.html#id4) |


### Measurepoint setting return structure

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| commandId  | String| Command ID|

## Error Codes

| Code | Description    |
|-------|------------------------------------------------------------------|
| 11904 | Command is not sent, and instant command timed out                         |
| 11915 | Command is sent, but response timed out                  |
| 11902 | The number of cached commands reaches the upper limit                                   |
| 11900 | The device is offline and the instant command cannot be sent.                                     |
| 11810 | The command can not be encoded into the product-customized format when the product supports custom data formats |
| 11888 | The device is not activated and the instant command cannot be sent.                        |


## Sample 1

### Request Sample

```
https://{apigw-address}/connect-service/v2.1/commands?measurepointId=measurepoint1&action=setMeasurepoint&deviceKey=zBAofs6D4s&pendingTtl=1000&productKey=6Bt59ySj&orgId=o15535059999891&timeout=30

{"value":1.0}
```

### Return Sample

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": {
        "commandId": "2078724684846989312",
     }
}
```

