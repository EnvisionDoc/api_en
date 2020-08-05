# Get Unresolved Messages

Get the list of unresolved messages that are reported for the applications.

## Prerequisites

Your organization has purchased the applications.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/message/unresolved/list
```

## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - accessKey
     - Mandatory
     - String
     - The service account of the application. The application authenticates with ``accessKey`` to obtain the data that it is authorized to access. `How to get accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
   * - orgId
     - Mandatory
     - String
     - The organization ID. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
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
     - The pagination and list of unresolved messages.


### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - pagination
     - Pagination Struct
     - The pagination information.
   * - ids
     - List<String>
     - The list of message IDs.


## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/message/unresolved/list
method: POST
requestBody:
{
  "accessKey":"624a8374-xxxx-xxxx-xxxx-ebabadec4524",
  "orgId":"yourOrgId",
  "pagination":{
    "pageNo":0,
    "pageSize":1000
  }
}
```


### Return Sample

```json
{
    "code": 200,
    "message": "",
    "data": {
        "pagination": {
            "total": 15094,
            "currentPage": 0,
            "limit": 1000
        },
        "ids": [
            "cjj-1",
            "cjj01",
            "cjj010",
            "cjj011",
            "cjj012",
            "..."
        ]
    }
}
```
