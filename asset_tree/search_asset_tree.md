# Search Asset Tree

Search for asset trees based on the query criterion.

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search
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
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - expression
     - Optional
     - String
     - The conditions used for the search. The use of `tags` , arithmetic operator "=" and "exists" are supported. `How to use expression>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-expression>`_
   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. If not specified, only the first page with 100 records will be returned. The maximum records per page is 1000. ``sorters`` is not support to sort the response. For more details, see `Pagination Request Struct>> </docs/api/en/2.1.0/overview.html#pagination-request-struct>`_
   * - projection
     - Optional 
     - Projection struct
     - Enables you to crop the data result set returned in the interface request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see `How does projection crop the result set>> </docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set>`_




## Response Parameters


.. list-table:: Response parameters
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of AssetTree Structs
     - For the definition of an AssetTree Struct, see the table below.


.. list-table:: AssetTree Struct
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - treeId
     - String
     - The asset tree ID.
   * - name
     - StringI18n
     - The asset tree name. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - tags
     - Tag struct
     - The user-defined tags.
   * - asset
     - Asset Struct
     - The details of an asset. For more information, see `Asset struct>> </docs/api/en/2.1.0/asset_tree/get_asset_tree.html#asset-assetstruct>`_


## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=search&orgId=yourOrgId
method: POST 
requestBody: 
{
  "expression":"tags.k1 ='v1' ",
  "pagination": {
    "pageNo": 1,
    "pageSize": 10
  },
  "projection": ["asset"]
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"82248518-6da4-49d2-8d07-cf7a0ff55b60",
	"data":[
		{
      "asset":{
			"modelId":"yourModelId",
			"assetId":"yourAssetId",
			"timezone":"+08:00",
			"name":{
				"i18nValue":{
					"en_US":"zmTree604111zzz"
				},
				"defaultValue":"zmTree604"
			},
			"description":"",
			"attributes":{

			},
			"inValid":false,
			"label":"1",
			"modelIdPath":"/NULLMODEL",
			"tags":{

			}
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

## Java SDK Sample

```java
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.api.common.constant.request.Projection;
import com.envisioniot.enos.asset_tree_service.v2_1.*;
import com.envisioniot.enos.asset_tree_service.vo.AssetCreateVo;
import com.envisioniot.enos.asset_tree_service.vo.I18nVo;
import com.envisioniot.enos.asset_tree_service.vo.TreeCreateVo;
import com.envisioniot.enos.asset_tree_service.vo.TreeUpdateVo;
import org.junit.Test;
import java.util.HashMap;
import java.util.Map;

public class AssetTreeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";


    @Test
    public void testSearchTree() {
        SearchAssetTreeRequest request = new SearchAssetTreeRequest();
        request.setOrgId(OrgId);
        request.setExpression("tags.k1 ='v1'");
        Pagination pagination = new Pagination(3, 1, null);
        Projection projection = new Projection();
        projection.add("asset");
        request.setPagination(pagination);
        request.setProjection(projection);
        SearchAssetTreeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, SearchAssetTreeResponse.class);
    }
}
```
