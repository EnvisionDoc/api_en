# Update Product

Update a product.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.1/products?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| productKey         | Query            | Mandatory     | String    | The product key.|


## Request Parameters (Body)

| Name            | Mandatory/Optional | Data Type | Description |
|-------------------|----------|-----------|--------------|
| productDesc       | Optional     | String       | The product description.     |
| biDirectionalAuth | Mandatory      | Boolean      | <ul><li>true = supports two-way authentication</li><li>false = does not support two-way authentication</li></ul>                                                  |
| dynamicActivateEnabled           | Optional      | Boolean      | <ul><li>true = able to activate dynamically</li><li>false (default) = not able to activate dynamically</li></ul>|
| productName       | Mandatory      | StringI18n | The product name. For more details on the structure and locales supported, see For the structure, see [Internationalized name struct>>](/docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct)                                                           |
|productTags|Optional|Map| The tags of the product. For details, see [How to use tag>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag) |



## Response Parameters

| Name | Data Type | Description |
|-------------|---------------|------------|
| data | String      | The key of the updated product.     |

<!--
## Error Codes

| Code|  Description |
|------|-------------|
| 11651 | The ``productkey`` does not exist.              |
-->


## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/products?action=update&orgId=yourOrgId&productKey=yourProductKey
method: POST
requestBody:
{
	"productDesc":"test_sdk_update",
	"biDirectionalAuth":true,
	"dynamicActivateEnabled":true,
	"productName": {
		"defaultValue":"AlterTest0615_Product",
		"i18nValue":{
                "en_US":"AlterTest0615_Product",
                "zh_CN":"产品"
            }
	},
	"productTags": {
		"key1": "v1"
	}
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"522d0269-445d-4f13-be04-1424e0e2893e",
	"data":"2zp6A70r"
}
```

### Java SDK调用示例

```java
package com.envisioniot.enos.api.sample.connect_service.product;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.common.StringI18n;
import com.envisioniot.enos.connect_service.v2_1.product.UpdateProductRequset;
import com.envisioniot.enos.connect_service.v2_1.product.UpdateProductResponse;

public class UpdateProduct {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";
        String orgId = "yourOrgId";
        UpdateProductRequset request = new UpdateProductRequset();
        request.setOrgId(orgId);
        request.setProductKey("yourProductKey");
        StringI18n productName = new StringI18n("yourProductName");
        request.setProductName(productName);
        request.setBiDirectionalAuth(true);
        request.setDynamicActivateEnabled(true);

        UpdateProductResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, UpdateProductResponse.class);
    }
}
```
