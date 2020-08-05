# Get Asset Structure   

Get the upstream organizational structure where the asset is located.



## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.1/asset/structure
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
   * - assetIds
     - Query
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get assetId >> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__




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
     - The organizational structure.



### data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - structures
     - AssetStructure Struct
     - The list of the organizational structure tree.


### AssetStructure Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The organizational structure ID.
   * - name
     - String
     - The organizational structure name.
   * - description
     - String
     - The organizational structure description.
   * - orgId
     - String
     - The organizational ID where the organizational structure is located.
   * - children
     - AssetStructure Struct
     - The sub-organizational structure.



## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.1/asset/structure?assetId=Dqp9GZsT
method: GET
requestHeader: 
{
  "Authorization":"yourBearerToken"
}
```


### Return Sample

```json
{
  "code": 200,
  "data": {
    "structures": [
      {
        "children": [],
        "description": "",
        "displayName": "wyf",
        "id": "sg1566xxxxxxxxxx",
        "name": "wyf",
        "orgId": "yourOrgId"
      }
    ]
  },
  "message": ""
}
```
