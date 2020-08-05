# Link Asset to Asset Tree

Link an existing asset to an asset tree. The asset to be linked can be a device asset or a non-device (logical) asset. 

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=associateAsset
```

## Request Parameters (URI)

.. note:: Use one of the following methods to link an asset:

   - Include the ``assetId`` in the request 
   - Include both ``productKey`` and ``deviceKey`` in the request 


.. list-table::
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
   * - treeId
     - Query
     - Mandatory
     - String
     - The asset tree ID. `How to get treeID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree>`_
   * - parentAssetId
     - Query
     - Mandatory
     - String
     - The asset ID of the parent node of the asset to be linked.
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey``.
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey``.



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - The ID of the asset that has been successfully linked.


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
   * - 17752
     - Parent assetId is not existed in the tree
     - The parent asset does not exist in this Tree
   * - 17558
     - AssetId is existed in the tree
     - Asset ID already exists in the tree.
   * - 17762
     - The tree is locked
     - The asset tree cannot be modified/deleted for the time being as someone is currently accessing the asset tree. Please try again later.
   * - 17770
     - Exceeding the layer limit(7)
     - The tree exceeds the maximum number of layers (7 layers).
   * - 99400
     - Invalid arguments
     - The request parameter is invalid. Check the request parameters.
   * - 99500
     - System error
     - Internal server error. Contact EnOS support.



## Samples

### Request Sample

```
url: https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=associateAsset&orgId=yourOrgId&treeId=yourTreeId&parentAssetId=yourAssetId&productKey=yourProductKey&deviceKey=yourDeviceKey
method: POST 
```

### Return Sample

```json
{
    "code": 0,
    "msg": "ok",
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
    "data": "cRUdS7sJ"
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.asset_tree_service;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.asset_tree_service.v2_1.AssociateAssetNodeRequest;
import com.envisioniot.enos.asset_tree_service.v2_1.AssociateAssetNodeResponse;
import org.junit.Test;

public class AssociateAssetNodeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";

    @Test
    public void testAssociateAssetNode() {
        AssociateAssetNodeRequest request = new AssociateAssetNodeRequest();
        request.setOrgId(OrgId);
        request.setTreeId("yourTreeId");
        request.setParentAssetId("yourParentAssetId");
        request.setAssetId("yourAssetId");
        AssociateAssetNodeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, AssociateAssetNodeResponse.class);
    }
}
```