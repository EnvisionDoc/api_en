# Invoke Service




Release a service invocation interface to the device.

This interface can execute cached commands or instant commands. When executing instant commands, the interface response data is returned after the device returns the service invocation results. If the device does not return the service invocation results within the specified service execution timeout period, the EnOS service invocation will wait for the timeout and then return the interface timeout response.

When executing cached commands, it will be returned directly after being cached.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=invokeService
```

## Request Parameters (URI)

.. note:: In the following non-required fields, you must provide ``assetId`` or a combination of ``productKey`` and ``deviceKey`` to specify the device.

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | False       | String       | Product Key     |
| deviceKey | Query           | False      | String       | Device Key         |
| serviceId      | Query| True | String    | ID of the invoked service |
| pendingTtl     | Query| False| Integer    | Cache storage time. Its unit is second and its range is [0 - 172800 (i.e. 48 hours)], which is 0 by default. If the pendingTtl is 0, it indicates that the commands will be executed immediately.  |
| timeout        | Query| False         | Integer    | Timeout period of service execution in seconds. Its range is [1-60], which is set as 30 seconds by default|

## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------|---------------|-------------------|----------|
| inputData | True| Map (Key is of String type and the Value is of String, Number, Array or Object type) | Input parameter for service invocation. The key is the parameter identifier, and the value type must conform to the definition of `ThingModel`.  |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Service invocation return struct      | Service invocation results. See [Service Invocation Return Struct](/docs/api/en/2.0.9/connect/invoke_service.html#service-invocation-return-struct-invo). |


### Service Invocation Return Struct <invo>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| commandId  | String| Command ID|
| outputData | Map (Key is of String type and the Value is of String, Number, Array or Object type) | If the request's pendingTtl is 0 (i.e. the requested commands are executed immediately), the device service invocation results are returned, which must conform to the definition of `ThingModel`. If the request's `pendingTtl` is not 0 (i.e. the requested commands are cached for execution later), this parameter will not be returned.  |

## Error Codes

| Code | Description    |
|-------|-------------|
| 11904 | Command is not sent, and instant command timed out                         |
| 11915 | Command is sent, but response timed out                  |
| 11902 | The number of cached commands reaches the upper limit                                   |
| 11900 | The device is offline and the instant command cannot be sent.                                     |
| 11810 | The command can not be encoded into the product-customized format when the product supports custom data formats |
| 11888 | The device is not activated and the instant command cannot be sent.                        |


## Sample 1

### Request Sample

```
https://{apigw-address}/connect-service/v2.1/commands?action=invokeService&deviceKey=zBAofs6D4s&pendingTtl=1000&productKey=6Bt59ySj&serviceId=identifier&orgId=o15535059999891&timeout=30
method: POST
requestBody:
{"inputData":{"canshu2":22.2,"canshu1":11}}
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
        "outputData": {
        }
    }
}
```

