# Get Assets by Organization


Get all the assets that a specified user can access under a specified organization.


## Prerequisites

- The associated application has been purchased by the organization.

- The associated application must have access permissions (authorized by the organization administrator) for the assets.



## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/user/asset/list
```


## Request Parameters (Body)


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - userId
     - Mandatory
     - String
     - The user ID.
   * - orgId
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId >> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. If not specified, the default pagination size is 1000 pages, starting from 0. For more details, see `Pagination Request Struct </docs/api/en/2.1.0/overview.html#pagination-request-struct>`__



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The pagination and list of the assets' information.

### data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - pagination
     - Pagination Struct
     - The pagination information.
   * - assets
     - Assets Struct
     - The list of the assets' information.

### Pagination Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - pageNo
     - Integer
     - The request pages.
   * - pageSize
     - Integer
     - The number of records in each page.
   * - totalElements
     - Long
     - The total number of records.


### Assets Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The asset ID.
   * - name
     - StringI18n
     - The asset's name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - orgId
     - String
     - The organization ID which the asset belongs to.



## Samples

### Request Sample

```json
url: https://alpha-apim-cn4.eniot.io/app-portal-service/v2.0/user/asset/list
method: POST
requestBody:
{
  "userId": "yourUserId",
  "orgId": "yourOrgId",
  "pagination": {
    "pageNo": 0,
    "pageSize": 1000,
    "sorters": []
  }
}
```


## Response Parameters

```json
{
  "code": 200,
  "message": "",
  "data": {
    "pagination": {
      "totalElements": 2,
      "pageNo": 0,
      "pageSize": 1000
    },
    "assets": [
      {
        "id": "2rVQ6zfF",
        "name": {
          "default": "wyf_asset_01",
          "en_US": "wyf_asset_01"
        }
      },
      {
        "id": "Sx0faZHR",
        "name": {
          "default": "12345678901234567890123456789012345678901234567890",
          "en_US": "12345678901234567890123456789012345678901234567890"
        }
      }
    ]
  }
}
```