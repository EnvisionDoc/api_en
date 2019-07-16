# Update Asset



Fully or partially update asset information.

## Request Format

```
https://{apigw-address}/asset-service/v2.1/assets?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| isPatchUpdate       | Query            | false    | Boolean    | Whether to perform partial update. Set as true by default               |
                                                                  

## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|------------------|----------|-----------|-------------|
| asset     | true  |`AssetUpdate` structure          | Used for asset update. For details about the structure, see [AssetUpdate Structure](/docs/api/en/latest/asset/update_asset.html#id2). <br>When `isPatchUpdate` is true, only the fields specified in the `asset` parameter are updated; when `isPatchUpdate` is false, the field value of `asset` will be completely covered, i.e. the fields with an unspecified value will be left blank.


### AssetUpdate Structure

| Name            | Required or Not | Data Type | Description |
|-------|--------|--------|---------------------------|
| assetId |   true   | String | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| name | false| StringI18n |Name of each language for this asset. For the structure, see [Internationalized name structure](/docs/api/en/latest/api_faqs.html#internationalized-name-structure)
| description | false     | String | Asset description|
|attributes  | false<br> (If `isPatchUpdate` is false, the `attributes` is mandatory) |Map  |Attributes of the model which the asset belongs to. <br>`Key` is the attribute ID, which is of String type. The value type depends on the attribute definition in the model. For details, see [attributes representation](/docs/api/en/latest/api_faqs.html#attributes-representation) |
|timezone  |  false    |String  |Timezone. For details, see [Timezone representation](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#timezone-representation) |
|modelId|false (if `isPatchUpdate` is false, `modelId` is required)|String|Model ID|
|tags|false|Map<br> (Key is of String type and the value is of String type)|User-customized tags. For details, see [How to use tag](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#how-to-use-tag) |


## Error Codes

| Code | Description    |
|-----------------|--------------|
| 11958  | Update failed due to asset attribute verification failure     |



## Sample 1

### Request Sample

```json
POST https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId=o15475450989191
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
  "msg": "OK"，
  "requestId": "fa11232e-7e45-4176-a382-963c1240a27f"
}

```


## Java SDK Sample

```java
public class UpdateAsset {
    private static String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";

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
