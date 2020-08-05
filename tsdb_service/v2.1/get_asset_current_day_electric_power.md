# Get Asset Current Day Electric Power

Get the accumulated power consumption/production data of specified devices from 00:00 (local time) of the current day.

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
POST https://{apigw-address}/tsdb-service/v2.1/electric-power/current-day
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
     - Asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - pointIds
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas.The upper limit of the number of measurement points that can be queried is 3,000 (number of devices * number of measurement points). `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
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
     - The list of asset data. The data returned for a single point of a single device is sorted by the data timestamp in ascending order. For more information, see `items <get_asset_current_day_electric_power#items>`__

### items

#### Sample  

```json
{
        "assetId": "Ps4PViva",		
        "timestamp": 1590076800000,        
        "sum(pi_point)": 10.615000000000002,
        "localtime": "2020-05-22 00:00:00"
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
   * - sum(pointId)
     - Double
     - This parameter is a variable, representing the identifier and data of the measurement point. The data here is the daily aggregation of the sum of power sonsumption/production data.  
   * - localtime
     - String
     - Local time stamp of the returned data.

## Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

## Samples

### Request Sample
```
url: https://{apigw-address}/tsdb-service/v2.1/electric-power/current-day?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva",
  "pointIds": "pi_point",
  "localTimeAccuracy": "true",
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
        "timestamp": 1590076800000,
        "sum(pi_point)": 10.615000000000002,
        "localtime": "2020-05-22 00:00:00"
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
    public void GetAssetCurrentDayElectricPower() {
        Request request = new Request();
        request.setBodyParams("assetIds", "yourAssetId1,yourAssetId2");
        request.setBodyParams("pointIds", "pi_point");
        request.setBodyParams("localTimeAccuracy", "true");
        request.setBodyParams("localTimeFormat", 1);
        request.setBodyParams("itemFormat", 0);

        request.setMethod("POST");

        JSONObject response = poseidon
                .url(API_Gateway_URL + "/tsdb-service/v2.1/electric-power/current-day")
                .queryParam("orgId", "yourOrgId")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
