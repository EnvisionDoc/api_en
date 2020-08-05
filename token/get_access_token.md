# Get Access Token

<br />

​Get the access token using the access key and secret key of your application.

<br />

If the access token for your application is already generated, when you call the **Get Access Token** API again, the same access token will be returned if the access token has not expired.

## Prerequisites

Register an application on the EnOS Management Console to get the application's access key and secret key, which are required as the values of the `appKey` and `appSecret` request parameters of the **Get Access Token** API.

## Request Format

```http
POST https://{apigw-address}/apim-token-service/v2.0/token/get
```

## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - appKey
     - Mandatory
     - String
     - The access key of the application.
   * - encryption
     - Mandatory
     - String
     - The encrypted ciphertext. For more details, see `Encryption Generation Rule <#encryption-generation-rule>`__
   * - timestamp
     - Mandatory
     - Long
     - The timestamp of the current system time (UNIX time, accurate to the millisecond), e.g. 1572574909697


### Encryption Generation Rule

1. Concatenate the values of ``appKey``, ``timestamp``, and ``appSecret`` to generate a string for encryption.

2. Encode the concatenated string in UTF-8 format and make a digest by **SHA256** algorithm.

3. Convert the digest to hexadecimal format to generate the encrypted ciphertext. See the following pseudo code:
```
sha256(appKey+timestamp+appSecret).toLowerCase();
```

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Descritpion
   * - status
     - Integer
     - The API request status code, with 0 indicating a successful request.
   * - msg
     - String
     - The explanation of the status code.
   * - business
     - String
     - The business parameter, with the value of `apim-token-service`.
   * - data
     - Data Struct
     - The generated access token and its expiring time.


### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - accessToken
     - String
     - The value of the generated access token.
   * - expire
     - Integer
     - The expiring time of the access token in seconds, with an initial value of 7,200 (i.e. 2 hours).


## Sample

### Request Sample

```http
POST
https://{apigw-address}/apim-token-service/v2.0/token/get   
{
	"appKey": "5acb82e7-a11e-4300-9164-c8b20b638e8b",
	"encryption": "87c6885cec7525e2f219f86a82b280cc8c2d6ff4040a4b5f8acf9aeeda37aba8",
	"timestamp": 1572574909697
}
```

### Return Sample

```json
{
    "stauts": 0,
    "msg": "SUCCESS",
    "business": "apim-token-service",
    "data": {
        "accessToken": "Generated_Access_Token",
        "expire": 7200
    }
}
```
