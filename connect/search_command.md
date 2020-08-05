# Search Command

Search for commands of a device and filter the results based on the search criteria.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Control

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.1/commands?action=search
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request




| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)        |
| assetId  | Query            | Optional (See **Note** above)  | String         | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | Optional (See **Note** above)      | String   | The product key. To be used with ``deviceKey``.    |
| deviceKey | Query           | Optional (See **Note** above)     | String       | The device key. To be used with ``productKey``.          |


## Request Parameters (Body)

| Name |  Mandatory/Optional | Data Type | Description |
|----------------|----------|--------------------|----|
| expression     | Optional    | String| The query expression, which supports sql-like query. The fields that are supported for query include: ``state``, ``commandName``, and ``createTime``. ``state``: supports arithmetic operator "=". ``commandName``: supports fuzzy inquiry, where ``locale`` is mandatory, such as "commandName.zh_CN" or "commandName.en_US". ``createTime``: supports ">", "=", and "<" to specify the time range. [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression) |
| pagination    | Optional     | Pagination Request Struct | Lists the paging requirements in a request. When not specified, the results are sorted in descending order by ``createTime`` by default with a pagination size of 100 pages. `sorters` is not supported to sort the response. For more details, see [Pagination Request Struct>>](/docs/api/en/2.1.0/overview.html#pagination-request-struct) |
| projection  | Optional    | Projection Struct | Enables you to crop the data result set returned in the request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see [How does projection crop the result set>>](/docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set)  |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |   Array of Command Structs       | The list of commands. For details, see [Command Struct>>](get_command.html#command-struct-command) |



## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/commands?action=search&deviceKey=yourDeviceKey&productKey=yourProductKey&orgId=yourOrgId
method: POST
requestBody:
{
    "expression": {
      "state = 2"
    },
    "pagination": {
      "pageNo":1,
      "pageSize":5
    }
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "df57e058-0d8b-4700-9e38-ef30132c155f",
  "data": [
    {
      "commandId": "2322417636630765568",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688731159,
      "createLocaltime": "2019-08-13 09:32:11",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 100,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417598073053184",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688726563,
      "createLocaltime": "2019-08-13 09:32:06",
      "commandType": 2,
      "commandName": {
        "defaultValue": "service522",
        "i18nValue": {
          "en_US": "service522"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "service522",
      "inputData": {
        "service_input": 555
      },
      "outputData": null
    },
    {
      "commandId": "2322417559066025984",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688721913,
      "createLocaltime": "2019-08-13 09:32:01",
      "commandType": 2,
      "commandName": {
        "defaultValue": "service522",
        "i18nValue": {
          "en_US": "service522"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "service522",
      "inputData": {
        "service_input": 555
      },
      "outputData": null
    },
    {
      "commandId": "2322417537678745600",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688719363,
      "createLocaltime": "2019-08-13 09:31:59",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417518334615552",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688717057,
      "createLocaltime": "2019-08-13 09:31:57",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    }
  ],
  "pagination": {
    "sortedBy": [
      {
        "field": "createDate",
        "order": "DESC"
      }
    ],
    "pageNo": 1,
    "pageSize": 5,
    "totalSize": 547
  }
}
```

## Sample 2

### Request Sample

```json
url: https://apigw-address/connect-service/v2.1/commands?action=search&deviceKey=zm_mqtt&productKey=bXuuAiku&orgId=yourOrgId
method: POST
requestBody:
{
  "expression": "commandName.zh_CN like \"Int_value\" AND createTime >= \"2019-08-13 09:00:00\"",
  "pagination": {
    "pageNo": 1,
    "pageSize": 5
  }
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "051ab2c9-5de4-4c05-9731-042475234267",
  "data": [
    {
      "commandId": "2322417698664521728",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688738554,
      "createLocaltime": "2019-08-13 09:32:18",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 0,
      "state": 6,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417676665921536",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688735932,
      "createLocaltime": "2019-08-13 09:32:15",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 0,
      "state": 6,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417636630765568",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688731159,
      "createLocaltime": "2019-08-13 09:32:11",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 30,
      "pendingTtl": 100,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417537678745600",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688719363,
      "createLocaltime": "2019-08-13 09:31:59",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    },
    {
      "commandId": "2322417518334615552",
      "orgId": "yourOrgId",
      "productKey": "yourProductKey",
      "deviceKey": "yourDeviceKey",
      "assetId": "sxH2DD6f",
      "createTime": 1565688717057,
      "createLocaltime": "2019-08-13 09:31:57",
      "commandType": 1,
      "commandName": {
        "defaultValue": "Int_value",
        "i18nValue": {
          "en_US": "Int_value"
        }
      },
      "timeout": 10,
      "pendingTtl": 600,
      "state": 2,
      "tslIdentifier": "Int_value",
      "inputData": 111,
      "outputData": null
    }
  ],
  "pagination": {
    "sortedBy": [
      {
        "field": "createDate",
        "order": "DESC"
      }
    ],
    "pageNo": 1,
    "pageSize": 5,
    "totalSize": 6
  }
}
```

## Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.command;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.connect_service.v2_1.service.SearchCommandRequest;
import com.envisioniot.enos.connect_service.v2_1.service.SearchCommandResponse;

public class SearchCommand {

    public static void main(String[] args) {
        String accessKey = "AccessKey of your APP";
        String secretKey = "SecretKey of your APP";
        String serverUrl = "https://{apigw-address}";

        String orgId = "yourOrgId";
        String productKey = "yourProdctKey";
        String deviceKey = "yourDeviceKey";

        SearchCommandRequest request = new SearchCommandRequest();
        request.setOrgId(orgId);
        request.setProductKey(productKey);
        request.setDeviceKey(deviceKey);
        request.setExpression("commandName.zh_CN like \"Int_value\" AND createTime >= \"2019-08-13 09:00:00\"");
        request.setPagination(new Pagination(5, 1, null));
        SearchCommandResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(serverUrl)
                .getResponse(request, SearchCommandResponse.class);
    }
}
```
