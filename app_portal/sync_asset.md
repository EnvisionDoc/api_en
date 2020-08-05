# Sync Asset

Synchronize assets on the EnOS to the Application Portal.


## Prerequisites

- The associated application has been purchased by the organization.

- The associated application must have access permissions (authorized by the organization administrator) for the assets.

## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.0/asset/sync
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
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId >> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Boolean
     - (null)



## Samples

### Request Sample

```
url: https://alpha-apim-cn4.eniot.io/app-portal-service/v2.0/asset/sync?orgId=yourOrgId
method: GET
```


### Return Sample

```json
{"code":200,"message":"","data":null}
```
