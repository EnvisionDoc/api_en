# Search Related Asset Node

Search for assets under the specified asset tree based on the relationship with a known asset.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset Tree Management
     - Read

## Request Format

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchRelatedAsset
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | Mandatory    | String    | The asset tree ID. [How to get treeId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| filter| Optional         |   Filter Struct       | The query criteria. The relationship between all the queried criteria uses the "AND" logical operator, i.e. all relationships between all the queried criteria must be true for data to be returned. <br>Only one out of the 4 relational query criteria (``isParentOfAssetId``, ``isChildOfAssetId``, ``isAncestorOfAssetId``, and ``isDescendantOfAssetId``) is allowed. For more details, see [Filter Struct](/docs/api/en/2.1.0/asset_tree/search_related_asset_node.html#filter-struct-filterstruc)   |
| pagination| Optional         |  Pagination Request Struct | Lists the paging requirements in a request. If not specified, only the first page with 100 records will be returned. The maximum records per page is 1000. ``sorters`` is not supported to sort the response. For more details, see [Pagination Request Struct](/docs/api/en/2.1.0/overview.html#pagination-request-struct)                               |
| projection| Optional         | String Array          | Enables you to crop the data result set returned in the interface request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see [How does projection crop the result set>>](/docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set)|


### Filter Struct <filterstruc>

| Name | Mandatory/Optional | Data Type | Description |
|-----------|---------|--------|-----------------------|
| assetIds          | Optional              | String Array    | The asset ID. Provide multiple asset IDs if you want to query multiple assets.  [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| nameLike          | Optional          | I18nSearchVo Struct     | The asset Name. Supports fuzzy query. For more details, see [I18nSearchVo Struct](/docs/api/en/2.1.0/asset_tree/search_related_asset_node.html#i18nsearchvo-struct-i18n)|
| modelIds        | Optional         | String Array   | The model ID. Provide multiple root model IDs if you want to query multiple models.  [How to get modelID>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-model-id-modelid-modelid)|
| rootModelIds      | Optional        | String Array  | The model ID of the root node. Provide multiple root model IDs if you want to query multiple root nodes. |
| isParentOfAssetId     | Optional     | String    | The asset to be queried is the immediate parent node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)  |
| isChildOfAssetId      | Optional    | String    | The asset to be queried is the immediate child node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)  |
| isAncestorOfAssetId      | Optional    | String     | The asset to be queried is the ancestor node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)  |
| isDescendantOfAssetId    | Optional   | String   | The asset to be queried is the descendant node of the specified asset, and its value is the asset ID of the specified asset. <br>[How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)  |



### I18nSearchVo Struct <i18n>


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - locale
     - Mandatory
     - String
     - The locale language, currently supporting:

       + default
       + zh_CN
       + en_US

   * - value
     - Mandatory
     - String
     - The corresponding asset name for the locale.



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of Asset Structs
     - For the definition of an asset struct, see `Asset Struct </docs/api/en/2.1.0/asset_tree/get_asset_tree.html#asset-assetstruct>`_

   * - Name
     - Data Type
     - Description
   * - data
     - Array of Asset Structs
     - For the definition of an asset struct, see `Asset Struct </docs/api/en/2.1.0/asset_tree/get_asset_tree.html#asset-assetstruc>`__


## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=searchRelatedAsset&treeId=k6wweMTP&orgId=yourOrgId
method: POST 
requestBody: 
{
  "filter": {
    "isChildOfAssetId": "4R6PbfVj"
  },
  "pagination":{
    "pageNo":1,
    "pageSize":10
  },
  "action": "searchRelatedAsset",
  "projection": ["attributes", "assetId", "name"]
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"153ad7a2-2ec1-41b0-b750-e4ea2ce2786c",
	"data":[
		{
			"assetId":"8byS3cuc",
			"name":{
				"i18nValue":{

				},
				"defaultValue":"ycmdevice_1"
			},
			"attributes":{

			}
		},
		{
			"assetId":"Fq5M1Y6E",
			"name":{
				"i18nValue":{

				},
				"defaultValue":"ycmdevice_3"
			},
			"attributes":{

			}
		},
		{
			"assetId":"nPQUW0Nr",
			"name":{
				"i18nValue":{
					"en_US":"Rebecca_testSiteAPI3"
				},
				"defaultValue":"Rebecca_testSiteAPI3"
			},
			"attributes":{

			}
		},
		{
			"assetId":"oLrrH1uz",
			"name":{
				"i18nValue":{

				},
				"defaultValue":"Rebecca_Service1"
			},
			"attributes":{

			}
		},
		{
			"assetId":"vuT6x3Xl",
			"name":{
				"i18nValue":{

				},
				"defaultValue":"ycmdevice_2"
			},
			"attributes":{

			}
		}
	],
	"pagination":{
		"pageNo":1,
		"pageSize":10,
		"totalSize":10,
		"sortedBy":null
	}
}
```

### Java SDK Sample

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
    public void testSearchRelatedAssetNode() {
        SearchRelatedAssetNodeRequest request = new SearchRelatedAssetNodeRequest();
        request.setOrgId(OrgId);
        request.setTreeId("yourTreeId");
        RelatedAssetSearchVo filter = new RelatedAssetSearchVo();
        filter.setIsChildOfAssetId("yourAssetId");
        Projection onep = new Projection();
        onep.addAll(Arrays.asList("attributes", "assetId", "name"));
        request.setFilter(filter);
        request.setProjection(onep);
        request.setFilter(filter);
        SearchRelatedAssetNodeResponse response =
            Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug()).url(ServerUrl)
            .getResponse(request, SearchRelatedAssetNodeResponse.class);
    }
}
```