# Check Asset Permission

Check if the current user has the access permission for the queried asset.


## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/user/authorization/asset/check
```

## Request Parameters (Header)

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


## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get assetId >> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - boolean
     - 
       + true = has access for all the queried assets 
       + false = has no permission or has permission for only some of the queried assets



## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.0/user/authorization/asset/check
method: POST
requestHeader: {"Authorization":"yourBearerToken"}
requestBody:{
  "assetIds": [
    "rJDyH3Rm",
    "FS6c3XAH",
    "qQHC4vyw",
    "txeiiU9x",
    "adNIljjB",
    "Dqp9GZsT",
    "Mk2BVzZN"
  ]
}
```

### Return Sample
```json
{
  "code": 200,
  "message": "",
  "data": false
}
```