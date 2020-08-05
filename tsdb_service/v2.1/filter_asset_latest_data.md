# Filter Asset Latest Data

Filter and query the latest data of a single measurement point for multiple devices.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Read

For more information about resources and required permission, see [Policies, Roles and Permissions>>](/docs/enos/en/2.1.0/iam/concept/access_policy.html)

## Request Format

```
POST https://{apigw-address}/tsdb-service/v2.1/latest/filter
```

## Request Parameters (URI)

.. list-table::
   :widths: 15 25 15 15 30
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
     - The organization ID which the asset belongs to. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - modelId
     - Mandatory
     - String
     - The model ID. `How to get model ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - pointId
     - Mandatory
     - String
     - The measurement point ID. `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
   * - operator
     - Mandatory
     - String
     - The query operator. It supports:   

       + eq: equals to
       + nq: not equals to
       + gt: greater than
       + lt: less than
       + ge: greater than or equals to
       + le: less than or equals to
       + between: interval of 2 values
       + in: one of multiple values
   * - valueFilter
     - Mandatory
     - String
     - The value to filter for. It must be used along with the operator. The operators "eq", "nq", "gt", "ge", "lt", and "le" correspond to a single value; "between" corresponds to 2 values; "in" corresponds to multiple values. Multiple values must be separated by commas, and the data types must be consistent with those of the measurement points. For example: "operator=betwteen&valueFilter=a, b" refers to filtering out the values between a and b.
   * - timeWindow
     - Optional
     - Integer
     - Specify the time window for filtering the latest data (by minutes). The minimum value is 0. If not specified, no constrain is applied.
   * - ifWithLocalTime
     - Optional
     - Boolean
     -      
       + true = returns data in local time format
       + false (default) = does not return data in local time format

   * - localTimeAccuracy
     - Optional
     - Boolean
     -      
       + true = query returns data with millisecond time stamp
       + false (default) = query returns data without millisecond time stamp

   * - localTimeFormat
     - Optional
     - Integer
     - Specify whether the local time value includes time zone information of devices. 0 (default): without time zone information; 1: with time zone information.
   * - itemFormat
     - Optional
     - Integer
     - Specify the displaying format of the returned device data. Available options are 0, 1, and 2. For the example of each displaying format, see `Item Format Example>> </docs/api/en/2.1.0/api_faqs#item-format-example>`__   

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<JSONObject>
     - The list of asset data. The data returned for a single point of a single device is sorted by the data timestamp in ascending order. For more information, see `items <filter_asset_latest_data#items>`__

### items

#### Sample

```json
{        
    "localtime":"2020-03-31T23:59:59+08:00",
    "assetId": "Ps4PViva",
    "pointId": 1.5,
    "timestamp": 1585670399000
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - assetId
     - String
     - The asset ID.
   * - timestamp
     - Long
     - The data timestamp (UNIX time, accurate to the second).
   * - pointId
     - Double
     - This parameter is a variable, representing the identifier and data of the measurement point.
   * - localtime
     - String
     - The data timestamp in local time format (accurate to the second). The value of the ``localTimeFormat`` parameter determines whether the local time value includes the time zone information.

## Error Codes
For the description of error codes, see [Common Error Codes](overview#common-error-codes).

## Samples

### Request Sample
```
url: https://{apigw-address}/tsdb-service/v2.1/latest/filter?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "modelId": "export_data",
  "assetIds": "Ps4PViva",
  "pointId": "pi_point",
  "operator": "le",
  "valueFilter": "100",
  "timeWindow": "",
  "ifWithLocalTime": "true",
  "localTimeAccuracy": "false",
  "localTimeFormat": 1,
  "itemFormat": 0
}
```

Where, `operator=le&valueFilter=100` means that: The sample code will filter out the `pi_point` value of the model `export_data`, which is less than or equal to 100.

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "submsg": null,
  "data": {
    "items": [
      {
        "localtime":"2020-03-31T23:59:59+08:00",
        "assetId": "Ps4PViva",
        "pi_point": 1.5,
        "timestamp": 1585670399000
      }
    ]
  }
}
```

## Java SDK Sample

```java
import com.alibaba.fastjson.JSONObject;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envision.apim.poseidon.request.PoseidonRequest;
import org.junit.Before;
import org.junit.Test;

public class Sample {
    private static final String API_Gateway_URL = "https://{domain_url}";
    private Poseidon poseidon;

    private static class Request extends PoseidonRequest {

        public void setBodyParams(String key, Object value) {
            bodyParams().put(key, value);
        }

        public void setMethod(String method) {
            this.method = method;
        }

        private String method;

        @Override
        public String baseUri() {
            return "";
        }

        @Override
        public String method() {
            return method;
        }
    }

    @Before
    public void init() {
        poseidon = Poseidon.config(
                PConfig.init()
                        .appKey("AccessKey of your APP")
                        .appSecret("SecretKey of your APP")
        ).method("POST").header("Content-Type", "application/json");
    }

    @Test
    public void FilterAssetLatestData() {
        Request request = new Request();
        request.setBodyParams("modelId", "yourModelId");
        request.setBodyParams("assetIds", "yourAssetId1,yourAssetId2");
        request.setBodyParams("pointId", "yourPointId");
        request.setBodyParams("operator", "gt");
        request.setBodyParams("valueFilter", "1000");
        request.setBodyParams("ifWithLocalTime", true);
        request.setBodyParams("localTimeAccuracy", false);
        request.setBodyParams("localTimeFormat", 1);
        request.setBodyParams("itemFormat", 0);

        JSONObject response =  poseidon
                .url(API_Gateway_URL + "/tsdb-service/v2.1/latest/filter")
                .queryParam("orgId", "yourOrgId")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
