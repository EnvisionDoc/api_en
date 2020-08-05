# Get Manageable User List

List all users that can be managed under the current account.

## Prerequisite

The requester must be the organization administrator.


## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/organization/user/list
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
     - UserDTO Struct
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



### UserDTO Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The user ID.
   * - name
     - String
     - The user name.
   * - domain
     - String
     - The domain name.
   * - description
     - String
     - The description of the user.
   * - nickName
     - String
     - The nickname of the user.
   * - phoneArea
     - String
     - The area code of the user's registered phone number.
   * - phone
     - String
     - The user's registered phone number.
   * - email
     - String
     - The user's registered email.
   * - createdTime
     - String
     - The time when this user account was created.
   * - joinTime
     - String
     - The time when the user joined the current organization.
   * - type
     - Integer
     - The user type.

       + 0: Application Portal account
       + 1: Third-party domain account
   * - exists
     - Boolean
     -
       + true = the user is in the current organization
       + false = the user is not in the current organization
       + null = the organization is not enabled

## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.0/organization/user/list
method: POST
header:
{
  "Authorization":"yourBearerToken"
}
requestBody: {
    "pageNo":0,
    "pageSize":5,
    "sorters":[]
}
```

### Return Sample

```json
{
    "code": 200,
    "message": "",
    "data": {
        "pagination": {
            "totalElements": 5,
            "pageNo": 0,
            "pageSize": 5
        },
        "users": [
            {
                "id": "userId_1",
                "name": "asd@aaa.com",
                "domain": "新增域测试",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "asd@aaa.com",
                "createdTime": "2019-09-23 02:32:51.0",
                "joinTime": "2019-09-23 02:32:52.0",
                "type": 1
            },
            {
                "id": "userId_2",
                "name": "12345@qq.com",
                "domain": "yang",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "12345@qq.com",
                "createdTime": "2019-09-20 06:46:34.0",
                "joinTime": "2019-09-20 06:46:34.0",
                "type": 1
            },
            {
                "id": "userId_3",
                "name": "435",
                "domain": "",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "435@qq.com",
                "createdTime": "2019-09-19 08:24:17.0",
                "joinTime": "2019-09-19 08:24:17.0",
                "type": 0
            },
            {
                "id": "userId_4",
                "name": "jane",
                "domain": "",
                "description": "",
                "nickName": "",
                "phoneArea": "",
                "phone": "",
                "email": "jane@test.com",
                "createdTime": "2019-05-30 07:41:31.0",
                "joinTime": "2019-09-11 09:42:54.0",
                "type": 0
            },
            {
                "id": "userId_5",
                "name": "portal_test01",
                "domain": "",
                "description": "",
                "nickName": "quququ",
                "phoneArea": "",
                "phone": "123232323",
                "email": "portaltest01@email.com",
                "createdTime": "2019-05-14 08:38:31.0",
                "joinTime": "2019-09-06 14:09:01.0",
                "type": 0
            }
        ]
    }
}
```
