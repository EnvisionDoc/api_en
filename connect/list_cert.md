# List Certificate

List the certificates bound to the specified device.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Read


## Request Format


```json
GET https://{apigw-address}/connect-service/v2.0/certificates?action=list
```


.. note:: Use one of the following methods to specify the device:

## Request Parameters (URI)


.. note:: Use one of the following methods to specify the device:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request

.. list-table:: Request Parameters (URI)
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
     - The organization ID which the asset belongs to. `How to get Organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey`` .
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey`` .


## Response Parameters

.. list-table:: Response Parameters
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of DeviceCertDetailInfo Structs
     - A list of the certificates returned. For details of a DeviceCertDetailInfo Struct, see the table below.

### DeviceCertDetailInfo Struct

.. csv-table:: DeviceCertDetailInfo Object
   :header: "Name", "Data Type", "Description"
   :widths: auto

   "certSN", "String", "The certificate number"
   "cert", "String", "The certificate content."
   "certStatus", "Integer", "Certificate Status:
   - 0: Valid
   - 1: Revoked
   - 2: Expired"
   "issuer", "String", "The information of the certificate authority."
   "subject", "String", "The request requestor information."
   "signDate", "Long", "The timestamp when the certificate was issued."
   "effetiveDate", "Long", "The validity period in days."
   "expireDate", "Long", "The timestamp when the certificate expired."
   "revoker", "String", "The entity that revokes the certificate. Required only if ``certStatus`` is ``1``. "
   "revokerReason", "String", "The reason why the certificate is revoked. Required only if ``certStatus`` is ``1`` ."

## Samples

### Request Sample

```
url: https://{apigw-address}/connect-service/v2.0/certificates?action=list&assetId=yourAssetId&orgId=youOrgId
method: GET
```

### Response Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "318d8b1f-1f27-4dd4-8299-b75a2015d425",
    "data": [
        {
            "certSN": "52725",
            "cert": "52725",
            "certStatus": 1,
            "issuer": "EMAILADDRESS=ca@gmail.com, CN=EnOS CA, OU=EnOS CA, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "subject": "EMAILADDRESS=xT7EaR, OU=EnOS, CN=xMen1, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "signDate": 1581216505000,
            "effetiveDate": 1581216505000,
            "expireDate": 1582080505000,
            "audit": {
                "createBy": "youOrgId",
                "createTime": 1581217021695,
                "updateBy": "youOrgId",
                "updateTime": 1581217021695,
                "ns": "youOrgId",
                "deleted": false
            },
            "revoker": "IoT_Hub",
            "revokerReason": "KEY COMPROMISE",
            "isEnosCert": true,
            "issueAuthority": "RSA"
        },
        {
            "certSN": "52726",
            "cert": "52726",
            "certStatus": 0,
            "issuer": "EMAILADDRESS=ca@gmail.com, CN=EnOS ECC CA, OU=Envision Digital, O=Envision, L=Shanghai, ST=Shanghai, C=CN",
            "subject": "EMAILADDRESS=uKGdK, OU=EnOS, CN=yPI9z8z, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "signDate": 1581218161000,
            "effetiveDate": 1581218161000,
            "expireDate": 1582082161000,
            "audit": {
                "createBy": "youOrgId",
                "createTime": 1581218161773,
                "updateBy": "youOrgId",
                "updateTime": 1581218161773,
                "ns": "youOrgId",
                "deleted": false
            },
            "revoker": "",
            "revokerReason": "",
            "isEnosCert": true,
            "issueAuthority": "ECC"
        },
        {
            "certSN": "52727",
            "cert": "52727",
            "certStatus": 2,
            "issuer": "EMAILADDRESS=ca@gmail.com, CN=EnOS ECC CA, OU=Envision Digital, O=Envision, L=Shanghai, ST=Shanghai, C=CN",
            "subject": "EMAILADDRESS=xT7EaR, OU=EnOS, CN=xMen1, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "signDate": 1581234648000,
            "effetiveDate": 1581234648000,
            "expireDate": 1581493848000,
            "audit": {
                "createBy": "youOrgId",
                "createTime": 1581234640405,
                "updateBy": "youOrgId",
                "updateTime": 1581234640405,
                "ns": "youOrgId",
                "deleted": false
            },
            "revoker": "",
            "revokerReason": "",
            "isEnosCert": true,
            "issueAuthority": "ECC"
        }
    ]
}
```

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
     - Call ca error!: Certificate service err info:, code: (code), message: (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Query cert is failed!message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - When calling Certificate Services, the call parameters are invalid.message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
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
     - Internal error of IoT hub service.
     - Refer to your EnOS administrator.

## Samples

### Request Sample

```json
GET https://{apigw-address}/connect-service/v2.0/certificates?action=list&assetId=youAssetId&orgId=youOrgId
```

### Response Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "318d8b1f-1f27-4dd4-8299-b75a2015d425",
    "data": [
        {
            "certSN": "52725",
            "cert": "52725",
            "certStatus": 1,
            "issuer": "EMAILADDRESS=ca@eniot.io, CN=EnOS CA, OU=EnOS CA, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "subject": "EMAILADDRESS=xT7EaR, OU=EnOS, CN=xMen1, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "signDate": 1581216505000,
            "effetiveDate": 1581216505000,
            "expireDate": 1582080505000,
            "audit": {
                "createBy": "youOrgId",
                "createTime": 1581217021695,
                "updateBy": "youOrgId",
                "updateTime": 1581217021695,
                "ns": "youOrgId",
                "deleted": false
            },
            "revoker": "IoT_Hub",
            "revokerReason": "KEY COMPROMISE",
            "isEnosCert": true,
            "issueAuthority": "RSA"
        },
        {
            "certSN": "52726",
            "cert": "52726",
            "certStatus": 0,
            "issuer": "EMAILADDRESS=ca@eniot.io, CN=EnOS ECC CA, OU=Envision Digital, O=Envision, L=Shanghai, ST=Shanghai, C=CN",
            "subject": "EMAILADDRESS=uKGdK, OU=EnOS, CN=yPI9z8z, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "signDate": 1581218161000,
            "effetiveDate": 1581218161000,
            "expireDate": 1582082161000,
            "revoker": "",
            "revokerReason": "",
            "isEnosCert": true,
            "issueAuthority": "ECC"
        },
        {
            "certSN": "52727",
            "cert": "52727",
            "certStatus": 2,
            "issuer": "EMAILADDRESS=ca@eniot.io, CN=EnOS ECC CA, OU=Envision Digital, O=Envision, L=Shanghai, ST=Shanghai, C=CN",
            "subject": "EMAILADDRESS=xT7EaR, OU=EnOS, CN=xMen1, O=EnOS, L=Shanghai, ST=Shanghai, C=CN",
            "signDate": 1581234648000,
            "effetiveDate": 1581234648000,
            "expireDate": 1581493848000,
            "revoker": "",
            "revokerReason": "",
            "isEnosCert": true,
            "issueAuthority": "ECC"
        }
    ]
}
```



### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.cert;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.cert.ListCertificatesRequest;
import com.envisioniot.enos.connect_service.v2_1.cert.ListCertificatesResponse;
import com.envisioniot.enos.connect_service.vo.CertificateInfo;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;

import java.util.List;

public class ListCert {

    public static void main(String[] args) {
        ListCertificatesRequest listCertificatesRequest = new ListCertificatesRequest();
        String appKey = "AccessKey of your APP";
        String appSecret = "SecretKey of your APP";
        String serverUrl = "https://{apigw-address}";

        String orgId = "yourOrgId";
        /*
         * Use one of the following methods to identify a device:
         * ASSET_ID
         * PRODUCT_KEY + DEVICE_KEY
         */
        listCertificateRequest.setAssetId(yourAssetId);
        listCertificateRequest.setProductKey(yourProductKey);
        listCertificateRequest.setDeviceKey(yourDeviceKey);
        listCertificatesRequest.setDevice(device);
        listCertificatesRequest.setOrgId(orgId);
        ListCertificatesResponse certRsp = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(listCertificatesRequest, ListCertificatesResponse.class);
        List<CertificateInfo> certificateInfos = certRsp.getData();
        if (certificateInfos != null) {
            for (CertificateInfo certificateInfo : certificateInfos) {
                System.out.println(certificateInfo);
            }
        }
    }
}
```




<!--需要示例展示Error info是怎么显示的-->
<!--End-->
