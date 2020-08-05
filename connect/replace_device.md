# Replace Device

Replace the ``deviceKey`` of a device without changing its ``assetId``. The system will override the original ``deviceKey`` and ``deviceSecret`` of the registered device, re-assign a ``deviceKey``, generate a new ``deviceSecret``, and reset the device to non-activated status. The new device can be connected to EnOS<sup>TM</sup> with the replaced ``deviceKey``, and the data of the old and new devices can be linked through the ``assetID``.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.1/devices?action=replaceDevice
```

## Request Parameters (URI)


.. note:: Use one of the following methods to specify the device to be replaced:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> <../api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetId>> <../api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key.  To be used with ``deviceKey`` .
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey`` .



## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - newDeviceKey
     - Mandatory
     - String
     - The new device key of the device. Supports English letters, at most 3 special characters, numbers, hyphens (-), underline (_), dot (.), and colon (:). The length is limited to within 4-64 characters.



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - DeviceReplaceResult Struct
     - The returned results of the device replacement. For details, see `DeviceReplaceResult Struct>> <replace_device#devicereplaceResult-struct-devicereplaceresult>`_




### DeviceReplaceResult Struct <devicereplaceresult>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - assetId
     - String
     - The asset ID.
   * - productKey
     - String
     - The product Key.
   * - deviceKey
     - String
     - The device Key.
   * - deviceSecret 
     - String
     - The new device secret assigned by the system.




## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code 
     - Description
   * - 11704 
     - The new and old device keys are the same.
   * - 11702
     - The new device key already exists in the database.




## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/devices?action=replaceDevice
method: POST
requestBody:
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
        "assetId":"yourAssetId",
        "productKey":"yourProductKey",
        "deviceKey":"yourNewDeviceKey",
        "deviceSecret":"yourDeviceSecret"
    }
}
```

## Java SDK Sample

```java
public class ReplaceDevice {
 
    public static void main(String[] args) {
 
        final String appKey = "yourAppAccessKe";
        final String appSecret = "yourAppSecretKey";
        final String serverUrl = "http://{apigw-address}";
        final String orgId = "yourOrgId";
        final String assetId = "yourAssetId";
 
        String newDeviceKey = "yourNewDeviceKey";
 
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
