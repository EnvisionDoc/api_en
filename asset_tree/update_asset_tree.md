# Update Asset Tree

Update the information of an asset tree.

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
POST https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=update
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
   * - treeUpdateInfo
     - Mandatory
     - TreeUpdateVo Struct
     - The details to be provided when updating an asset tree. For more details, see `TreeUpdateVo Struct>> <update_asset_tree#treeupdatevo-struct-treeupdatevostruc>`_




### TreeUpdateVo Struct <treeupdatevostruc>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - treeId
     - Mandatory
     - String
     - The asset tree ID.
   * - name
     - Optional
     - StringI18n
     - Specify the asset tree's name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - tags
     - Optional
     - Tag Struct
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tags>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_




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

| Code | Description    |
|-----------|-----------------------------|
| 400| This error indicates that the asset tree to be updated does not exist. |

## Samples

### Request Sample

```json
url: https://{apigw-address}/asset-tree-service/v2.1/asset-trees?action=update&orgId=yourOrgId
method: POST 
requestBody: 
{
"treeUpdateInfo":{
    "treeId": "H4yVDl2U",
    "name": {
        "defaultValue": "Tree Name",
        "i18nValue":{
            "en_US":"EN Tree Name",
            "zh_CN":"名字"
        }
    },
    "tags":{
        "tag1":"Tag 1"
    }
}
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

## Java SDK Sample

```java
package com.envisioniot.enos.asset_tree_service;

import com.envision.apim.poseidon.config.PConfig;
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
    public void testUpdateTree() {
        UpdateTreeRequest request = new UpdateTreeRequest();
        request.setOrgId(OrgId);
        TreeUpdateVo treeUpdateVo = new TreeUpdateVo();
        treeUpdateVo.setTreeId("yourTreeId");
        I18nVo name = new I18nVo();
        name.setDefaultValue("treeDefaultName");
        treeUpdateVo.setName(name);
        Map < String, String > tagMap = new HashMap < > ();
        tagMap.put("key1", "value1");
        treeUpdateVo.setTags(tagMap);
        request.setTreeUpdateInfo(treeUpdateVo);
        UpdateTreeResponse response = Poseidon.config(PConfig.init().appKey(AccessKey).appSecret(SecretKey).debug())
            .url(ServerUrl)
            .getResponse(request, UpdateTreeResponse.class);
    }
}
```