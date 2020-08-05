# Get App User List

Based on the `accessKey` of an application, get the list of users who have access to the application.


## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.2/user/list
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
     - APIUserDTO Struct
     - The list of the users' information.


### APIUserDTO Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - userId
     - String
     - User ID.
   * - email
     - String
     - The user's registered email address.
   * - phoneArea
     - String
     - The area code of the user's registered phone number.
   * - phone
     - String
     - The user's registered phone number.
   * - name
     - String
     - User name.

## Error Code

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 31401
     - The provided access token is not valid.
   * - 31403
     - OU administrator permission is required.

## Sample

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.2/user/list
method: POST
requestBody:
{
  "pagination":{
    "pageSize":1000,
    "pageNo":0
  }
}
```

### Return Sample

```json
{
  "code": 0,
  "message": "",
  "data": {
    "pagination":{
      "totalElements":15000,
      "pageSize":1000,
      "pageNo":0
    },
    "users": [
      {
        "userId": "u15665532373241",
        "email": "1123456666@Fsn.sg",
        "phoneArea": "",
        "phone": "",
        "name": "1123456666@Fsn.sg"
      },
      {
        "userId": "u15665405431611",
        "email": "1qaz@ws.sx",
        "phoneArea": "",
        "phone": "",
        "name": "1qaz"
      }
    ]
  }
}
```
