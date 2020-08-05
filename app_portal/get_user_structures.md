# Get User Structures

Get the information of the organization structure to which a user is assigned.


## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.2/user/structures
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
     - The list of organization structure.

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - structures
     - StructureDTO Struct
     - The list of organization structures.

### StructureDTO Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The node ID in the organization structure.
   * - name
     - String
     - The name of the organization structure.
   * - parentId
     - String
     - The parent node ID.


## Error Code

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 31401
     - The provided access token is not valid.



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.2/user/structures
method: GET
header: {"Authorization":"Bearer APP_PORTAL_S_TDKKeqfYBK3m5z3LRgKVqThWDYnRBN44"}
```

### Return Sample

```json
{
    "code":0,
    "data":{
        "structures":[
          {
            "id":"sg133",
            "name":"name133",
            "parentId":"sg13"
          },
          {
            "id":"sg134",
            "name":"name134",
            "parentId":"sg14"
          },
        ]
    },
    "message":""
}
```
