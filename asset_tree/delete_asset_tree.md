# Delete Asset Tree

Delete an asset tree.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset Tree Management
     - Full Access

## Prerequisite

Ensure that there are no child nodes under the asset tree before deleting.

## Request Format

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=delete

```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | Mandatory    | String    | The asset tree ID. [How to get treeId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |



## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 17404
     - TreeId is not exist
     - The tree ID does not exist.
   * - 17800
     - Query it has sub nodes when delete node
     - Nodes with child nodes cannot be deleted.
   * - 99400
     - Invalid arguments
     - The request parameter is invalid. Check the request parameters.
   * - 99500
     - System error
     - Internal server error. Contact EnOS support.




## Samples

### Request Sample

```
url: https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=delete&orgId=yourOrgId&treeId=H4yVDl2U
method: POST 
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
  "data": null
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.asset_tree_service;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.api.common.constant.request.Projection;
import com.envisioniot.enos.asset_tree_service.v2_1.*;
import com.envisioniot.enos.asset_tree_service.vo.*;
import org.junit.Test;
import java.util.HashMap;
import java.util.Map;

public class AssetTreeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";

    @Test
    public void testDeleteTree() {
        DeleteTreeRequest request = new DeleteTreeRequest();
        request.setOrgId(OrgId);
        request.setTreeId("yourTreeId");
        DeleteTreeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, DeleteTreeResponse.class);
    }
}
```