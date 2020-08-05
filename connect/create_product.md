# Create Product

Create a product.

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
POST https://{apigw-address}/connect-service/v2.1/products?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|--------------------|----------|-----------|--------------|
| productDesc       | Optional     | String       | The product description. |
| biDirectionalAuth | Mandatory      | Boolean      | <ul><li>true = supports two-way authentication</li><li>false = does not support two-way authentication</li></ul>                                                  |
| modelId           | Mandatory      | String      | The model ID which the asset belongs to. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid)   |
| dataFormat        | Mandatory      | String      | Supports only two values: "Custom" and "Json". <ul><li>"Custom" represents the user-defined data type.</li><li>"Json" represents the JSON data type.</li></ul> |
| productName       | Mandatory      | StringI18n | The product name. For more details on the structure and locales supported, see [Internationalized name struct](/docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct). |
| productType       | Mandatory      | String      | Supports only two values: "Device" and "Gateway".<ul><li>"Device" represents common product types.</li><li>"Gateway" represents gateway types.</li></ul> |
|dynamicActivateEnabled|Optional|Boolean|<ul><li>true = able to activate dynamically</li><li>false (default) = not able to activate dynamically</li></ul> |
|productTags|Optional|Map|The tags of the product. For details, see [How to use tags](/docs/api/en/2.1.0/api_faqs.html#how-to-use-tag).|



## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| String          | The key of the created product.    |


## Error Codes

| Code|Description |
|-----|---------------------|
| 11699| The ``modelId`` does not exist.              |

## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/products?action=create&orgId=yourOrgId
method: POST
requestBody:
{
	"productDesc":"openapi_sdk_create_test",
	"biDirectionalAuth":false,
	"modelId":"AlterTest0615",
	"dataFormat":"Custom",
	"productName":{
		"defaultValue":"AlterTest0615_Product",
		"i18nValue":{}
	},
	"productType":"Device",
	"dynamicActivateEnabled":"false",
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
import com.envisioniot.enos.connect_service.v2_1.product.CreateProductRequest;
import com.envisioniot.enos.connect_service.v2_1.product.CreateProductResponse;

public class CreateProduct {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourSeverUrl";

        String orgId = "yourOrgId";
        CreateProductRequest request = new CreateProductRequest();
        request.setOrgId(orgId);
        StringI18n productName = new StringI18n("yourProductName");
        request.setProductName(productName);
        request.setProductDesc("yourProductDesc");
        request.setBiDirectionalAuth(false);
        request.setDataFormat("Custom");
        request.setProductType("Device");
        request.setModelId("yourModelId");
        CreateProductResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, CreateProductResponse.class);
    }
}
```
