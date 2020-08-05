# Renew Certificate

Update a certificate and bind the updated certificate to the specified device.

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
- The product to which the device belongs to supports bi-directional authentication.
- The certificate to be updated is bound to the device.
- The certificate to be updated is valid.

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.0/certificates?action=renew
```


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
     - Optional
     - String
     - The CSR file (Certificate Signing Request) in the Privacy-Enhanced Mail (PEM) format. If this parameter is not included in the request, a certificate will be generated based on the request data of the existing certificate. For details on how to generate a CSR file, see `Creating your Certificate Signing Request (CSR) File>> </docs/enos/en/2.1.0/security/x509_ca/creating_csr.html>`_
   * - certSn
     - Mandatory
     - Integer
     - The certificate number to be updated.
   * - validDay
     - Optional
     - Integer
     - The validity period of the certificate in days. If not specified, the default value used would be "730". The rules that apply to this parameter are listed below.
   * - issueAuthority
     - Optional
     - String
     - The type of certificate to apply for. Only accepts two values: "RSA" (default) and "ECC". The rules that apply to this parameter are listed below.

### Rules for the Validity Period of a Certificate (validDay)

### Rules for the Validity Period of a Certificate (validDay)

To use ``validDay`` in a request, the following rules apply:

- When the user does not specify ``validDay`` in the request, the default value, "730", would be used.
- When the user specifies ``validDay`` in the request:
 + If the specified value is no greater than the maximum validity period of the product that this device belongs to, the user-specified value is used.
 + If the specified value is greater than the maximum validity period of the product that this device belongs to, the request will fail and an error message will be returned.
 + If the default or specified value (not greater than the maximum validity period of the product) is greater than the remaining validity period of the certificate authority's root certificate (root CA), then the remaining validity period of the root CA would be used.


### Rules for issueAuthority


- If ``issueAuthority`` is not specified in a request, the default value, "RSA", would be used.
- The two certificate types applicable for ``issueAuthority`` are "RSA" and "ECC". If other values are given, an error would be returned.
- It is not case-sensitive.

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
     - DeviceCertRenewResultInfo Struct
     - The Certificate binding information. Refer to the table below for its structure.

### DeviceCertRenewResultInfo Struct

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
     - The certificate type.


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
     - Invalid Argument certSn:certSn is missing
     - Include a valid ``certSn`` in your request.
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
     - Renew cert is failed!message:  (message content), detail message: (detailed message content)
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
     - The original certificate has been revoked and cannot be updated.
     - Apply for a new certifcate instead of updating the original.
   * - 99400
     - The original certificate has expired and cannot be updated.
     - Apply for a new certifcate instead of updating the original.
   * - 99400
     - The certificate list bound to the device does not have the certificate, or the certificate is bound to other devices.
     - Ensure the certificate specified in the request is valid.
   * - 11404
     - Device cannot be found
     - Ensure the device exists and is registerd on EnOS.
   * - 11833
     - Certificate is already bound to another device.
     - Replace the CSR file.
   * - 99500
     - Internal error of certificate service.
     - Refer to your EnOS administrator.
   * -  99500
     - Internal error of product service.
     - Refer to your EnOS administrator.
   * -  99500
     - Internal error of IoT Hub service.
     - Refer to your EnOS administrator.


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.0/certificates?assetId=yourDeviceAssetId&action=renew&orgId=yourOrgId
method: POST
requestBody:
{
    "csr":"-----BEGIN NEW CERTIFICATE REQUEST-----\nMIICxDCCAawCAQAwfzELMAkGA1UEBhMCQ04xETAPBgNVBAgMCFNoYW5naGFpMREw\nDwYDVQQHDAhTaGFuZ2hhaTENMAsGA1UECgwERW5PUzERMA8GA1UEAwwITnNQTU1F\ncHExDTALBgNVBAsMBEVuT1MxGTAXBgkqhkiG9w0BCQEWCjB5eGtWY2pwZXIwggEi\nMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDIiuFINos2TgLO6G+yQdKs3hc+\n+Cuael/AB8bP2IlunlDdyrllpWT4ROimDDEUfV/qXzlHYvxBwaL7GKPFPKeoercn\ntS6ttGBkeZXMJwbXdfpXsusubmy8qOZqBofikjZ+CaAuUd6fvEA3aqLHDaHrhtYi\nfoQOBRsuzr16JW79AMjwPdbXA4UtcLlloDEtccJInwlT3F/Ck7CEQ4n8TcNrpfkT\nsVfLaYt1AkdokKD1cKVDp5kYoHr4bUJK+y1vII+hyRnkmazs5AsiMzc5+nllWyq0\nnwptoyqzy7ynu6k/4myUMZBPd4qrbbNuJjvx/wWf0q9RaY9ri8Rdii9q76zlAgMB\nAAGgADANBgkqhkiG9w0BAQsFAAOCAQEAUJeY3lGdFNLd+KifKUjlYqQKRaknsDhg\no2wyxrofzkTSVPR/gxR+lTPaZJdaHoSTylXUPZ2P/NDtclYnw2XVcg8eCZH0B0BA\nZ9V/t8Z8LXxZx++Cm3B6kvt8FtOZpBnqxkKlht28Sh14tKPdLDE684aFrnQjYgS1\nfJdn0W9tEr27GbUf+xmsY5hnPwh7VxcJ1k46eCLZd0Jj2+DdOhqb3nW1Q9I22Fsr\n9z0ccXmY573svl49nd8jAExsin/qJpd3ATZj2PXQ2HJPi38hT/KRYxjmXjQjTF+K\ngw+KmU7UWOpeSZYiHMGN+8krfjT4mbPcCPWePRMSVJjXsXwj7YbLYQ==\n-----END NEW CERTIFICATE REQUEST-----\n",
    "validDay":220,
    "certSn":52770,
    "issueAuthority":"RSA"
}
```

