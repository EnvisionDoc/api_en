# Refresh Access Token

Request a new access token using the refresh token.


## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.0/token/refresh
```

## Request Parameters (URI)


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - refreshToken
     - Query
     - Mandatory
     - String
     - The refresh token. Refer to `Choose Organization <choose_organization>`__ to learn how to get the refresh token.



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The details of the new access token.

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
   * - accessToken
     - String
     - The new access token.
   * - refreshToken
     - String
     - The new refresh token.
   * - refreshTokenExpire
     - String
     - The refresh token expiration time in UTC format. For time formats, refer to `ISO8601 Standard Time Formats Used by UTC </docs/api/en/2.1.0/api_faqs.html#iso8601-standard-time-format-adopted-by-utc-time>`__



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/token/refresh?refreshToken=yourRefreshToken
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
    "currentOrgName": "Portal Demo",
    "accessToken": "yourBearerToken",
    "refreshToken": "yourRefreshToken",
    "refreshTokenExpire": 1571368315000
  }
}
```
