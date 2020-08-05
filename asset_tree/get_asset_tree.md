# Get Asset Tree

Get the details of an asset tree using an asset tree ID.

## Access Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Access
     - Permission Type
   * - Asset Tree Management
     - Read

## Request Format

```json
GET https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=get
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
     - The organization ID which the asset belongs to. `How to obtain orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - treeId
     - Query
     - Mandatory
     - String
     - The asset tree ID. `How to obtain treeID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree>`_


## Response Parameters

.. list-table::
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
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - asset
     - Asset Struct
     - The details of an asset. For more information, see `asset Struct </docs/api/en/2.1.0/asset_tree/get_asset_tree.html#asset-struct-assetstruct>`_


### Asset Struct <assetstruct>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - assetId
     - String
     - Asset ID
   * - modelId
     - String
     - Model ID of this asset
   * - modelIdPath
     - String
     - Path of Model ID
   * - name
     - StringI18n
     - The Asset's name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - timezone
     - String
     - Timezone where the asset is located.
   * - description
     - String
     - Description of the Asset
   * - label
     - String
     - The type of Asset. "0" = Device Asset and "1" = Logical Asset.
   * - inValid
     - Boolean
     - "True" indicates invalid nodes while "false" indicates valid nodes.
   * - attributes
     - Map
     - Attributes of the Model which the Asset belongs to. Key is the attribute ID, which is of String type. The Value type depends on the attribute defined in the Model. 
   * - tags
     - Map 
     - User-defined tags. (The Key and Value are of String type.)


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
   * - 99400
     - Invalid arguments
     - The request parameter is invalid. Check the request parameters.
   * - 99500
     - System error
     - Internal server error. Contact EnOS support.

## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=get&treeId=yourTreeId&orgId=yourOrgId
method: GET 
```

### Return Sample

```json
{
 "code": 0,
 "msg": "OK",
 "requestId": "f3c1ffc7-cc8e-4a50-ad40-0fa7b0c3a7ac",
 "data": {
  "treeId": "BRIt3ee3",
  "name":{
			"defaultValue":"ourTreeId",
			"i18nValue":{
				"en_US":"ourTreeID"
			}
		},
  "tags": {
   "user": "zm",
   "user0": "lily"
  },
  "asset": {
   "inValid": false,
   "assetId": "nlw68lR5",
   "modelId": "model_0422",
   "modelIdPath": "/model_0422",
   "name": {
    "defaultValue": "0430343",
    "i18nValue": {
     "en_US": "0430343"
    }
   },
   "timezone": "+08:00",
   "description": null,
   "label": "1",
   "attributes": {},
   "tags": {
    "tree": "0430"
   }
  }
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
    public void testGetTree() throws Exception {;
        GetAssetTreeRequest request = new GetAssetTreeRequest();
        request.setOrgId(OrgId);
        request.setTreeId("yourTreeId");
        GetAssetTreeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, GetAssetTreeResponse.class);
        System.out.println(response.getData());
    }
}
```