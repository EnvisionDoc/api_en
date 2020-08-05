# Get Token Information

Get information about the user who is currently logged-in through the access token.

## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.1/session/info
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



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The details of the user who is currently logged-in. For more information, see `Data Struct <get_token_information#data-struct>`__

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - userId
     - String
     - The user ID.
   * - userName
     - String
     - The user name.
   * - currentOrgId
     - String
     - The current organization ID.
   * - currentOrgName
     - String
     - The current organization name.



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.1/session/info
headers: {"Authorization":"yourBearerToken"}
method: GET
```

### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": {
    "userId": "yourUserId",
    "userName": "portal_demo",
    "currentOrgId": "yourOrgId",
    "currentOrgName": "Portal Demo"
  }
}
```
