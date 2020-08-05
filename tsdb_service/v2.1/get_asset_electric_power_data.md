# Get Asset Electric Power Data

Get the power consumption/production data of specified devices within a certain period.

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
POST https://{apigw-address}/tsdb-service/v2.1/electric-power
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
     - Optional
     - String
     - The model ID. `How to get model ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - pointIdsWithLogic
     - Mandatory
     - String
     - The aggregation logic with measurement point ID. The supported aggregation calculation methods include count, avg, sum, max, min, first, and last. The time range for the aggregation query is ``[startTime, endTime)``, that is, the aggregation operand contains the data at the time of ``startTime``, but does not contain the data at the time of ``endTime``. The upper limit of the number of measurement points that can be queried is 3,000. Format: ``Function(pointId)``, supporting multiple measurement points e.g. `sum(pointId1),sum(pointId2)`. `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
   * - interval
     - Mandatory
     - Integer
     - The time interval for the aggregation algorithm to work. The effective value is 0-1440, calculated in minutes. If the interval value is 0, the measurement point has no aggregation logic; if the interval value is greater than 0, the measurement point must have the aggregation logic.
   * - startTime
     - Mandatory
     - String
     - The start time of the sampling data, where both UTC and local time formats are supported.

       + For UTC time format, the application will query all the asset data by the unified start timestamp and end timestamp. Timezone information is required for the UTC time format: 2019-06-01T00:00:00+08:00.
       + For local time format, the application will query the asset data by the local time of where the device is located. Its format is: YYYY-MM-DD HH:MM:SS.
   * - endTime
     - Mandatory
     - String
     - The end time of the sampling data. Its format must be consistent with ``startTime``.
   * - pageSize
     - Optional
     - Integer
     - The upper limit of the returned records in a single page for a single measurement point of a single device, which is 1,000 by default. For a single query, the total returned data amount follows the constraint: (Number of devices  * Number of points * pagesize) ≤ 640,000.
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
     - The list of asset data. The data returned for a single point of a single device is sorted by the data time stamp in ascending order. For more information, see `items <get_asset_electric_power_data#items>`__

### items

#### Sample

```json
{
       "assetId": "4DXYH7nS", 		
       "timestamp": 1560249300000,
       "sum(opentsdb_pi_point)": 4.246,  
       "localtime": "2019-06-11 18:35:00"
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
   * - pointIdsWithLogic
     - Double
     - This parameter is a variable, representing the identifier and data of the measurement point (with or without aggregation logic). The data here is the daily aggregation of the sum of power consumption/production data.
   * - timestamp
     - Long
     - The data timestamp (UNIX time, accurate to the second).
   * - localtime
     - String
     - The data timestamp in local time format (accurate to the second). The value of the ``localTimeFormat`` parameter determines whether the local time value includes the time zone information.


## Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

## Sample 1

### Request Sample
Local time format:
```
url: https://{apigw-address}/tsdb-service/v2.1/electric-power?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva,VRV1XRJO",
  "pointIdsWithLogic": "sum(pi_point)",
  "startTime": "2020-03-01 00:00:00",
  "endTime": "2020-03-01 00:15:00",
  "interval": 10,
  "localTimeAccuracy": "false",
  "localTimeFormat": 1,
  "itemFormat": 0
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "submsg": null,
  "data": {
    "items": [
      {
        "assetId": "Ps4PViva",
        "timestamp": 1582992000000,
        "sum(pi_point)": 6.853,
        "localtime": "2020-03-01T00:00:00+08:00"
      },
      {
        "assetId": "VRV1XRJO",
        "timestamp": 1582992000000,
        "sum(pi_point)": 4.246,
        "localtime": "2020-03-01T00:00:00+08:00"
      }
    ]
  }
}
```


## Sample 2

### Request Sample
UTC time format:
```
url: https://{apigw-address}/tsdb-service/v2.1/electric-power?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva,VRV1XRJO",
  "pointIdsWithLogic": "sum(pi_point)",
  "startTime": "2020-03-01T00:00:00+08:00",
  "endTime": "2020-03-01T00:15:00+08:00",
  "interval": 10,
  "localTimeAccuracy": "false",
  "localTimeFormat": 1,
  "itemFormat": 0
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "submsg": null,
  "data": {
    "items": [
      {
        "assetId": "Ps4PViva",
        "timestamp": 1582992000000,
        "sum(pi_point)": 6.853,
        "localtime": "2020-03-01T00:00:00+08:00"
      },
      {
        "assetId": "VRV1XRJO",
        "timestamp": 1582992000000,
        "sum(pi_point)": 4.246,
        "localtime": "2020-03-01T00:00:00+08:00"
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
    public void GetAssetElectricPowerData() {
        Request request = new Request();
        request.setBodyParams("modelId", "yourModelId");
        request.setBodyParams("assetIds", "yourAssetId1,yourAssetId2");
        request.setBodyParams("pointIdsWithLogic", "sum(pi_point)");
        request.setBodyParams("startTime", "2020-03-01 00:00:00");
        request.setBodyParams("endTime", "2020-03-01 01:01:12");
        request.setBodyParams("localTimeAccuracy", false);
        request.setBodyParams("localTimeFormat", 1);
        request.setBodyParams("itemFormat", 0);
        request.setBodyParams("interval", 10);

        JSONObject response = poseidon
                .url(API_Gateway_URL + "/tsdb-service/v2.1/electric-power")
                .queryParam("orgId", "yourOrgId")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
