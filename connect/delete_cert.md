# Revoke Certificate


Revoke the certificate bound to a device.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

### Prerequisites

- The device exists and is registered on EnOS.
- The certificate is bound to the device.
- The certificate is within its validity period.



## Request Format


```json
POST https://{apigw-address}/connect-service/v2.0/certificates?action=revoke
```


## Request Parameters (URI)


.. note:: Use one of the following methods to specify the device:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request

.. csv-table:: Request Parameters（URI）
   :header: "Name", "Location (Path/Query)", "Mandatory/Optional", "Data Type", "Description"
   :widths: auto

   "orgId", "Query", "Mandatory", "String", "The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_"
   "assetId", "Query", "Optional (See **Note** above)", "String", "The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`_"
   "productKey", "Query", "Optional (See **Note** above)", "String", "The product key. To be used with ``deviceKey``."
   "deviceKey", "Query", "Optional (See **Note** above)", "String", "The device key. To be used with ``productKey``."
   "certSn", "Query", "Mandatory", "Integer", "The number of the certificate to be revoked."
   "reason", "Query", "Optional", "RevokeReason", " ``RevokeReason`` is an enum whose default value is ``0 UNSPECIFIED`` . The enum values are as follows:
   - 0 UNSPECIFIED：The reason why the certificate is revoked is unknown.
   - 1 KEY_COMPROMISE：The private key of the certificate owner has been compromised.
   - 3 AFFILIATION_CHANGED：The certificate owner's name or information has been changed.
   - 4 SUPERSEDED：The certificate has been replaced.
   - 5 CESSATION_OF_OPERATION：The certificate is no longer needed.
   - 6 CERTIFICATE_HOLD：The certificate has been suspended.
   - 9 PRIVILEGE_WITHDRAWN：The certificate issuing entity's privilege has been withdrawn. The CA becomes invalid or the certificate is unreliable."


## Request Parameter (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - certSn
     - Mandatory
     - Integer
     - The number of the certificate to be revoked.
   * - reason
     - Optional
     - Integer
     - ``RevokeReason`` is an integer whose default value is ``0 UNSPECIFIED`` . The other possible values are as follows:

       + 0 UNSPECIFIED：The reason why the certificate is revoked is unknown.
       + 1 KEY_COMPROMISE：The private key of the certificate owner has been compromised.
       + 3 AFFILIATION_CHANGED：The certificate owner's name or information has been changed.
       + 4 SUPERSEDED：The certificate has been replaced.
       + 5 CESSATION_OF_OPERATION：The certificate is no longer needed.
       + 6 CERTIFICATE_HOLD：The certificate has been suspended.
       + 9 PRIVILEGE_WITHDRAWN：The certificate issuing entity's privilege has been withdrawn. The CA becomes invalid or the certificate is unreliable.


## Error Code

.. list-table:: Error codes
   :widths: auto
   :header-rows: 1

   * - Code
     - Type
     - Solution
   * - 99400
     - invalid argument: The device identifier is invalid
     - Specify (``assetId``) or (``productKey`` + ``deviceKey``) in your request.
   * - 99400
     - Invalid Argument certSn:certSn is missing
     - Include a valid ``certSn`` in your request.
   * - 99400
     - Call ca error!: Certificate service err info:, code: (code), message: (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Invalid cert request!message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Query cert is failed!message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - When calling Certificate Services, the call parameters are invalid.message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - The serial number of the certificate to be updated is required.
     - Include ``certSn`` in your request.
   * - 99400
     - The serial number of the new certificate is invalid (less than 0).
     - Ensure ``certSn`` is valid.
   * - 99400
     - The certificate list bound to the device does not have the certificate, or the certificate is bound to other devices.
     - Ensure the certificate specified in the request is valid.
   * - 11404
     - Device cannot be found
     - Ensure that the device exists and is registerd on EnOS.
   * - 99500
     - Internal error of certificate service.
     - Refer to your EnOS administrator.
   * - 99500
     - Internal error of product service.
     - Refer to your EnOS administrator.
   * - 99500
     - Internal error of IoT Hub service.
     - Refer to your EnOS administrator.





## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.0/certificates?action=revoke&assetId=yourDeviceAssetId&orgId=yourOrgId
method: POST
requestBody:
{
    "reason":0,
    "certSn":52739
}
```

### Response Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"e3391ff8-19ba-4809-b944-c1b29f468af9",
    "data":null
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.cert;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.cert.RevokeCertificateRequest;
import com.envisioniot.enos.connect_service.v2_1.cert.RevokeCertificatesResponse;
import com.envisioniot.enos.connect_service.v2_1.cert.RevokeReason;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;

public class RevorkCert {
    public static void main(String[] args) {
        String appKey = "yourAppAccessKey";
        String appSecret = "yourAppSecretKey";
        String serverUrl = "https://{apigw-address}";

        String orgId = "yourOrgId";
        Integer certSn = 2661;
        RevokeCertificateRequest request = new RevokeCertificateRequest();
        /*
         * Use one of the following methods to identify a device：
         * ASSET_ID
         * PRODUCT_KEY + DEVICE_KEY
         */
        request.setAssetId(yourAssetId);
        request.setProductKey(yourProductKey);
        request.setDeviceKey(yourDeviceKey);
        request.setDevice(identifier);
        request.setCertSn(certSn);
        request.setOrgId(orgId);
        request.setReason(RevokeReason.UNSPECIFIED);
        RevokeCertificatesResponse certRsp = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, RevokeCertificatesResponse.class);
        if (certRsp.success()) {
            System.out.println("Certificate revoked.");
        }
    }
}
```
<!--End-->





