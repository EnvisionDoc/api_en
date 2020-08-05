# Get User Domain

Get the domain information of a user using the email address.


## Request Format

```
GET http://{apigw-address}/app-portal-service/v2.2/user/domain
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
   * - email
     - Query
     - Mandatory
     - String
     - The email address of the user.


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The domain ID.
   * - name
     - String
     - The domain name.
   * - url
     - String
     - The domain URL.
   * - description
     - String
     - The description of the domain.


## Error Code

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 31400
     - The user email address is required.



## Samples

### Request Sample

```
url: http://{apigw-address}/app-portal-service/v2.2/user/domain?email=xxx.yy@envision-digital.com
method: GET
```

### Return Sample

```json
{
    "code":0,
    "data":{
        "id":"xxx",
        "name":"domain name",
        "url":"domain url",
        "description":"domain description"
    },
    "message":""
}
```
