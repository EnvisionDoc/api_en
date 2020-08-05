# Revoke Refresh Token

Revoke a user's refresh token.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/refreshToken/revokeAll
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
   * - Content-Type
     - Optional
     - String
     - The content type of the returned content is "application/x-www-form-urlencoded".


## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - refreshToken
     - Mandatory
     - String
     - The refresh token. Refer to `Choose Organization <choose_organization>`__ to learn how to get the refresh token.


## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.0/refreshToken/revokeAll
method: POST
requestHeaders: 
{
  "Authorization":"yourBearerToken"
}
requestBody:
{
  "refreshToken":"yourRefreshToken"
}
```

### Return Sample

```json
{
  "code":200,
  "message":"",
  "data":null
}
```
