# Get Asset

Get asset data by asset ID.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Read

## Request Format

```
GET https://{apigw-address}/asset-service/v2.1/assets?action=get
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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - assetId
     - Query
     - Mandatory
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Asset Struct
     - The details of the asset. For more information, see `Asset Struct </docs/api/en/2.1.0/asset/get_asset.html#asset-struct-asset>`_ .


### Asset Struct <asset>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - assetId
     - String
     - The asset ID.
   * - orgId
     - String
     - The organization ID which the asset belongs to.
   * - name
     - StringI18n
     - The asset's name in its respective locale's language. For more details on the structure and locales supported, see  `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - description
     - String
     - The asset description.
   * - attributes
     - Map
     - Attributes of the model which the asset belongs to. The Key is the attribute ID, which is of String type. The Value type depends on the attribute defined in the model. 
   * - timezone
     - String
     - The timezone where the asset is located.
   * - modelId
     - String
     - The model ID.
   * - modelIdPath
     - String
     - The model ID path. E.g.: /Turbine/Double_Feed_Turbine
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)


## Error Codes

Refer to [Public Response Codes](/docs/api/en/2.1.0/overview.html#public-response-codes-connection-service-etc).



## Samples

### Request Sample

```
url: https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=yourOrgId&assetId=yourAssetId
method: GET 
```

### Return Sample

```json
{
  "msg": "OK",
  "code": 0,
  "data": {
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
    "timezone": "+00:00",
    "name": {
      "defaultValue":"venus!",
      "i18nValue": {
        "en_US": "English name ",
        "zh_CN": "Chinese name"
      }
    },
    "attributes": {
      "system": "Solar System"
    },
    "modelIdPath": "/planet",
    "orgId": "yourOrgId",
    "desc": null,
    "tags": {
      "tag1":"bright"
    }
  },
  "requestId": "9a5cfbac-b2f8-4a37-b38d-8bccdd77d073"
}
```


## Java SDK Sample

```java
public class GetAsset {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        GetAssetRequest request = new GetAssetRequest();
        request.setOrgId(orgId);
        request.setAssetId("XBOBqC1O");

        GetAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey)
                .appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getCode());
    }
}
```