### Response Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "3eaf8fb2-9305-4db9-8044-b5632044abf8",
    "data": {
        "certChainURL": "https://{domain-name}/enos/CA/cacert/RSA",
        "caCert": "-----BEGIN CERTIFICATE-----\nMIID7DCCAtSgAwIBAgIJAK3CuSWAQ/PIMA0GCSqGSIb3DQEBCwUAMIGCMQswCQYD\nVQQGEwJDTjERMA8GA1UECAwIU2hhbmdoYWkxETAPBgNVBAcMCFNoYW5naGFpMQ0w\nCwYDVQQKDARFbk9TMRAwDgYDVQQLDAdFbk9TIENBMRAwDgYDVQQDDAdFbk9TIENB\nMRowGAYJKoZIhvcNAQkBFgtjYUBlbmlvdC5pbzAeFw0xOTAyMjYwOTExMzlaFw0y\nOTAyMjMwOTExMzlaMIGCMQswCQYDVQQGEwJDTjERMA8GA1UECAwIU2hhbmdoYWkx\nETAPBgNVBAcMCFNoYW5naGFpMQ0wCwYDVQQKDARFbk9TMRAwDgYDVQQLDAdFbk9T\nIENBMRAwDgYDVQQDDAdFbk9TIENBMRowGAYJKoZIhvcNAQkBFgtjYUBlbmlvdC5p\nbzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAMU32ZYkLVcUzdvlASek\npL7oiwK4dCsmNmIIL0JHyfjPoIk34ud0eB3YR/6wv4n4eXkLp51ZOMcfTC/TXGW2\noz3gwhv/hIVg2vtu3sIYiKoL87UtMk1B6nlWdiuNeklGWEzY7nrdUEBjZn0l93Oy\nSmkXT/zPbK0ix5qLAcSuV23zADNihdh7oiUIEk8M4qz1QZWKaU+l7WPEcGZiDkRh\nZ8SWZ3Z4TQZoazDV1EGXTiw0v722O/TsnviTWilFhGsUclW91VzicZQf6NStp6Wc\nJtsGviiN+HPI+gpX2TVl/1lQmom9YPBhwdVzqGPs4NqhTClVkXUSxKSoA4ab42P/\nUBUCAwEAAaNjMGEwHQYDVR0OBBYEFINjzI33ermRFRvh5oVmH1TbgYcaMB8GA1Ud\nIwQYMBaAFINjzI33ermRFRvh5oVmH1TbgYcaMA8GA1UdEwEB/wQFMAMBAf8wDgYD\nVR0PAQH/BAQDAgEGMA0GCSqGSIb3DQEBCwUAA4IBAQACseTlfMbEA0PVbwxTSuNp\npaJ5XBFGqxFkuK5MYYBAVFmqlfSluH39BPJQFCnSNZi16T6vEXuvqqTZOIylE3z1\nVARUg3sHKLIx7sKKA4rFjTb49h48BlQGHHuyapdSJwRHuIqrWuGwgHz7Bi7NZ6EO\ngw+xkfMlEC846mlsRfqxxkFiI69hIkpu5rdO7Ya8uaXJSyAi1J3/gLSidWyyUMFM\nAq1eeWRDY/IrEcb0nRjgObuqE5DVq/1ylpkL+5DAaSiG9vYSpyIacnKxkPlg6ezJ\nqXJM+s3XWxm8/mlqspb5ewHxj6dVw/DOhFky+3l7zHERdWPkHHysEp/IcHB6Vj6y\n-----END CERTIFICATE-----",
        "cert": "-----BEGIN CERTIFICATE-----\nMIIEPDCCAySgAwIBAgIDAM4jMA0GCSqGSIb3DQEBCwUAMIGCMQswCQYDVQQGEwJD\nTjERMA8GA1UECAwIU2hhbmdoYWkxETAPBgNVBAcMCFNoYW5naGFpMQ0wCwYDVQQK\nDARFbk9TMRAwDgYDVQQLDAdFbk9TIENBMRAwDgYDVQQDDAdFbk9TIENBMRowGAYJ\nKoZIhvcNAQkBFgtjYUBlbmlvdC5pbzAeFw0yMDA0MjEwNzA0MDVaFw0yMDExMjcw\nNzA0MDVaMH8xCzAJBgNVBAYTAkNOMREwDwYDVQQIDAhTaGFuZ2hhaTERMA8GA1UE\nBwwIU2hhbmdoYWkxDTALBgNVBAoMBEVuT1MxETAPBgNVBAMMCE5zUE1NRXBxMQ0w\nCwYDVQQLDARFbk9TMRkwFwYJKoZIhvcNAQkBFgoweXhrVmNqcGVyMIIBIjANBgkq\nhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyIrhSDaLNk4CzuhvskHSrN4XPvgrmnpf\nwAfGz9iJbp5Q3cq5ZaVk+ETopgwxFH1f6l85R2L8QcGi+xijxTynqHq3J7UurbRg\nZHmVzCcG13X6V7LrLm5svKjmagaH4pI2fgmgLlHen7xAN2qixw2h64bWIn6EDgUb\nLs69eiVu/QDI8D3W1wOFLXC5ZaAxLXHCSJ8JU9xfwpOwhEOJ/E3Da6X5E7FXy2mL\ndQJHaJCg9XClQ6eZGKB6+G1CSvstbyCPockZ5Jms7OQLIjM3Ofp5ZVsqtJ8KbaMq\ns8u8p7upP+JslDGQT3eKq22zbiY78f8Fn9KvUWmPa4vEXYovau+s5QIDAQABo4G8\nMIG5MAkGA1UdEwQCMAAwJwYJYIZIAYb4QgENBBpFbm9zIEdlbmVyYXRlZCBDZXJ0\naWZpY2F0ZTAdBgNVHQ4EFgQU2+AZzfu8kL4+xUOy1nrulgHLBrcwHwYDVR0jBBgw\nFoAUg2PMjfd6uZEVG+HmhWYfVNuBhxowQwYJYIZIAYb4QgEEBDZodHRwczovL2Fs\ncGhhLXBvcnRhbC1jbjQuZW5pb3QuaW86ODA4MS9lbm9zL0NBL2NybC9SU0EwDQYJ\nKoZIhvcNAQELBQADggEBABonMzhNpDhXLPSwsm2x3xzgsnsYiCzZd+2+T01zN9dt\no/UOrG3OLduZd90DrqKmsTXOhcNsUxrhdFo2sB2N6xEsHhB6vH41LdHHdvAJjEG9\nlKpU9ZX666loa9GUcN1/Lm2+MjBkUw7GBbSZGQBFRII6JDiBWlWzgzvjeTkB4i0u\nHcZ/y/S1Fv5jmF1vxFLvXUiBvljf3YPqVFFGt4WNXvWuDpRG0RRdozo4UkYrlJOD\nkZTFP4jSyROAFvvc4d5TnMtOySvKuAmRD7UmHrDoT/gNd4SG3f3fpTBVsxFHs4FI\nTXllWR55xQv68rEn8VsoUUpPpLzyZ+AmiOocOCCIhQY=\n-----END CERTIFICATE-----\n",
        "certSN": "52771",
        "issueAuthority": "RSA"
    }
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.cert;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.cert.RenewCertificateRequest;
import com.envisioniot.enos.connect_service.v2_1.cert.RenewCertificateResponse;
import com.envisioniot.enos.connect_service.vo.DeviceIdentifier;

