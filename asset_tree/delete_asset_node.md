# Delete Asset Node

Remove an asset from an asset tree. The asset to be removed can be a device asset or a non-device (logical) asset.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset Tree Management
     - Full Access

## Request Format

```
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=delete
```

## Request Parameters (URI)

.. note:: Use one of the following methods to identify the Asset to be deleted. 

   - Include the ``assetId`` in the request (applicable for both device and logical assets)
   - Include both ``productKey`` and ``deviceKey`` in the request (applicable only for device asset)



| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the Asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| treeId        | Query            | Mandatory    | String    | The asset tree ID. [How to get the ID of an asset tree>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree)        |
| assetId  | Query            | Optional (See **Note** above)   | String    |  The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid)  |
| productKey  | Query            | Optional (See **Note** above)   | String    | The product key. To be used with ``deviceKey``.|
| deviceKey  | Query            | Optional  (See **Note** above)  | String    | The device key. To be used with ``productKey``. |


## Error Codes


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 17764
     - The root asset node cannot be deleted.
     - The root node cannot be deleted
   * - 17766
     - The noleaf asset node cannot be deleted.
     - Nodes with child nodes cannot be deleted.
   * - 17762
     - The tree is locked
     - The asset tree cannot be modified/deleted for the time being as someone is currently accessing the asset tree. Please try again later.
   * - 99400
     - Invalid arguments
     - The request parameter is invalid. Check the request parameters.
   * - 99500
     - System error
     - Internal server error. Contact EnOS support.







## Samples

### Request Sample

```
url: https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=delete&treeId=yourTreeId&orgId=yourOrgId
method: POST
```

### Return Sample

```json
{
  "code": 0,
  "msg": "ok",
  "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f" ,
  "data": null
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.asset_tree_service;

import com.envisioniot.enos.asset_tree_service.v2_1.DeleteAssetNodeRequest;
import com.envisioniot.enos.asset_tree_service.v2_1.DeleteAssetNodeResponse;
import org.junit.Test;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class DeleteAssetNodeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";

    @Test
    public void testRequestRemoteBeta() throws Exception {
        DeleteAssetNodeRequest request = new DeleteAssetNodeRequest();
        request.setOrgId(OrgId);
        request.setTreeId("yourTreeId");
        request.setAssetId("yourAssetId");
        DeleteAssetNodeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl).getResponse(request, DeleteAssetNodeResponse.class);
    }
}
```