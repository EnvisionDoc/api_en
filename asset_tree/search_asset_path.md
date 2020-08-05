# Search Asset Path

Search for paths on the asset tree. A path is a complete path from a superior asset node to a subordinate asset node, which can contain intermediate asset nodes.

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-paths?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId          | Query            | Mandatory     | String    | The asset tree ID. [How to get treeID>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree) |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| pagination| Optional         |  Pagination Request Struct | Lists the paging requirements in an interface request. If not specified, only the first page with 100 records will be returned. The maximum records per page is 1000. ``sorters`` is not supported for sorting the response. For more details, see [Pagination Request Struct](/docs/api/en/2.1.0/overview.html#pagination-request-struct)  |
| from | Optional        | From-to Struct       | The starting point of the asset path. If not provided, it is the root node of the asset tree. For more details, see [From-to Struct](/docs/api/en/2.1.0/asset_tree/search_asset_path.html#from-to-struct-fromtostruc)                         |
| to            | Optional        | From-to Struct           | The ending point of the asset path. If not provided, it is the child node of the asset tree. For more details, see [From-to Struct](/docs/api/en/2.1.0/asset_tree/search_asset_path.html#from-to-struct-fromtostruc) |
| projection| Optional         | Projection struct         | Enables you to crop the data result set returned in the interface request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see [How does projection crop the result set](/docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set)|
| pathProjection| Optional        | String                | Accepts only 2 two types of values: "COMPLETE" (default) or "END_NODE_ONLY". <ul><li>"COMPLETE" means all the nodes of the returned path.</li><li>"END_NODE_ONLY" means only the start and end nodes of the returned path.</li></ul>  |


### From-to Struct <fromtostruc>

| Name | Mandatory/Optional | Data Type | Description |
|-----------|---------------|----|-----------------------|
| rootModelIds| Optional  | String Array         | The model ID of the root node. Provide multiple root model IDs if you want to query multiple root nodes. |
| modelIds   | Optional  | String Array         | The model ID. Provide multiple root model IDs if you want to query multiple Models. [How to get modelID>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-model-id-modelid-modelid)|
| assetIds        | Optional     | String Array        | The asset ID. Provide multiple asset IDs if you want to query multiple assets.  [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |



## Response Parameters

| Name | Data Type | Description |
|-----------|------------------|------------------|
| assets     | Map | The asset data on the path. The Key is of String type, and the Value is of ``Asset`` struct type. |
| assetPaths | String Array| If the `pathProjection` parameter is "COMPLETE", each String in the String Arrays is the ID of the asset from the start to end node on the path, with the length greater than or equals to 2. If the `pathProjection` parameter is "END_NODE_ONLY", each String in the String Arrays is the ID of the asset of the start and end node of the path, with the length fixed at 2.  |


### Asset Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - assetId
     - String
     - The asset ID.
   * - name
     - StringI18n
     - The name of the asset in all its respective locale's language.
   * - description
     - String
     - The asset description.
   * - attributes
     - Map
     - The attributes of the model which the asset belongs to. The Key is the attribute ID, which is of String type. The Value type depends on the attribute defined in the model.
   * - timezone
     - String
     - The timezone where the asset is located.
   * - modelId
     - String
     - The model ID.
   * - modelIdPath
     - String
     - The model ID path.
   * - tags
     - Tag struct
     - User-defined tags. (The Key and Value are of String type.)
   * - inValid
     - Boolean
     - Whether the node is valid or not.
   * - label
     - String
     - The tag of the asset.




## Sample 1

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-paths?action=search&treeId=yourTreeId&orgId=yourOrgId
method: POST 
requestBody: 
{
    "pagination":{
        "pageNo":1,
        "pageSize":10
    },
    "projection":[
        "assets.*.attributes",
        "assetPaths"
    ]
}
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "381ffc90-ee96-45a9-bbf4-8f82efed9823",
    "data": {
        "assets": {
            "rzjwQAHU": {
                "attributes": {
                    "starsystem": "sss",
                    "de001": 123
                }
            },
            "iQFjlwoH": {
                "attributes": {

                }
            },
            "sDx0Uk2Z": {
                "attributes": {

                }
            },
            "4uR3ZsqP": {
                "attributes": {

                }
            }
        },
        "assetPaths": [
            [
                "4uR3ZsqP",
                "rzjwQAHU",
                "sDx0Uk2Z"
            ],
            [
                "4uR3ZsqP",
                "iQFjlwoH"
            ]
        ]
    },
    "pagination": {
        "sortedBy": null,
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 2
    }
}
```

## Sample 2

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-paths?action=search&treeId=yourTreeId&orgId=yourOrgId
method: POST 
requestBody: 
{
    "pagination": {
        "pageNo": 1,
        "pageSize": 10
    },
    "from": {
        "modelIds": [
            "extend_model"
        ]
    },
    "to": {
        "assetIds": [
            "MkblvAJ5"
        ]
    }
}
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "94347fc1-4b3c-447b-b542-03fa68a1a88f",
    "data": {
        "assetPaths": [
            [
                "DWJdfX3D",
                "MkblvAJ5"
            ]
        ],
        "assets": {
            "DWJdfX3D": {
                "inValid": false,
                "assetId": "DWJdfX3D",
                "modelId": "extend_model",
                "modelIdPath": "/copy_model/extend_model",
                "name": {
                    "defaultValue": "hahha",
                    "i18nValue": {
                        "en_US": "hahha"
                    }
                },
                "timezone": "+09:00",
                "description": "eeeeee",
                "label": "1",
                "attributes": {
                    "invType": 1,
                    "capacity": 5.0
                },
                "tags": {

                }
            },
            "MkblvAJ5": {
                "inValid": false,
                "assetId": "MkblvAJ5",
                "modelId": "planet",
                "modelIdPath": "/planet",
                "name": {
                    "defaultValue": "lkkkkk",
                    "i18nValue": {
                        "en_US": "lkkkkk"
                    }
                },
                "timezone": "+08:00",
                "description": "huyyyyy",
                "label": "1",
                "attributes": {
                    "starsystem": "yyyy",
                    "de001": 123
                },
                "tags": {

                }
            }
        }
    },
    "pagination": {
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 1
    }
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.asset_tree_service;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.api.common.constant.request.Projection;
import com.envisioniot.enos.api.common.constant.request.Sorter;
import com.envisioniot.enos.asset_tree_service.v2_1.SearchAssetPathRequest;
import com.envisioniot.enos.asset_tree_service.v2_1.SearchAssetPathResponse;
import com.envisioniot.enos.asset_tree_service.vo.AssetTreePathSearchEndVo;
import org.junit.Test;
import java.util.ArrayList;
import java.util.Arrays;

public class SearchAssetNodePathTest {
    private static String ACCESSKEY = "yourAccessKey";
    private static String SECRETKEY = "yourSecretKey";
    private static String ORGID = "yourOrgId";
    private static String SERVERURL  = "yourServerUrl";
    private static String TREEID  = "yourTreeId";
    
    
    @Test
    public void testSearchAssetNodePath() {
        SearchAssetPathRequest request = new SearchAssetPathRequest();
        request.setOrgId(ORGID);
        request.setTreeId(TREEID);
        AssetTreePathSearchEndVo from = new AssetTreePathSearchEndVo();
        from.setAssetIds(Arrays.asList("assetId1","assetId2","assetId3","assetId4","assetId5","assetId6"));
        AssetTreePathSearchEndVo to = new AssetTreePathSearchEndVo();
        to.setRootModelIds(Arrays.asList("modelId1","modelId2","modelId3"));
        request.setFrom(from);
        request.setTo(to);
        Projection projection = new Projection();
        projection.add("assetPaths");
        projection.add("assets.*.attributes");
        request.setProjection(projection);
        Pagination page = new Pagination();
        page.setPageNo(1);
        page.setPageSize(100);
        page.setSorters(new ArrayList<Sorter>());
        request.setPagination(page);
        SearchAssetPathResponse response = Poseidon.config(PConfig.init().appKey(ACCESSKEY).appSecret(SECRETKEY).debug())
                .url(SERVERURL)
                .getResponse(request, SearchAssetPathResponse.class);
    }
}
```