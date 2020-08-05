# Create Asset Tree and Link an Asset

Create an asset tree and link an existing asset as the root node of the asset tree. The asset to be linked can be a device asset or a non-device (logical) asset. 

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset Tree Management
     - Full Access

## Request Format

```json
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=associate
```

## Request Parameters (URI)

.. note:: Use one of the following methods to identify the asset to be linked.

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
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey`` .
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey`` .


## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - tree
     - Optional
     - TreeCreateVo Struct
     - The details of the asset tree to be created. For more details, see `TreeCreateVo Struct </docs/api/en/2.1.0/asset_tree/create_asset_tree.html#treecreatevo-treecreatevostruct>`_

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - The created asset tree ID.


## Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 17772
     - The quota of tree reaches ceiling
     - Number of trees already reaches maximum of the OU.
   * - 99400
     - Invalid arguments
     - The request parameter is invalid. Check the request parameters.
   * - 99500
     - System error
     - Internal server error. Contact EnOS support.


## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=associate&orgId=yourOrgId&assetId=yourAssetId
method: POST 
requestBody:
{
	"tree":{
		"name":{
			"defaultValue":"Name"
		}
	}
}
```

### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "01b5477a-374e-49a0-8b68-7dbfe8f0b74f",
    "data": "cRUdS7sJ"
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
    public void testAssociateTree() {
        AssociateTreeRequest request = new AssociateTreeRequest();
        TreeCreateVo tree = new TreeCreateVo();
        I18nVo treeName = new I18nVo();
        treeName.setDefaultValue("treeDefaultName");
        tree.setName(treeName);
        request.setTree(tree);
        request.setOrgId(OrgId);
        request.setAssetId("yourAssetId");
        AssociateTreeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, AssociateTreeResponse.class);
    }
}
```