public class RenewCert {

    public static void main(String[] args) {
        String appKey = "yourAppAccessKey";
        String appSecret = "yourAppSecretKey";
        String serverUrl = "https://{apigw-address}";

        String orgId = "yourOrgId";
        // newCert表示CSR文件，为可选项，如不包含该参数，则以旧证书的请求数据重新生成证书。
        String newCert = "-----BEGIN NEW CERTIFICATE REQUEST-----\n" +
                "MIICwTCCAakCAQAwfDELMAkGA1UEBhMCQ04xETAPBgNVBAgMCFNoYW5naGFpMREw\n" +
                "DwYDVQQHDAhTaGFuZ2hhaTENMAsGA1UECgwERW5PUzERMA8GA1UEAwwITVJtSXl6\n" +
                "UFcxDTALBgNVBAsMBEVuT1MxFjAUBgkqhkiG9w0BCQEWBzREbmIxVDEwggEiMA0G\n" +
                "CSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC+dU5jLAu7Kb88hONou6PycTnv9+3/\n" +
                "FFPaHm5I8vPfhh0QL6TcunKpm97Dyds1yHgMCqVT+gWgO4MHFz8TiIb9JKRjHn/6\n" +
                "kFea1ccZU9nYGuv+yMGqa340NjN/vP+XpjXm6Xkqw7ujehhNoBuKJZh6+uXlf2yw\n" +
                "1gTP9vWJTc7cuiky2jgKl6/47iKEmIMT1xpHVDp16LWX08/aamJESPJ171RFFxf/\n" +
                "6z2taiK/z7McXFRHk+SdYGN0iTNZQqoFKi3S9S8FvkLBQF8gHOytZdpnSz6SZwW0\n" +
                "DJUv8VGFWQYOVU67BzVR59s0CVM9IdAHntjXm2t3BF0A9kKZa6VDzHpxAgMBAAGg\n" +
                "ADANBgkqhkiG9w0BAQsFAAOCAQEASGPYV0t4zPT3XA42SKqNzNEiYvB550/6Vh1y\n" +
                "mxD+mQXeyvkZn5OcxtuzrgD7aBVRcT/j+tK4XP8s+ODYiM+VSrqLs+a5ZGmOhHHf\n" +
                "36MdmAK8I/dNyHZBiTf+GI5ibul2vaSpYYUwarzMu0azT6+d2qiUl7TqVVIGo4+P\n" +
                "PSRp+V+9e4RJ/TKUjAToBazz154tXU5psVmQ1Ac9oF7Y/9AvGTtusLUDHCu3T45J\n" +
                "QiwAUsMkSla5HCZEftNV8uC+BR6GktfFGLv3Gx+havoBsi82OPDUbBBtKgbiIQyq\n" +
                "bslaLc4GkDZTZPz4st7/ChYOZVJNxz2CAx1JU4VAfjonqChzbw==\n" +
                "-----END NEW CERTIFICATE REQUEST-----";
        Integer certSn = 2667;
        RenewCertificateRequest request = new RenewCertificateRequest();
        request.setCertSn(certSn);
        request.setCsr(newCert);
        //validDay indicates the validity period of the certificate and is optional. If this parameter is not included in your code, the default validity period of the EnOS deployment will be used.
        request.setValidDay(220);
         /*
         * Use one of the following methods to identify a device:
         * ASSET_ID
         * PRODUCT_KEY + DEVICE_KEY
         */
        request.setAssetId(ASSET_ID);
        request.setProductKey(PRODUCT_KEY);
        request.setDeviceKey(DEVICE_KEY);
        request.setDevice(identifier);
        request.setOrgId(orgId);
        RenewCertificateResponse certRsp = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, RenewCertificateResponse.class);
        System.out.println(certRsp.getData());
    }
}
```



<!--End-->
