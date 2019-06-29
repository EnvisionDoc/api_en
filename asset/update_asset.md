# Update Asset

*Note: This documentation is in the progress of translation. Thanks for your visit!*

全量或部分更新资产信息。

## 请求格式

```
https://{apigw-address}/asset-service/v2.1/assets?action=update
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| isPatchUpdate       | Query            | false    | Boolean    | 是否是局部更新，默认为true               |
                                                                  

## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|------------------|----------|-----------|-------------|
| asset     | true  |`AssetUpdate`结构体          | 用于资产更新，结构请见[AssetUpdate结构体](/docs/api/en/latest/asset/update_asset.html#id2)。<br>在`isPatchUpdate`为true时，只更新`asset`参数中指定的字段；在`isPatchUpdate`为false时，将完全覆盖`asset`各字段值，即未指定值的字段将被置空       |


### AssetUpdate结构体

| 名称  | 是否必须| 数据类型      | 描述               |
|-------|--------|--------|---------------------------|
| assetId |   true   | String | 资产ID。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)|
| name | false| StringI18n |该资产的各语言名称。结构请见[国际化名称结构体](/docs/api/en/latest/api_faqs.html#id3) |
| description | false     | String | 资产描述|
|attributes  | false<br>(如果`isPatchUpdate`为false，`attributes`必填) |Map  |资产所属的模型属性。<br>`Key`为属性id，String类型。Value的类型取决于模型中这个属性的定义。详情请见 [attributes的表示方法](/docs/api/en/latest/api_faqs.html#attributes) |
|timezone  |  false    |String  |时区。详情请见[时区表示方法](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#id4) |
|tags|false|Map<br>（Key为String, Value为String）|用户自定义标签，详情请见[标签的作用与表示方法](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#id6) |


## 错误码

| 代码  | 描述               |
|-----------------|--------------|
| 11958  | 由于资产属性校验失败导致更新失败     |



## 示例 1

### 请求示例

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

### 返回示例

```json
{
  "code": 0,
  "msg": "OK"，
  "requestId": "fa11232e-7e45-4176-a382-963c1240a27f"
}

```


## Java SDK调用示例

```java
public class UpdateAsset {
    private static String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
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

        UpdateAssetResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response);
    }
}
```
