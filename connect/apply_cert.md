# Apply Certificate


Apply for a certificate and bind it to the specified device. You can also configure the validity period for a certificate you have previously obtained.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Prerequisites

- The device exists and is registered on EnOS.
- The product to which the device belongs to support bi-directional authentication.


## Request Format


```
POST https://{apigw-address}/connect-service/v2.0/certificates?action=apply
```


## Request Parameters (URI)

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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey``.
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey``.


## Request Parameters (Body)

.. list-table:: Request Parameters (Body)
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - csr
     - Mandatory
     - String
     - The CSR file (Certificate Signing Request) in the Privacy-Enhanced Mail (PEM) format. For how to generate CSR, see `Creating your Certificate Signing Request (CSR) File>> </docs/enos/zh_CN/dev/security/x509_ca/creating_csr.html>`_
   * - validDay
     - Optional
     - Integer
     - The validity period of the certificate in days. If not specified, the default value used would be "730". The rules that apply to this parameter are listed below.
   * - issueAuthority
     - Optional
     - String
     - The type of certificate to apply for. Only accepts two values: "RSA" (default) and "ECC". The rules that apply to this parameter are listed below.



### Rules for the Validity Period of a Certificate (validDay)

To use `validDay` in a request, the following rules apply:

- When the user does not specify ``validDay`` in the request, the default value would be used.
- When the user specifies ``validDay`` in the request:
 + If the specified value is no greater than the maximum validity period of the product that this device belongs to, the user-specified value is used.
 + If the specified value is greater than the maximum validity period of the product that this device belongs to, the request will fail and an error message will be returned.
 + If the default or specified value (not greater than the maximum validity period of the product) is greater than the remaining validity period of the certificate authority's root certificate (root CA), then the remaining validity period of the root CA would be used.

### Rules for issueAuthority


- If `issueAuthority` is not specified in a request, the default value, "RSA", would be used.
- The two certificate types applicable for `issueAuthority` are "RSA" and "ECC". If other values are given, an error would be returned. It is not case-sensitive.

### Certificate Type Description

- RSA: To apply for an RSA certificate, a Certificate Signing Request (.csr) file is required. The CSR file must use 2048-bit RSA public key. The signature algorithm must be "SHA256withRSA".
- ECC: To apply for an ECC certificate, a Certificate Signing Request (.csr) file is required. The CSR file must use 256-bit ECC public key. The public key algorithm is "prime256v1". The signature algorithm must be "SHA256withECDSA".




## Response Parameters

.. list-table:: Response Parameters (Body)
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - DeviceCertApplyResultInfo Struct
     - The certificate binding information. Refer to the table below for its structure.

### DeviceCertApplyResultInfo Struct

.. list-table:: deviceCertApplyResultInfo Struct
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - certChainURL
     - String
     - The CA root certificate URL.
   * - cert
     - String
     - The content of the certificate obtained.
   * - certSn
     - String
     - The certificate number.
   * - caCert
     - String
     - The CA root certificate.
   * - issueAuthority
     - String
     - The type of the certificate.

## Error Code

