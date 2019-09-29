# Search Command

Query the details of the commands. List all commands of one device and do result filter based on search criteria.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/commands?action=search
```

## Request Parameters (URI)

.. note:: In the following non-required fields, you must provide ``assetId`` or a combination of ``productKey`` and ``deviceKey`` to specify the device.

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>


| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)        |
| assetId  | Query            | False   | String         | Asset ID. [How to get assetId>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query          | False       | String   | Product Key     |
| deviceKey | Query           | False      | String       | Device Key         |


## Request Parameters (Body)

| Name |  Required or Not | Data Type | Description |
|----------------|----------|--------------------|----|
| expression     | false    | String| Query expression, which supports for sql-like query. The fields that are supported for query include: `state`, `commandName`, and `createTime`.<br>`state`: support arithmetic operators "=".<br>`commandName`: support fuzzy inquiry, `locale` is mandatory, such as "commandName.zh_CN" or "commandName.en_US".<br>`createTime`: supports ">", "=", and "<" to specify a time range. [How to use expression>>](/docs/api/en/2.0.9/api_faqs.html#how-to-use-expression) |
| pagination    | false     | Pagination request struct | Pagination parameter. The default is to sort in descending order by `occurTime`. When not specified, the default pagination size is 100 pages. See [Pagination Request Struct>>](/docs/api/en/2.0.9/overview.html#pagination-request-struct) |
| projection  | false    | Projection struct | Used to describe the object projection to be returned in the interface request. For details, see [How does projection crop the result set>>](/docs/api/en/2.0.9/api_faqs.html#how-does-projection-crop-the-result-set)  |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    getCommand struct       | Information corresponding to the search criteria. See [Command Struct>>](get_command.html#command-struct-command) |



## Sample 1

### Request Sample

```
POST
https://apigw-address/connect-service/v2.1/commands?action=search&deviceKey=zm_mqtt&productKey=bXuuAiku&orgId=yourOrgId
{
    "expression": "state = 2",
    "pagination": {"pageNo":1,"pageSize":5}
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

```
POST
https://apigw-address/connect-service/v2.1/commands?action=search&deviceKey=zm_mqtt&productKey=bXuuAiku&orgId=yourOrgId
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
        String accessKey = "...";
        String secretKey = "...";
        String serverUrl = "https://...";
 
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