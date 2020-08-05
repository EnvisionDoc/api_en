# Search Product

Search for products based on the search criteria.

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
POST https://{apigw-address}/connect-service/v2.1/products?action=search
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


## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - expression
     - Optional
     - String
     - The query expression, which supports sql-like query. The fields that are supported for query include: ``productKey``, ``modelId``, ``productTags`` and ``productName`` . The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or".

         + ``productKey`` : supports arithmetic operators "=" and "in"
         + ``modelId`` : supports arithmetic operators "=" and "in"
         + ``productTags``: supports arithmetic operators "=", "exists", and "not exists"
         + ``productName`` supports fuzzy inquiry of specified language:

            * ``productName like 'xxx'``: fuzzy inquiry of default name, Chinese name, and English name
            * ``productName.default like 'xxx'``: fuzzy inquiry of default name
            * ``productName.zh_CN like 'xxx'``: fuzzy inquiry of Chinese name, if no Chinese name, fuzzy inquiry of default name
            * ``productName.en_US like 'xxx'``: fuzzy inquiry of English name, if no English name, fuzzy inquiry of default name

       `How to use expression>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`_
   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. When not specified, 10 entries are displayed per page by default. ``sorters`` is not supported to sort the response. The maximum records per page is 200. For more details, see `Pagination Request Struct>> </docs/api/en/2.1.0/overview.html#pagination-request-struct>`_



## Response Parameters


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of Product Structs
     - A list of the products returned. For details of a Product Struct, see `Product Struct </docs/api/en/2.1.0/connect/get_product.html#product-struct-productstruc>`_



## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/products?action=search&orgId=yourOrgId
method: POST
requestBody:
{
	"expression":"modelId=\"AlterTest0615\"",
	"pagination":{
		"pageNo":1,
		"pageSize":5
	}
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"a82752bb-9eb0-4cd5-b0c6-0c1aeb35f6d2",
	"data":[
		{
			"orgId":"yourOrgId",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"openapi_sdk_8",
				"i18nValue":{}
			},
			"productSecret":"yourProductSecret",
			"productDesc":"test_sdk_update",
			"productType":"Device",
			"dataFormat":"Custom",
			"productTags":{},
			"modelId":"AlterTest0615",
			"dynamicActiveEnabled":false,
			"biDirectionalAuth":true,
      "createBy": null,
      "createTime": null,
      "updateBy": null,
      "updateTime": 1589767858113
		},
		{
			"orgId":"yourOrgId",
			"productKey":"yourProductKey",
			"productName":{
				"defaultValue":"AlterTest0615_Product",
				"i18nValue":{}
			},
			"productSecret":"yourProductSecret",
			"productDesc":"",
			"productType":"Device",
			"dataFormat":"Json",
			"productTags":{},
			"modelId":"AlterTest0615",
			"dynamicActiveEnabled":false,
			"biDirectionalAuth":false,
      "createBy": null,
      "createTime": null,
      "updateBy": null,
      "updateTime": 1589767858113,
      "defaultValidDay":null,
      "maxValidDay":null
		}
	],
	"pagination":{
		"sortedBy":null,
		"pageNo":1,
		"pageSize":5,
		"totalSize":2
	}
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.product;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.api.common.constant.request.Projection;
import com.envisioniot.enos.connect_service.v2_1.product.SearchProductRequest;
import com.envisioniot.enos.connect_service.v2_1.product.SearchProductResponse;

public class SearchProduct {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        SearchProductRequest request = new SearchProductRequest();
        request.setOrgId(orgId);
        request.setExpression("modelId='yourModelId'"); // or productKey = 'yourProductKey'
        request.setPagination(new Pagination(5, 1, null));
        Projection projection = new Projection();
        projection.add("productName");
        request.setProjection(projection);
        SearchProductResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, SearchProductResponse.class);
    }
}

```

