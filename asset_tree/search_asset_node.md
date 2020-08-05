# Search Asset Node

Search for assets based on the search criteria.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset Tree Management
     - Read

## Request Format

```json
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset
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
     - The conditions used for the search. The fields that are supported for query include: ``assetIds``, ``modelIds``, ``rootModelIds``, ``name``, ``attributes``, ``tags``, ``treeId``, ``productKey`` and ``deviceKey``.

       + ``assetIds``, ``modelIds``, and ``rootModelIds``: support arithmetic operators "=" and "in"
       + ``productKey`` and ``deviceKey``: supports arithmetic operator "=" and fuzzy inquiry (like)
       + ``createTime`` ：support =, <=, >= 
       + ``tags.*`` : supports fuzzy inquiry (like) and exists
       + ``name``: supports fuzzy inquiry of specified language:

         * ``name like 'xxx'``: fuzzy inquiry of default name, Chinese name, and English name
         * ``name.default like 'xxx'``: fuzzy inquiry of default name
         * ``name.zh_CN like 'xxx'``: fuzzy inquiry of Chinese name, if no Chinese name, fuzzy inquiry of default name
         * ``name.en_US like 'xxx'``: fuzzy inquiry of English name, if no English name, fuzzy inquiry of default name

       `How to use expression </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`_

   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. If not specified, only the first page with 100 records will be returned. The maximum records per page is 1000. **Note:** Does not support ``sorters`` struct. For more details, see `Pagination Request Struct </docs/api/en/2.1.0/overview.html#pagination-request-struct>`_
   * - projection
     - Optional
     - Projection Struct
     - Enables you to crop the data result set returned in the request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see `How does projection crop the result set? </docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set>`_



## Response Parameters


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Asset Struct Array
     - A list of the assets

## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 99400
     - Invalid arguments
     - The request parameter is invalid. Check the request parameters.
   * - 99500
     - System error
     - Internal server error. Contact EnOS support.



## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchAsset&orgId=yourOrgId
method: POST 
requestBody:
{
"projection": ["attributes", "assetId", "name"]
}
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "cf08e75c-325a-429f-bdb9-ec5d6a1250d7",
    "pagination": {
       "pageNo": 1,
       "pageSize": 10,
       "totalSzie": 10,
       "sortedBy": null
    },
    "data": [{
       "assetId": "f1Y6KiOr",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "WHIFQDEZ",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "TdqGOisO",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "T9VewFFA",
       "name": {
           "i18nValue": {},
           "defaultValue": "venus"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "NU3EbpXK",
       "name": {
           "i18nValue": {},
           "defaultValue": "1559140566137"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "9AE1XYBl",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }, {
       "assetId": "ZPuCIbDw",
       "name": {
           "i18nValue": {},
           "defaultValue": "earth"
       },
       "attributes": {
           "starsystem": "Solar System",
           "de001": 123
       }
    }]
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.asset_tree_service;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Projection;
import com.envisioniot.enos.asset_tree_service.v2_1.*;
import com.envisioniot.enos.asset_tree_service.vo.AssetSearchVo;
import com.envisioniot.enos.asset_tree_service.vo.RelatedAssetSearchVo;
import org.junit.Test;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class SearchNodeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";

    @Test
    public void testSearchAssetNode() {
        SearchAssetNodeRequest request = new SearchAssetNodeRequest();
        request.setOrgId(OrgId);
        request.setExpression("name.default like'assetDefaultName'");
        Projection projection = new Projection();
        projection.addAll(Arrays.asList("attributes", "assetId", "name"));
        request.setProjection(projection);
        SearchAssetNodeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl).getResponse(request, SearchAssetNodeResponse.class);
    }
}
```