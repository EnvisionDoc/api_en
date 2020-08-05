# Get Product

Get the details of a product via its `productKey`.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Read

## Request Format

```
GET https://{apigw-address}/connect-service/v2.1/products?action=get
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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - productKey
     - Query
     - Mandatory
     - String
     - The product key.

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Product struct
     - The details of the product. For more information, see `Product Struct>> </docs/api/en/2.1.0/connect/get_product.html#product-struct-productstruct>`_



### Product Struct <productstruct>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - orgId
     - String
     - The organization ID which the asset belongs to.
   * - productKey
     - String
     - The product key.
   * - productName
     - StringI18n
     - The product name.
   * - productSecret
     - String
     - The product private key.
   * - productDesc
     - String
     - The product description.
   * - productType
     - String
     - The product type. ``Device`` stands for common product types, while ``Gateway`` stands for gateway types.
   * - dataFormat
     - String
     - + ``Custom`` represents the user-defined data type.
       + ``Json`` represents the json data type.
   * - productTags
     - Map
     - The product tags.  (The Key and Value are of String type.)
   * - modelId
     - String
     - The model ID which the asset belongs to.
   * - dynamicActiveEnabled
     - Boolean
     - + `true` = able to activate dynamically
       + `false` = not able to activate dynamically
   * - biDirectionalAuth
     - Boolean
     - + ``true`` = supports two-way authentication
       + ``false`` = does not support two-way authentication
   * - createTime
     - Long
     - The time the product is created.
   * - createBy
     - String
     - The name of the person who created the product.
   * - updateTime
     - Long
     - The time when the product was last updated. This will have the same value as ``createTime`` if there are no updates made after the product was created.
   * - updateBy
     - String
     - The name of the person who updated the product.



## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Data Type
     - Description
   * - 11611
     - Not found
     - The ``productKey`` does not exist.





## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/products?action=get&orgId=yourOrgId&productKey=yourProductKey
method: GET
```

### Return Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"864291ce-ca48-457f-a790-a3415c0169ad",
    "data":{
        "orgId":"yourOrgId",
        "productKey":"yourProductKey",
        "productName":{
            "defaultValue":"202cp",
            "i18nValue":{
                "en_US":"",
                "zh_CN":""
            }
        },
        "productSecret":"yourProductSecret",
        "productDesc":"",
        "productType":"Device",
        "dataFormat":"Json",
        "productTags":null,
        "modelId":"202model",
        "dynamicActivateEnabled":false,
        "biDirectionalAuth":false,
        "createBy":"DM001",
        "createTime":1582861255508,
        "updateBy":"DM001",
        "updateTime":1582861255508,
        "defaultValidDay":null,
        "maxValidDay":null
    }
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.product;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.product.GetProductRequest;
import com.envisioniot.enos.connect_service.v2_1.product.GetProductResponse;


public class GetProduct {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";
        
        String orgId = "yourOrgId";
        GetProductRequest request = new GetProductRequest();
        request.setOrgId(orgId);
        request.setProductKey("yourProductKey");
        GetProductResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, GetProductResponse.class);
    }
}
```