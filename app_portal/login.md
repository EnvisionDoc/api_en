# Log In

Log in to the account.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/login
```


## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - account
     - Mandatory
     - String
     - The user name.
   * - password
     - Mandatory
     - String
     - The password of the user name.



## Response Parameters


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The details of the user.

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - organizations
     - Array of IdNamePair Structs
     - The list of organizations that the user belongs to.
   * - user
     - IdNamePair Struct
     - The ID and name of the user.
   * - accessToken
     - String
     - The access token, represented as bearer token.

### IdNamePair Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The organization/user ID.
   * - name
     - String
     - The organization/user name.

## Error Code

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 31400
     - User password is missing or not valid
   * - 31429
     - Attemp of accessing with incorrent password or IP reaches the limit. Please try again later.

## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/login
{"account":"portal_demo","password":"yourPassword"}
method: POST
```

### Return Sample

```json
{
  "code": 200,
  "data": {
    "accessToken": "APP_PORTAL_S_WX89rC4pqsMc478tyP6gb9zFmT9qYaW7",
    "organizations": [
      {
        "id": "yourOrgId_1",
        "name": "Portal Demo"
      },
      {
        "id": "yourOrgId_2",
        "name": "rm_0726_001"
      }
    ],
    "user": {
      "id": "yourUserId",
      "name": "portal_demo"
    }
  },
  "message": ""
}
```
