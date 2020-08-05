# Get Assets by Application

Get all the assets that the current user can access under a specified application.

## Prerequisites

- The associated application has been purchased by the organization.

- The associated application must have access permissions (authorized by the organization administrator) for the assets.

## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.1/user/app/asset/tree
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
   * - accessKey
     - Query
     - Mandatory
     - String
     - The service account of the application. The application authenticates with ``accessKey`` to obtain the data that it is authorized to access. `How to get accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__


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
     - The list of the assets.

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The node ID.
   * - name
     - String
     - The node name.
   * - tag
     - String
     - The tag of a node. "Asset" will mean the node is an asset with a parent node that is also an organizational structure node (because an asset can only be mounted on the leaf node of the organizational structure), and "null" will mean the node is an organizational structure node. 
   * - parentId
     - String
     - The parent node ID.
   * - children
     - Data Struct
     - The child nodes.



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.1/user/app/asset/tree?accessKey=yourAccessKey
method: GET
requestHeader: 
{
  "Authorization":"yourBearerToken"
}
```

### Return Sample

```json 
{
  "id": "sg1566xxxxxxxxxx",
  "name": "Solar_shangHai",
  "tag": null,
  "parentId": "",
  "children": [
    {
      "id": "sg15663524029331",
      "name": "江阴",
      "tag": null,
      "parentId": "sg1566xxxxxxxxxx",
      "children": [
        {
          "id": "zULM004t",
          "name": "Solar_Assert",
          "tag": "asset",
          "parentId": "",
          "children": null
        },
        {
          "id": "osvxGtJC",
          "name": "shangHai",
          "tag": "asset",
          "parentId": "",
          "children": null
        }
      ]
    }
  ]
}
```
