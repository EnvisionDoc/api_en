# Invoke Service

Service invocation interface for the device.

This interface can execute cached commands or instant commands. When executing instant commands, the interface response data is returned after the device returns the service invocation results. If the device does not return the service invocation results within the specified service execution timeout period, the EnOS service invocation will wait for the timeout and then return the interface response data.

When executing cached commands, the data will be returned directly after being cached.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Control

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/commands?action=invokeService
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request



| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query            | Optional (See **Note** above)   | String         | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | Optional (See **Note** above)       | String       | The product key. To be used with ``deviceKey``.     |
| deviceKey | Query           | Optional (See **Note** above)      | String       | The device key. To be used with ``productKey``.         |
| serviceId      | Query| Mandatory| String    | The ID of the invoked service. |
| pendingTtl     | Query| Optional| Integer    | The cache storage time. Its unit is seconds and its range is [0 - 172800 (i.e. 48 hours)], which is 0 by default. If the pendingTtl is 0, it indicates that the commands will be executed immediately.  |
| timeout        | Query| Optional         | Integer    | The timeout period of the service execution in seconds. Its range is [1-60] with a default value of 30 seconds.|

## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|-----------|---------------|-------------------|----------|
| inputData | Mandatory| Map (Key is of String type and the Value is of String, Number, Array or Object type) | The input parameter for service invocation. The key is the parameter identifier, and the value data type will be as per defined in the ``ThingModel``.  |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Service Invocation Return Struct      | The service invocation results. For details, see [Service Invocation Return Struct](/docs/api/en/2.1.0/connect/invoke_service.html#service-invocation-return-struct-invo). |


### Service Invocation Return Struct <invo>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| commandId  | String| The command ID|
| outputData | Map (Key is of String type and the Value is of String, Number, Array or Object type) | If the request's pendingTtl is 0 (i.e. the requested commands are executed immediately), the device service invocation results are returned, where the value data type will be as per defined in the ``ThingModel``. If the request's ``pendingTtl`` is not 0 (i.e. the requested commands are cached for execution later), this parameter will not be returned.  |

## Error Codes

| Code | Description    |
|-------|-------------|
| 11904 | The command is not sent, and the instant command timed out.    |
| 11915 | The command is sent, but the response timed out.                  |
| 11902 | The number of cached commands reached the upper limit.                                   |
| 11900 | The device is offline and the instant command cannot be sent.                                     |
| 11810 | The command is not able to encode/convert to the product's custom data format. |
| 11888 | The device is not activated and the instant command cannot be sent.                        |


## Samples

### Request Sample

```
url: https://{apigw-address}/connect-service/v2.1/commands?action=invokeService&deviceKey=yourDeviceKey&pendingTtl=1000&productKey=yourProductKey&serviceId=identifier&orgId=yourOrgId&timeout=30
method: POST
requestBody:
{
  "inputData":{
    "canshu2":22.2,
    "canshu1":11
  }
}
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
