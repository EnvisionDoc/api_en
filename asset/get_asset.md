# Get Asset



Get asset data by asset id.

## Request format

```
https://{apigw-address}/asset-service/v2.1/assets?action=get
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| assetId       | Query            | true    | String    | Asset ID. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |


## Response parameters

| Name | Data Type | Description |
|------|------------|-----------|-------------|
| data    |asset structure | Asset. See [Asset Structure](/docs/api/en/latest/asset/get_asset.html#id3).     |


### Asset Structure

| Name | Data Type | Description |
|-------|---------|---------------------------|
| assetId |  String | Asset ID|
| orgId      | String    | Organization ID which the asset belongs to|
| name | StringI18n |Name of each language for this asset|
| description   | String | Asset description|
|attributes   |Map  |Attributes of the model which the asset belongs to. <br>`Key` is the attribute id, which is of String type. The value type depends on the definition of this attribute in the model|
|timezone  |  String  |Timezone|
|modelId|String|Model ID which the asset belongs to|
|modelIdPath|String|Model inheritance path. <br>E.g.: /Turbine/Double_Feed_Turbine|
|tags|Map<br>(Key is of String type, and the value is of String type)|User-customized tags|


## Error codes

See [Public Return Code](/docs/api/en/latest/overview.html#id8).



## Sample 1

### Request sample

```
GET
https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=1c499110e8800000&assetId=TZ8AOlJU

```

### Return sample

```json
{
  "msg": "OK",
  "code": 0,
  "data": {
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
    "timezone": "+00:00",
    "name": {
      "i18nValue": {
        "en_US": "English name ",
        "zh_CN": "Chinese name"
                   }
      "defaultValue": "venus!"
            },
    "attributes": {
      "system": "Solar System"
                  },
    "modelIdPath": "/planet",
    "orgId": "o15444172373271",
    "desc": null,
    "tags": {}
           },
  "requestId": "9a5cfbac-b2f8-4a37-b38d-8bccdd77d073"
}
```


## Java SDK invocation sample

```java
public class GetAsset {
    private static String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        GetAssetRequest request = new GetAssetRequest();
        request.setOrgId(orgId);
        request.setAssetId("XBOBqC1O");

        GetAssetResponse response = Poseidon.config(PConfig.init().appKey(appKey)
                .appSecret(appSecret).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getCode());
    }
}
```
