# Get Users with Asset Access 

Get the list of users who have access permission to a specific asset.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.1/asset/authorize/user/list
```

## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - assetId
     - Mandatory
     - String
     - The asset ID. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - orgId
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The user information.


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


## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.1/asset/authorize/user/list
method: POST
requestBody:
{
  "orgId":"yourOrgId",
  "assetId":"Dqp9GZsT"
}
```


### Return Sample

```json
{
    "code": 200,
    "message": "",
    "data": [
        {
            "id": "theUserId",
            "name": "Pony"
        }
    ]
}
```
