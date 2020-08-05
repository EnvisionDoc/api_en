# Create and Link Asset

Create an asset and link it to an asset tree.

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=createAsset
```

## Request Parameters (URI)

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
     - The organization ID which the asset belongs to `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - treeId
     - Query
     - Mandatory
     - String
     - The asset tree ID. `How to get treeID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-the-id-of-an-asset-tree>`__
   * - parentAssetId
     - Query
     - Mandatory
     - String
     - The asset ID of the parent node of the asset to be linked.



## Request Parameters (Body)

.. list-table::
   :header-rows: 1

   * - Name
     - Mandatory / Optional
     - Data Type
     - Description
   * - asset
     - Mandatory
     - ``Asset`` Struct
     - The asset details to be provided when creating an asset. For more information, see `Asset Struct <create_and_associate_asset#asset-struct-assetstruc>`_



### Asset Struct <assetstruc>

.. list-table::
   :widths: 15 15 25 45
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - modelId
     - Mandatory
     - String
     - The model ID which the asset belongs to. `How to get modelID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-model-id-modelid-modelid>`_
   * - name
     - Mandatory
     - StringI18n
     - Specify the asset's name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - timezone
     - Mandatory
     - String
     - The timezone where the asset is located. Use the "+08:00" format for time zones that do not support Daylight Saving Time (DST). Use the "Asia/Shanghai" format for time zones that support DST. For details, see `Timezone representation>> </docs/api/en/2.1.0/api_faqs.html#timezone-representation>`_
   * - description
     - Optional
     - String
     - The asset description.
   * - attributes
     - Optional
     - Map
     - Attributes of the model which the asset belongs to. The Key is the attribute ID, which is of String type. The Value type depends on the attribute defined in the Model. For details, see `attributes representation>> </docs/api/en/2.1.0/api_faqs.html#attributes-representation>`_
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tag>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_





## Response Parameters

| Name | Data Type | Description      |
|:-----|:----------|:-----------------|
| data | String    | The ID of the created asset. |


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

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-nodes?action=createAsset&treeId=yourTreeId&parentAssetId=yourParentAssetId&orgId=yourOrgId
method: POST 
requestBody: 
{
    "asset": {
        "modelId": "STRING-INVERTER-MODEL",
        "name": {
            "defaultValue": "逆变器 #1",
            "i18nValue": {
                "en_US": "Inverter #1"
            }
        },
        "timezone": "+08:00",
        "description": "This is a sample asset.",
        "attributes": {
            "foo": 100,
            "bar": "example"
        },
        "tags": {
            "foo": "bar",
            "hello": "world"
        }
    }
}
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

import java.util.HashMap;
import java.util.Map;

import com.envisioniot.enos.asset_tree_service.v2_1.CreateAssetNodeRequest;
import com.envisioniot.enos.asset_tree_service.v2_1.CreateAssetNodeResponse;
import org.junit.Test;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.asset_tree_service.vo.AssetCreateVo;
import com.envisioniot.enos.asset_tree_service.vo.I18nVo;

public class CreateAssetNodeTest {
    private static String AccessKey = "yourAccessKey";
    private static String SecretKey = "yourSecretKey";
    private static String OrgId = "yourOrgId";
    private static String ServerUrl = "yourServerUrl";

    @Test
    public void testCreateAssetNode() {

        CreateAssetNodeRequest request = new CreateAssetNodeRequest();
        request.setOrgId(OrgId);
        request.setTreeId("yourTreeId");
        request.setParentAssetId("yourParentAssetId");
        AssetCreateVo asset = new AssetCreateVo();
        Map < String, String > i18nValue = new HashMap();
        i18nValue.put("zh_CN", "assetName");
        I18nVo name = new I18nVo();
        name.setDefaultValue("asseTDefaultName");
        name.setI18nValue(i18nValue);
        asset.setName(name);
        asset.setModelId("yourModelId");
        asset.setTimezone("+08:00");
        asset.setDescription("This is a sampled asset");
        request.setAsset(asset);
        CreateAssetNodeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl).getResponse(request, CreateAssetNodeResponse.class);
    }
}
```