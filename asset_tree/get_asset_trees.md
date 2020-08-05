# Get Asset Trees

Get the details of one or multiple asset trees based on a set of ``assetIds``. If the `assetId` is not in the tree, no Key will be returned in `data`.

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=getAssetTree
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |

## Request Parameters (Body)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| assetIds         | Query            | Mandatory     | String Array   | Provide multiple asset IDs if you want to query multiple assets. The array can support a max of 100 IDs. Applicable to both device and non-device (logical) assets.  [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid)   |
| projection         | Query            | Optional    | Projection struct   | Enables you to crop the data result set returned in the interface request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see [How does projection crop the result set](/docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set)|


## Response Parameters

| Name | Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| data| Map  | A list of assets and the asset trees they are in. The Key is ``assetId`` and the Value is the assetTree struct array. For more details, see [AssetTree Struct](/docs/api/en/2.1.0/asset_tree/get_asset_trees.html#assettree-struct-assettree) |


### AssetTree Struct <assettree>

| Name | Data Type | Description |
|-------|-------|---------------------------|
| treeId  |  String | The asset tree ID. |
|tags|Map|User-defined tags. (The Key and Value are of String type.)|
|asset|Asset Struct|The details of an asset.|


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
url: https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=getAssetTree&orgId=yourOrgId
method: POST 
requestBody: 
{
  "action": "getAssetTree",
  "assetIds": ["BtsYmF2r", "qf1vsBQW"]
}
```

### Return Sample

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "82248518-6da4-49d2-8d07-cf7a0ff55b60",
 "data": {
 "BtsYmF2r" : [{
   "treeId" : "yourTreeId",
   "tags" : { },
   "asset": {
    "modelId": "yourModelId",
    "assetId": "yourAssetId",
    "timezone": "+08:00",
    "name": {
     "i18nValue": {
      "en_US": "zmTree604111zzz"
     },
     "defaultValue": "zmTree604"
    },
    "description": "",
    "attributes": {},
    "inValid": false,
    "label": "1",
    "modelIdPath": "/NULLMODEL",
    "tags": {}
   }}
 ]
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
import com.envisioniot.enos.asset_tree_service.vo.RelatedAssetSearchVo;
import org.junit.Test;
import java.util.Arrays;

public class SearchNodeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";

    @Test
    public void testSearchTreeByAssetId() throws Exception {
        SearchAssetTreeByAssetIdsRequest request = new SearchAssetTreeByAssetIdsRequest();
        request.setOrgId(OrgId);
        request.setAssetIds(Arrays.asList("assetId1", "assetId2"));
        SearchAssetTreeByAssetIdsResponse response =
            Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug()).url(ServerUrl)
            .getResponse(request, SearchAssetTreeByAssetIdsResponse.class);
        System.out.println(response.getData());
    }
}
```