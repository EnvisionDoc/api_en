# Create Asset Tree

Create an asset tree as well as its root node.

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=create
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
     - The organization ID which the Asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_




## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - asset
     - Mandatory
     - Asset Struct
     - The required data when creating a root node asset. For more details, see `Asset Struct <create_asset_tree.html#asset-struct-assetstruct>`_
   * - tree
     - Optional
     - TreeCreateVo Struct
     - The details of the asset tree to be created. For more details, see `TreeCreateVo Struct>> <create_asset_tree.html#treecreatevo-struct-treecreatevostruct>`_

### Asset Struct <assetstruct>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - modelID
     - Mandatory
     - String
     - The model ID. `How to get modelID </docs/api/en/2.1.0/api_faqs.html#how-to-get-model-id-modelid-modelid>`__
   * - name
     - Mandatory
     - StringI18n
     - Specify the asset's name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - timezone
     - Mandatory
     - String
     - + The timezone where the asset is located. 
       + Use the "+08:00" format for time zones that do not support Daylight Saving Time (DST). 
       + Use the "Asia/Shanghai" format for time zones that support DST. 
       For details, see `Timezone representation </docs/api/en/2.1.0/api_faqs.html#timezone-representation>`_
   * - description
     - Optional
     - String
     - The asset description.
   * - attributes
     - Optional
     - Map
     - Attributes of the model which the asset belongs to.
       The Key is the attribute ID, which is of String type. The Value type depends on the attribute defined in the Model. For details, see `attributes representation </docs/api/en/2.1.0/api_faqs.html#attributes-representation>`_
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tag </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_

### TreeCreateVo Struct <treecreatevostruct>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - name
     - Mandatory
     - StringI18n
     - Specify the asset tree's name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tags </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_

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
url: https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=create&orgId=yourOrgId
method: POST 
requestBody:
{
	"asset":{
		"modelId":"modelName",
		"name":{
			"defaultValue":"Name"
		},
		"timezone":"+12:00",
		"description":"Example of description"
	},
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
  "msg": "OK",
  "code": 0,
  "data": "HfzFPn1H",
  "requestId": "bb4f8c40-604a-451e-83bd-99cfba6bd53e"
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
    public void testCreateTree() {
        TreeCreateVo tree = new TreeCreateVo();
        I18nVo treeName = new I18nVo();
        treeName.setDefaultValue("treeDefaultName");
        tree.setName(treeName);
        CreateTreeRequest request = new CreateTreeRequest();
        Map < String, String > i18nValue = new HashMap();
        i18nValue.put("zh_CN", "assetName");
        I18nVo name = new I18nVo();
        name.setDefaultValue("assetDefaultName");
        name.setI18nValue(i18nValue);
        AssetCreateVo asset = new AssetCreateVo();
        asset.setModelId("yourModelId");
        asset.setName(name);
        asset.setTimezone("+08:00");
        asset.setDescription("This is a sampled asset");
        request.setTree(tree);
        request.setAsset(asset);
        request.setOrgId(OrgId);
        CreateTreeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, CreateTreeResponse.class);
    }
}
```