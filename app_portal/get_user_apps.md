# Get User's Applications

Get a list of applications that the current user has permission to access through the access token.


## Request Format

```
GET http://{apigw-address}/app-portal-service/v2.0/user/app/list
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
     - The data of the list of apps.


### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - apps
     - AppDTO Struct
     - The deatils of the application.

### AppDTO Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The application ID.
   * - identifier
     - String
     - The application identifier given by the user.
   * - name
     - String
     - The application name.
   * - description
     - String
     - The application description.
   * - type
     - Integer
     - The application type.

       + 0: web application
       + 1: mobile application

   * - createdTime
     - String
     - The time the application was created.
   * - status
     - Boolean
     - The application status under the organization.

       + 0: not enabled
       + 1: enabled
   * - order
     - Integer
     - The position of the application in the organization. 0 means the first position. The higher the number, the lower the position.
   * - url
     - String
     - The URL of the application.
   * - isShortcut
     - Boolean
     - + true = this application is a shortcut
       + false = this application is not a shortcut
   * - category
     - ApplicationCategory Struct
     - The application category ID and name. For example, "21" represents "Wind" and "22" represents "Solar". For details on the structure, see `ApplicationCategory Struct <get_user_apps#applicationcategory-struct>`__ . For more information on the list of Application Categories, see `List of Application Categories <get_user_apps#list-of-application-categories>`__


### ApplicationCategory Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - Integer
     - The application category ID.
   * - name
     - String
     - The application category name.

### List of Application Categories

.. list-table::
   :widths: auto
   :header-rows: 1

   * - ID
     - Name
   * - 21
     - Wind
   * - 22
     - Solar
   * - 23
     - Hydroelectricity
   * - 24
     - Thermal
   * - 25
     - Storage
   * - 26
     - Pile
   * - 27
     - Electricity Sale
   * - 28
     - Distribution Network
   * - 29
     - Micro Intelligent Network
   * - 30
     - Industry Park
   * - 31
     - Smart Building
   * - 32
     - Smart City
   * - 33
     - AI
   * - 34
     - Other
   * - 35
     - Comprehensive
   * - 36
     - Substation





## Samples

### Request Sample

```
url: http://alpha-apim-cn4.eniot.io/app-portal-service/v2.0/user/app/list
headers: {Authorization=yourBearerToken}
method: GET
```

### Return Sample

```json
{
    "code":200,
    "data":{
        "apps":[
            {
                "category":{
                    "id":27,
                    "name":"Electricity Sale"
                },
                "createdTime":"2019-05-28 07:49:39",
                "description":"售电能源资产管理",
                "id":"accessKey",
                "isShortcut":false,
                "name":"Energy assets Mgmt",
                "order":4,
                "status":false,
                "type":0
            },
            {
                "category":{
                    "id":21,
                    "name":"Wind"
                },
                "createdTime":"2019-06-19 05:03:32",
                "description":"默认菜单组5",
                "id":"accessKey",
                "isShortcut":false,
                "name":"默认菜单组5",
                "order":6,
                "status":true,
                "type":1
            }
        ]
    },
    "message":""
}
```
