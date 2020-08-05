# Authorize Asset

When a new asset on the EnOS platform is synchronized to the Application Portal, use this API to authorize the new asset to the asset creator.

## Prerequisite

The associated application must have access permissions (authorized by the organization administrator) for the user and asset information.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.0/asset/append
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
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get assetId >> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__




## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Boolean
     - + true = successful
       + false = unsuccessful


## Samples

### Request Sample

```json
url: https://alpha-apim-cn4.eniot.io/app-portal-service/v2.0/user/asset/append
method: POST
requestBody:
{
  "userId": "yourUserId",
  "assetIds": [
    "H77kS15O"
  ],
  "orgId": "yourOrgId"
}
```


### Return Sample

```json
{"code":200,"message":"","data":true}
```

