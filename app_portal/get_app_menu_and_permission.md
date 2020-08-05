# Get App Menu and Permission

Get the list of application menus and permissions.

## Prerequisites

- The associated application has been purchased by the organization.

- The user must have access permission for the application's menus and permissions (otherwise the response result is empty).

## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.1/user/app/resource/info
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
     - The list of application menus and permissions.

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - permissions
     - Array
     - The list of permissions.
   * - menus
     - Array
     - The list of menus.

### Permission List

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The permission ID.
   * - identifier
     - String
     - The permission identifier.
   * - name
     - String
     - The permission name.


### Menu List

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The menu ID.
   * - name
     - String
     - The menu name.
   * - identifier
     - String
     - The menu identifier.
   * - displayOrder
     - Integer
     - The display order of the menu. The value is an integer starting from 1. The smaller the number is, the higher the place on the menu list.
   * - url
     - String
     - The menu URL.
   * - parentId
     - String
     - The parent menu.
   * - children
     - Menu Struct
     - The sub-menu.



## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.1/user/app/resource/info?accessKey=app_1
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
  "message": "",
  "data": {
    "permissions": [],
    "menus": [
      {
        "id": "accessKey",
        "identifier": "menu",
        "name": "menu",
        "url": "/a",
        "displayOrder": 1,
        "parentId": "",
        "children": []
      },
      {
        "id": "accessKey",
        "identifier": "menu2",
        "name": "menu2",
        "url": "/eos-wind-map/assetOverview.html",
        "displayOrder": 2,
        "parentId": "",
        "children": []
      }
    ]
  }
}
```
