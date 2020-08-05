# Log Out

Log out of the account.

## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.0/logout
```

## Request Parameters (Headers)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Authorization
     - Mandatory
     - String
     - The access token (or bearer token). Refer to `Log In <login>`__ or `Refresh Access Token <refresh_access_token>`__ to learn how to get the access token.



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Boolean
     - + true = successful
       + false = unsuccessful



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/logout
headers: {"Authorization":"yourBearerToken"}
method: GET
```

### Return Sample

```json
{
  "code":200,
  "message":"",
  "data":true
}
```