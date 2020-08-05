# Update Asset

Update asset information.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Write

## Prerequisite

- The asset to be updated must exist.
- The fields to be updated must exist.

## Request Format

```
POST https://{apigw-address}/asset-service/v2.1/assets?action=update
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
   * - isPatchUpdate
     - Query
     - Optional
     - Boolean
     - + true (default) = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.
       + false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.


## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - asset
     - 
       + If ``isPatchUpdate`` = ``true``, then optional
       + If ``isPatchUpdate`` = ``false``, then mandatory
     - AssetUpdateVo Struct
     - Used for asset update.
       + When ``isPatchUpdate`` is ``true`` , only the fields specified in this structure are updated. The values of those fields not specified will be retained.
       + When ``isPatchUpdate`` is ``false`` , the fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.
       For details, see `AssetUpdateVo Struct </docs/api/en/2.1.0/asset/update_asset.html#assetupdate-struct-assetupdate>`_


### AssetUpdateVo Struct <assetupdate>

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
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - name
     - Optional
     - StringI18n
     - Specify the asset's name in its respective locale's language. For more details on the structure and locales supported, see  `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - description
     - Optional
     - String
     - The asset description.
   * - attributes
     - 
      + if ``isPatchUpdate`` is false, this is mandatory
      + if ``isPatchUpdate`` is true, this is optional
     - Map
     - Attributes of the model which the asset belongs to.
       The Key is the attribute ID, which is of String type. The Value type depends on the attribute defined in the model. For details, see `attributes representation </docs/api/en/2.1.0/api_faqs.html#attributes-representation>`_
   * - timezone
     - Optional
     - String
     - + The timezone where the asset is located. 
       + Use the "+08:00" format for time zones that do not support Daylight Saving Time (DST). 
       + Use the "Asia/Shanghai" format for time zones that support DST. 
       For details, see `Timezone representation </docs/api/en/2.1.0/api_faqs.html#timezone-representation>`_
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tag </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_



## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 12958
     - Update failed due to asset attribute verification failure


## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId=yourOrgId&isPatchUpdate=true
method: POST 
requestBody:
{
  "asset": {
    "assetId": "Instance_cshan_001",
    "name": {
        "defaultValue": "daniu",
        "i18nValue": {
          "en_US": "English name ",
          "zh_CN": "Chinese name"
        }
    },
    "description": "hahdesc",
    "attributes": {},
    "modelId": "cshan111602",
    "timezone": "+08:00",
    "tags": {
        "year": "2000",
        "author": "cshan"
    }
  }
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "fa11232e-7e45-4176-a382-963c1240a27f"
}

```


## Java SDK Sample

```java
public class UpdateAsset {
    private static String accessKey = "yourAccessKey";
    private static String secretKey = "yourSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";

    //Make sure that an asset by this Asset ID and the fields to be updated exist.

    public static void main(String[] args) {
        UpdateAssetRequest request = new UpdateAssetRequest();
        request.setOrgId(orgId);

        AssetUpdateVo asset = new AssetUpdateVo();
        asset.setAssetId("XBOBqC1O");
        Map<String, Object> newAttrs = new HashMap<>();
        newAttrs.put("doubleTest",123.45);
        asset.setAttributes(newAttrs);

        request.setAsset(asset);
        request.setIsPatchUpdate(true);

        UpdateAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response);
    }
}
```
