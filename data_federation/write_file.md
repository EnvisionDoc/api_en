# Write File

Write a file to data source through a specified channel.

## Prerequisites

Write channels are created and started in the organization.

## Request Format

```
POST https://{apigw-address}/data-federation/v2.0/channels/write/{channelId}/file
```

## Request Parameters (Header)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Content-Type
     - Mandatory
     - String
     - Content or file type. The default value is `application/json`.
   * - Authorization
     - Mandatory
     - String
     - Access Token, by the format of `Bearer xxx`. `How to get the Access Token >> <../token/get_access_token>`__


## Request Parameters (URI)

.. list-table::
   :widths: 15 25 15 15 30
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
     - Your organization ID. `How to get the orgId>> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__
   * - channelId
     - Path
     - Mandatory
     - String
     - Channel ID
   * - dataSourceName
     - Query
     - Mandatory
     - String
     - 数据源别名

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - fileName
     - Mandatory
     - String
     - 待写入的文件名

## Error Code


## Sample

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels/write/{channelId}/file&orgId={}&dataSourceName={}

method: POST

requestBody:

```

### Return Sample

```
{
  "msg": "OK",
  "code": 0,
  "submsg": ""
}
```
