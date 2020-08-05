# Delete Product
Delete a product. 

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Full Access

## Prerequisite

Ensure that there are no devices under the product before deleting.

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/products?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| productKey         | Query            | Mandatory     | String    | The product key.|




## Response Parameters

| Name | Data Type | Description |
|-------------|---------------------------|-----------------------------|
| data | String                           | The product key of the deleted product.       |


## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 99404|   Not found           | The `productKey` does not exist.              |
| 11619|   Existing Device Restrictions       |There are devices under the product to be deleted.   |

## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/products?action=delete&orgId=yourOrgId&productKey=yourProductKey
method: POST
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"ef6a7fbb-0834-45fb-b1d4-6bd2dc25796f",
	"data":"atC41UIe"
}

```

### Java SDK调用示例

```java
package com.envisioniot.enos.api.sample.connect_service.product;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.product.DeleteProductRequest;
import com.envisioniot.enos.connect_service.v2_1.product.DeleteProductResponse;

public class DeleteProduct {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourSeverUrl";
        String orgId = "yourOrgId";
        DeleteProductRequest request = new DeleteProductRequest();
        request.setOrgId(orgId);
        request.setProductKey("yourProductKey");
        DeleteProductResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, DeleteProductResponse.class);
    }
}
```