.. list-table:: Error codes
   :widths: auto
   :header-rows: 1

   * - Code
     - Type
     - Solution
   * - 99400
     - The specified validity period exceeds the maximum certificate validity period of the product to which this device belongs.
     - Change to a valid value for ``validDay``.
   * - 99400
     - invalid argument: The device identifier is invalid
     - Specify (``assetId``) or (``productKey`` + ``deviceKey``) in your request.
   * - 99400
     - Invalid Argument csr:csr is missing
     - Include a valid CSR file in your request.
   * - 99400
     - The product to which the device belongs to is not a product that supports bi-directional authorization.
     - Change the configuration of the product to support bi-directional authroization.
   * - 99400
     - Call ca error!: Certificate service err info:, code: (code), message: (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Invalid cert request!message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Duplicate subject by certificate request!message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Revoke cert is failed!message:  (message content), detail message: (detailed message content)
     - Refer to the "message" and "detailed message".
   * - 99400
     - Renew cert is failed!message:  (message content), detail message: (detailed message content)
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
   * - 11833
     - Certificate is already bound to another device.
     - Replace the CSR file.
   * - 99500
     - Internal error of certificate service.
     - Refer to your EnOS administrator.
   * - 99500
     - Internal error of product service.
     - Refer to your EnOS administrator
   * - 99500
     - Internal error of IoT Hub service.
     - Refer to your EnOS administrator

## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.0/certificates?assetId=yourDeviceAssetId&action=apply&orgId=yourOrgId
method: POST
requestBody: 
{
    "csr": "-----BEGIN NEW CERTIFICATE REQUEST-----\nMIICpzCCAY8CAQAwYjELMAkGA1UEBhMCQ04xETAPBgNVBAgTCFNoYW5naGFpMREw\nDwYDVQQHEwhTaGFuZ2hhaTENMAsGA1UEChMERW5PUzENMAsGA1UECxMERW5PUzEP\nMA0GA1UEAxMGMjVTWkFsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA\njWydoAdwoJcpvpNLr1zrsUHUXPCOLwl7jDZsBCWo8aEVv8tn4qI1VG4pqn5nqYzG\n40aoAFz1MBGxPIpjGHWbQfAaRgUlEf352ql6cpP/T1Qm6f8CjECY8vFbl4ABwOye\ncCjZJ7KIXHPF81OWOi2+JDsjDVOp747zuDpNwxkI3lIre3cj9zTa6/L+mAO34W/5\nGyHPTZ3wl7x2eFQMNXnccRoCzeXGOmk0+Cikdr5ERkZogLzW1h6JO2Gm6hAFhxjf\nuKVolAgdkjjiNoN4TTaHH4o+JNBzsV8UR4amtaFo0a+NXjZgwr2V9IMjtjkV6YIe\nHhFRLg5EpJmd4KEOUazwbwIDAQABoAAwDQYJKoZIhvcNAQELBQADggEBAIm5PAnG\ny0AIxDCB0cttTnxmOP8uquva4wnl3ZbX3cNWudzZXXHjCwYRXBhDWHJ1qM8yV1mN\nTJ1irW6Ebwq3kSqW4moJk161gKvspJuHlZhr+8eH0t/z1yLHD4sdf1XAqZ8CtIaG\nZpaOnYmp4bBu/SpfPi+S4VBU48KIc86yBtfQ1GpZiwBTpjiDTG1tyIJe2Vtd26WE\nc2LwBn9zRaFwQQ6AKCdzjGejXcWgXxRgHmxaN1zx3l4xKWR4ZAoON9Hx26RWG7zt\nQlQreoVD/FiERI81OijqrrX0LLAx4CpHVEGhrNykRAdWph47Z5vkNnfaIu2T9HWI\nsYYM5JVl66v3x7I=\n-----END NEW CERTIFICATE REQUEST-----\n",
    "validDay": 250,
    "issueAuthority": "RSA"
}
```

### Response Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "6f0c1c93-08f9-404c-a403-b49cbdab2938",
    "data": {
        "certChainURL": "https://{domain-name}/enos/CA/cacert",
        "caCert": "-----BEGIN CERTIFICATE-----\nMIID7DCCAtSgAwIBAgIJAK3CuSWAQ/PIMA0GCSqGSIb3DQEBCwUAMIGCMQswCQYD\nVQQGEwJDTjERMA8GA1UECAwIU2hhbmdoYWkxETAPBgNVBAcMCFNoYW5naGFpMQ0w\nCwYDVQQKDARFbk9TMRAwDgYDVQQLDAdFbk9TIENBMRAwDgYDVQQDDAdFbk9TIENB\nMRowGAYJKoZIhvcNAQkBFgtjYUBlbmlvdC5pbzAeFw0xOTAyMjYwOTExMzlaFw0y\nOTAyMjMwOTExMzlaMIGCMQswCQYDVQQGEwJDTjERMA8GA1UECAwIU2hhbmdoYWkx\nETAPBgNVBAcMCFNoYW5naGFpMQ0wCwYDVQQKDARFbk9TMRAwDgYDVQQLDAdFbk9T\nIENBMRAwDgYDVQQDDAdFbk9TIENBMRowGAYJKoZIhvcNAQkBFgtjYUBlbmlvdC5p\nbzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAMU32ZYkLVcUzdvlASek\npL7oiwK4dCsmNmIIL0JHyfjPoIk34ud0eB3YR/6wv4n4eXkLp51ZOMcfTC/TXGW2\noz3gwhv/hIVg2vtu3sIYiKoL87UtMk1B6nlWdiuNeklGWEzY7nrdUEBjZn0l93Oy\nSmkXT/zPbK0ix5qLAcSuV23zADNihdh7oiUIEk8M4qz1QZWKaU+l7WPEcGZiDkRh\nZ8SWZ3Z4TQZoazDV1EGXTiw0v722O/TsnviTWilFhGsUclW91VzicZQf6NStp6Wc\nJtsGviiN+HPI+gpX2TVl/1lQmom9YPBhwdVzqGPs4NqhTClVkXUSxKSoA4ab42P/\nUBUCAwEAAaNjMGEwHQYDVR0OBBYEFINjzI33ermRFRvh5oVmH1TbgYcaMB8GA1Ud\nIwQYMBaAFINjzI33ermRFRvh5oVmH1TbgYcaMA8GA1UdEwEB/wQFMAMBAf8wDgYD\nVR0PAQH/BAQDAgEGMA0GCSqGSIb3DQEBCwUAA4IBAQACseTlfMbEA0PVbwxTSuNp\npaJ5XBFGqxFkuK5MYYBAVFmqlfSluH39BPJQFCnSNZi16T6vEXuvqqTZOIylE3z1\nVARUg3sHKLIx7sKKA4rFjTb49h48BlQGHHuyapdSJwRHuIqrWuGwgHz7Bi7NZ6EO\ngw+xkfMlEC846mlsRfqxxkFiI69hIkpu5rdO7Ya8uaXJSyAi1J3/gLSidWyyUMFM\nAq1eeWRDY/IrEcb0nRjgObuqE5DVq/1ylpkL+5DAaSiG9vYSpyIacnKxkPlg6ezJ\nqXJM+s3XWxm8/mlqspb5ewHxj6dVw/DOhFky+3l7zHERdWPkHHysEp/IcHB6Vj6y\n-----END CERTIFICATE-----",
        "cert": "-----BEGIN CERTIFICATE-----\nMIIEtTCCA52gAwIBAgICf9AwDQYJKoZIhvcNAQELBQAwgYIxCzAJBgNVBAYTAkNO\nMREwDwYDVQQIDAhTaGFuZ2hhaTERMA8GA1UEBwwIU2hhbmdoYWkxDTALBgNVBAoM\nBEVuT1MxEDAOBgNVBAsMB0VuT1MgQ0ExEDAOBgNVBAMMB0VuT1MgQ0ExGjAYBgkq\nhkiG9w0BCQEWC2NhQGVuaW90LmlvMB4XDTIwMDEwNjEwNDYzM1oXDTIwMDkxMjEw\nNDYzM1owYjELMAkGA1UEBhMCQ04xETAPBgNVBAgTCFNoYW5naGFpMREwDwYDVQQH\nEwhTaGFuZ2hhaTENMAsGA1UEChMERW5PUzENMAsGA1UECxMERW5PUzEPMA0GA1UE\nAxMGMjVTWkFsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAjWydoAdw\noJcpvpNLr1zrsUHUXPCOLwl7jDZsBCWo8aEVv8tn4qI1VG4pqn5nqYzG40aoAFz1\nMBGxPIpjGHWbQfAaRgUlEf352ql6cpP/T1Qm6f8CjECY8vFbl4ABwOyecCjZJ7KI\nXHPF81OWOi2+JDsjDVOp747zuDpNwxkI3lIre3cj9zTa6/L+mAO34W/5GyHPTZ3w\nl7x2eFQMNXnccRoCzeXGOmk0+Cikdr5ERkZogLzW1h6JO2Gm6hAFhxjfuKVolAgd\nkjjiNoN4TTaHH4o+JNBzsV8UR4amtaFo0a+NXjZgwr2V9IMjtjkV6YIeHhFRLg5E\npJmd4KEOUazwbwIDAQABo4IBUjCCAU4wCQYDVR0TBAIwADAnBglghkgBhvhCAQ0E\nGkVub3MgR2VuZXJhdGVkIENlcnRpZmljYXRlMB0GA1UdDgQWBBRGmiiFkKBySldM\nc8qtiBeXWLtYTDCBtwYDVR0jBIGvMIGsgBSDY8yN93q5kRUb4eaFZh9U24GHGqGB\niKSBhTCBgjELMAkGA1UEBhMCQ04xETAPBgNVBAgMCFNoYW5naGFpMREwDwYDVQQH\nDAhTaGFuZ2hhaTENMAsGA1UECgwERW5PUzEQMA4GA1UECwwHRW5PUyBDQTEQMA4G\nA1UEAwwHRW5PUyBDQTEaMBgGCSqGSIb3DQEJARYLY2FAZW5pb3QuaW+CCQCtwrkl\ngEPzyDA/BglghkgBhvhCAQQEMmh0dHBzOi8vYWxwaGEtcG9ydGFsLWNuNC5lbmlv\ndC5pbzo4MDgxL2Vub3MvQ0EvY3JsMA0GCSqGSIb3DQEBCwUAA4IBAQAeunPZdxzS\nksI1iEr5eG6BVF96dahGtKdNwd8bZqkF0hfZ2OTaXX019lQHpE/KU0wRBSpNXMfq\nwtUlmK4dAzUVhWdW48gNv3jSrdxj2iwK27j7DyMpNup+mKI2AR9AMjhPzVnHXt9M\nNEK7BxTqsPs+I6gFSLr9fUV7kozROm5jEVvvLrEvX68LKvyXAqkYTtPHZlR4oj/v\nDgZwXfE9rFEi9OFYYl0Xm4lSH3HhTh9vxgq08mGtyoUiGi8h6Uy79Slwk40oblE5\n1sV1o+31MDpzQTca1aAsL/g3XL6aLUFziMHzkn5peHuf+njN0tNupNn2CLK1cl2n\nBr9WJ55OFglM\n-----END CERTIFICATE-----\n",
        "certSN": "32720",
        "issueAuthority": "RSA"
    }
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.cert;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.cert.ApplyCertificateRequest;
import com.envisioniot.enos.connect_service.v2_1.cert.ApplyCertificateResponse;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;


public class applyCert {

    public static void main(String[] args) {

        String appKey = "yourAppAccessKey";
        String appSecret = "yourAppSecretKey";
        String serverUrl = "https://{apigw-address}";

        String orgId = "yourOrgId";

        ApplyCertificateRequest applyCertificateRequest = new ApplyCertificateRequest();
        String csr = "-----BEGIN NEW CERTIFICATE REQUEST-----\n" +
                "MIICwTCCAakCAQAwfDELMAkGA1UEBhMCQ04xETAPBgNVBAgMCFNoYW5naGFpMREw\n" +
                "DwYDVQQHDAhTaGFuZ2hhaTENMAsGA1UECgwERW5PUzERMA8GA1UEAwwITVJtSXl6\n" +
                "UFcxDTALBgNVBAsMBEVuT1MxFjAUBgkqhkiG9w0BCQEWBzREbmIxVDEwggEiMA0G\n" +
                "CSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCCRmPrs0ubuH2HeGT9kwB72/SuKWf3\n" +
                "WtWQ5csRWlSOullOQn2OUqdVPOcnZm2hQQ7WGDH3cvyD49CIeVF/a8jqzqbkrk/5\n" +
                "jINuu71tjMzRRZWym8KOmYbA2nO8Wdko8mebuYtcSpic7fByGRhGytsE2EU+TD0a\n" +
                "K1tSjMCME0ba9/ImU+q5ziI0YPRI2Pz2Sw08rpTxICocw/oGEqNbK0cYHMbQjEmQ\n" +
                "spa5MARGz3coGlRu8CsyGXwkUC6zJVxJxbNA7/VTc2PCRhS2SfjBOT226cSharH8\n" +
                "4VGywXN+YLaMUDFui2gb2E5tHFIzWD0X1qCWtDsbPIZhlPt7agsmPkLrAgMBAAGg\n" +
                "ADANBgkqhkiG9w0BAQsFAAOCAQEAVMv03+jwh/6H4+x+sQiu4qxQeBuNWagqVL/C\n" +
                "HEoyWkWOzeJHpMI59OLukHQ4QJi1IwBSB0TdWn1kfpb0ztNaYfKCR5mQLErNw9ee\n" +
                "01mEeG+3Lgmd4FRWvnNdL42kQ4GeDIkmpI/aEabMHjLwcFofzeZHRsaRyeetG5Bv\n" +
                "oGTOK1hFP4lS1p40aueHa3WNEw7z/QG2lNMz5+HPbEqJhe5AoQicMMFciZ+y1LZV\n" +
                "ZU72eVecirZPMsYOjjQ9+TLztfSLEPCZ60xA0QkTn4CFgoX8DvuzxP2uJeZ70Mch\n" +
                "Z58IqTZQkAWrTx7t4w3+rGBwQ/pkFXANd2NtYr9Mt50wIoMXzw==\n" +
                "-----END NEW CERTIFICATE REQUEST-----\n";
        applyCertificateRequest.setCsr(csr);
         /*
         * Use one of the following methods to identify a device：
         * ASSET_ID
         * PRODUCT_KEY + DEVICE_KEY
         */
        applyCertificateRequest.setAssetId(yourAssetId);
        applyCertificateRequest.setProductKey(yourProductKey);
        applyCertificateRequest.setDeviceKey(yourDeviceKey);
        applyCertificateRequest.setDevice(device);
        applyCertificateRequest.setValidDay(250);
        applyCertificateRequest.setOrgId(orgId);
        ApplyCertificateResponse certRsp = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(applyCertificateRequest, ApplyCertificateResponse.class);
        System.out.println(certRsp.getData());
    }
}
```





<!--End-->
