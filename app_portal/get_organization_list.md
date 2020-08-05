# Get Organization List

List the organizations which the current user belongs to according to the access token.

## Request Format

```
url: https://{apigw-address}/app-portal-service/v2.0/user/organization/list
method: GET
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
     - The list of the organizations.

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - organizations
     - IdNamePair Struct
     - The details of the organizations.

### IdNamePair Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The organization ID.
   * - name
     - String
     - The organization name.



## Samples

### Request Sample

```
GET
https://{apigw-address}/app-portal-service/v2.0/user/organization/list
headers: {"Authorization":"yourBearerToken"}
```

### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": {
    "organizations": [
      {
        "id": "yourOrgId_1",
        "name": "rm_0726_001"
      },
      {
        "id": "yourOrgId_2",
        "name": "Portal Demo"
      }
    ]
  }
}
```
