# Choose Organization

Select the organization that the user needs to use after login.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.1/session/set
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
   * - orgId
     - Mandatory
     - String
     - The organization ID.



## Response Parameters


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The details of the organization.

### data Struct

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
     - The access token in the request.
   * - refreshToken
     - String
     - The new refresh token.
   * - refreshTokenExpire
     - String
     - The refresh token expiration time in UTC format. For the time format, see `ISO8601 Standard Time Formats Used by UTC </docs/api/en/2.1.0/api_faqs.html#iso8601-standard-time-format-adopted-by-utc-time>`__



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.1/session/set
headers: {"Authorization":"yourBearerToken"}
method: POST
requestBody:
{
  "orgId":"yourOrgId"
}
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
    "refreshTokenExpire": 1570018958000
  }
}
```
