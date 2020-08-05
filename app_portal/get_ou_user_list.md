# Get Organization User List

Authorize an application to get a list of all the users under a specified organization (OU) without logging in to the Application Portal.

## Prerequisite

The associated application must have access permissions (authorized by the organization administrator) to get the user information.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/user/organization/roster
```

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
     - The pagination and list of the users' information.



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
   * - users
     - Array of Users Struct
     - The list of the users' information.

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



### Users Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - userId
     - String
     - The user ID.
   * - email
     - String
     - The user's registered email.
   * - phone
     - String
     - The user's registered phone number.
   * - phoneArea
     - String
     - The area code of the user's registered phone number.
   * - name
     - String
     - The user name.



## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.0/user/organization/roster
method: POST
requestBody: 
{
  "orgId": "yourOrgId",
  "pagination": {
    "pageNo": 0,
    "pageSize": 1000,
    "sorters": []
  }
}
```


### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": {
    "users": [
      {
        "userId": "userId_1",
        "email": "1234",
        "phone": "",
        "phoneArea": "",
        "name": "1234"
      },
      {
        "userId": "userId_2",
        "email": "71019669@qq.com",
        "phone": "",
        "phoneArea": "",
        "name": "wyf"
      }
    ],
    "pagination": {
      "totalElements": 2,
      "pageNo": 0,
      "pageSize": 1000
    }
  }
}
```

