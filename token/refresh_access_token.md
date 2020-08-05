# Refresh Access Token

<br />

​​Refresh the generated access token before it expires (the expiring time of the access token is 2 hours by default).

## Request Format

```http
POST https://{apigw-address}/apim-token-service/v2.0/token/refresh
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
     - The encrypted ciphertext. For more details, see `Encryption Generation Rule <get_access_token#encryption-generation-rule>`__
   * - timestamp
     - Mandatory
     - Long
     - The timestamp of the current system time (UNIX time, accurate to the millisecond), e.g. 1572574909697
   * - accessToken
     - Mandatory
     - String
     - The access token to be refreshed.


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
     - The refreshed access token and its expiring time.



### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - accessToken
     - String
     - The refreshed access token.
   * - expire
     - Integer
     - The expiring time of the access token in seconds, with an initial value of 7,200 (i.e. 2 hours).


## Sample

### Request Sample

```html
POST
https://{apigw-address}/apim-token-service/v2.0/token/refresh  
{
	"appKey": "5acb82e7-a11e-4300-9164-c8b20b638e8b",
	"encryption": "87c6885cec7525e2f219f86a82b280cc8c2d6ff4040a4b5f8acf9aeeda37aba8",
	"accessToken":"adsfwerasdfsdfasggaaf",
	"timestamp": 1572574909697
	}
```


### Return Sample

```json
{
    "status": 0,
    "msg": "SUCCESS",
    "business": "apim-token-service",
    "data": {
        "accessToken": "Refreshed_Access_Token",
        "expire": 7200
    }
}
```
