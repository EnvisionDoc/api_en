# Invoke Service




Release a service invocation interface to the device.

This interface can execute cached commands or instant commands. When an instant command is executed, the interface response data is returned after the device returns the service invocation results. If the device does not return the service invocation results within the specified service execution timeout period, the EnOS service invocation will wait for the timeout period and then return the interface timeout response data.

In case of a cached command, it will be returned to the user directly after being cached.

## Request format

```
https://{apigw-address}/connect-service/v2.1/commands?action=invokeService
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | Device key          |
| serviceId      | Query| True | String    | Id of the service invoked|
| pendingTtl     | Query| False| Integer    | Cache storage time. Its unit is second and its range is [0 - 172800 (i.e. 48 hours)], which is 0 by default. If the pendingTtl is 0, it indicates that the commands will be executed immediately.  |
| timeout        | Query| False         | Integer    | Service execution timeout time in seconds. Its range is [1-60], which is set as 30 seconds by default|

## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------|---------------|-------------------|----------|
| inputData | True| Map (Key is of String type and the Value is of String, Number, Array or Object type) | Input parameter for service invocation. The key is the parameter identifier, and the value type needs to conform to the definition of `ThingModel`.  |




## Response parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Service invocation return structure      | Service invocation results. See [Service Invocation Return Structure](/docs/api/en/latest/connect/invoke_service.html#id4) |


### Service invocation return structure

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| commandId  | String| Command ID|
| outputData | Map (Key is of String type and the Value is of String, Number, Array or Object type) | If the request's pendingTtl is 0 (i.e. the requested commands are executed immediately), the device service invocation results are returned, which should conform to the definition of `ThingModel`. If the request's `pendingTtl` is not 0 (i.e. the requested commands are cached for execution later), this parameter will not be returned.  |

## Error codes

| Code | Description    |
|-------|------------------------------------------------------------------|
| 11904 | Command is not sent, and instant command timed out                         |
| 11915 | Command is sent, but response timed out                  |
| 11902 | The number of cached commands reaches the upper limit                                   |
| 11900 | The device is offline and the instant command cannot be sent.                                     |
| 11810 | The command can not be encoded into the product-customized format when the product supports custom data formats |
| 11888 | The device is not activated and the instant command cannot be sent.                        |


## Sample 1

### Request sample

```
https://{apigw-address}/connect-service/v2.1/commands?action=invokeService&deviceKey=zBAofs6D4s&pendingTtl=1000&productKey=6Bt59ySj&serviceId=identifier&orgId=o15535059999891&timeout=30

requestBody:
{"inputData":{"canshu2":22.2,"canshu1":11}}
```

### Return sample

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

