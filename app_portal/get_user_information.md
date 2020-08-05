# Get User Information

Get the information of the current user.


## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.0/user/info
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
     - The information of the user.



### Data Struct


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
     - The time the user joined the current organization.
   * - type
     - Integer
     - The user type.
     
       + 0 = Application Portal account
       + 1 = Third-party domain account



## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/user/info
headers: {"Authorization":"yourBearerToken"}
method: GET
```

### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": {
    "id": "yourUserId",
    "name": "portal_demo",
    "domain": "",
    "description": "",
    "nickName": "",
    "phoneArea": "",
    "phone": "",
    "email": "1@163.com",
    "createdTime": "2019-05-27 04:33:30.0",
    "type": 0
  }
}
```
