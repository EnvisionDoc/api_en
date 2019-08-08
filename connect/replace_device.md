# Replace Device

Replace the Device Key of a device without changing its asset ID (`assetId`). The interface will override the original Device Key and Device Secret of the registered device, re-assign a Device Key and generate a new Device Secret, and reset the device to non-activated status. The new device can be connected to EnOS with the replaced Device Key, and the data of old and new devices can be associated through asset IDs.

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/devices?action=replaceDevice
```

## Request Parameters (URI)


.. note:: In the following non-required fields, you must provide assetId or a combination of productKey and deviceKey to specify the device.

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](../api_faqs#how-to-get-organization-id-orgid-orgid)              |
| assetId  | Query          | False      | String        | Asset ID. [How to get assetId](../api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key identifier      |
| deviceKey | Query         | False     | String          | Device Key identifier          |



## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|------|---------------|---------------|--------|
| newDeviceKey | True | String | Device Key identifier of the new device. Supports English letters, numbers and special characters (-_.:). The length is limited within 4-64 characters. |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    DeviceReplaceResult structure        | Device replacement results. See [DeviceReplaceResult Structure](replace_device#devicereplaceResult-structure-devicereplaceresult)|


### DeviceReplaceResult Structure <DeviceReplaceResult>

| Name           | Data Type | Description      |
|---------------|-----------|--------------|
| assetId    | String        | Asset ID. |
| productKey   | String         | Product Key identifier      |
| deviceKey  | String          | Device Key identifier          |
| deviceSecret  | String          | New device key assigned by the system          |


## Error Codes

| Code           | Description|
|----------------|--------------|
|11704|New and old Device Keys are the same|
|11702|The new Device Key already exists in the database|



## Sample 1

### Request Sample

```
POST http://{apigw-address}/connect-service/v2.1/devices?action=replaceDevice&orgId=1c499110e8800000&assetId=FsTV44kr
{
    "newDeviceKey":"yourNewDeviceKey"
}
```

### Return Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"fa377585-8240-4d1e-ad9d-a8d820873142",
    "data":{
        "assetId":"FsTV44kr",
        "productKey":"O658R5li",
        "deviceKey":"yourNewDeviceKey",
        "deviceSecret":"QbgsPK6eFyue2BRlCr3r"
    }
}
```

## Java SDK Sample

```java
public class ReplaceDevice {
 
    public static void main(String[] args) {
 
        final String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
        final String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
        final String serverUrl = "http://{apigw-address}";
        final String orgId = "yourOrgId";
        final String assetId = "FsTV44kr";
 
        String newDeviceKey = "abcdefg123";
 
        ReplaceDeviceRequest request = new ReplaceDeviceRequest();
        request.setOrgId(orgId);
        request.setAssetId(assetId);
        request.setNewDeviceKey(newDeviceKey);
 
        ReplaceDeviceResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, ReplaceDeviceResponse.class);
 
        DeviceReplaceResult replaceResult = response.getData();
        String newDeviceSecret = replaceResult.getDeviceSecret();
        System.out.println(newDeviceSecret);
        System.out.println(response);
        System.out.println(response.getData()); 
    } 
}
```
