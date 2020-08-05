# Get Asset DI Data Duration

Get the duration of different status (DI) data of specified devices within a certain period.

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
POST https://{apigw-address}/tsdb-service/v2.1/di/duration
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
     - he model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get assetId>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - pointIds
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 10 (Number of devices * Number of measurement points). `How to get pointId>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
   * - startTime
     - Mandatory
     - String
     - The start time of the sampling data, where both UTC and local time formats are supported. For UTC time format, the application will query all the asset data by the unified start timestamp and end timestamp. Timezone information is required for the UTC time format: 2019-06-01T00:00:00+08:00. For local time format, the application will query the asset data by the local time of where the device is located. Its format is: YYYY-MM-DD HH:MM:SS.
   * - endTime
     - Mandatory
     - String
     - The end time of the sampling data. Its format must be consistent with ``startTime``.
   * - status
     - Optional
     - String
     - Filter results that include multiple status durations. For example, if only the results of status 0 are required, set the value as "0". Multiple status are supported. Separate the status by commas.
   * - ifWithUnknown
     - Optional
     - Boolean
     - When the status cannot be confirmed for a certain period of time, the status is “Unknown”. true (default) = includes the "Unknown" status in the response. false = does not include the "Unknown" status in the response.
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
     - The list of asset data. The data returned for a single point of a single device is sorted by the data timestamp in ascending order. For more information, see `items <get_asset_di_data_durations#items>`__

### items

#### Sample

```json
{
    "scanEndTimestamp": 1569859800000,   
    "pointId": "di_point",
    "assetId": "Ps4PViva",			
    "durations": [
      {
        "duration": 60000,
        "status": 0
      },
      {
        "duration": 60000,
        "status": 1
      }
    ]
}
```

#### Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - scanEndTimestamp
     - Long
     - The timestamp of the last data to be scanned. The total number of data for one time scan must not exceed 640000. When the data exceeds 640000, the scan is stopped. This parameter returns the timestamp of the last data scanned, indicating the data after this timestamp are not included.
   * - assetId
     - String
     - The asset ID.
   * - pointId
     - String
     - The measurement point ID.
   * - durations
     - List<JSONObject>
     - A list of the durations of different statuses.
   * - status
     - Integer
     - The value of the measurement point of the device.
   * - duration
     - Integer
     - The duration of the above ``status`` from the start time selected by the user to the ``scanEndTimestamp`` (in milliseconds).

## Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

## Sample 1

### Request Sample

When ``ifWithUnknown`` is true:

```
url: https://{apigw-address}/tsdb-service/v2.1/di/duration?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva,d5CT3dY7",
  "pointIds": "di_point",
  "startTime": "2020-03-01 00:00:00",
  "endTime": "2020-03-02 00:00:00",
  "status": "0,1",
  "ifWithUnknown": "true",
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
                "scanEndTimestamp": 1583082072000,
                "pointId": "di_point",
                "assetId": "Ps4PViva",
                "durations": [
                    {
                        "duration": 60000,
                        "status": 0
                    },
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 180000,
                        "status": "Unknown"
                    }
                ]
            },
            {
                "scanEndTimestamp": 1583082072000,
                "pointId": "di_point",
                "assetId": "d5CT3dY7",
                "durations": [
                    {
                        "duration": 60000,
                        "status": 0
                    },
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 180000,
                        "status": "Unknown"
                    }
                ]
            }
        ]
    }
}
```


## Sample 2

### Request Sample

When ``ifWithUnknown`` is false:

```
url: https://{apigw-address}/tsdb-service/v2.1/di/duration?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva,d5CT3dY7",
  "pointIds": "di_point",
  "startTime": "2020-03-01 00:00:00",
  "endTime": "2020-03-02 00:00:00",
  "status": "0,1",
  "ifWithUnknown": "false",
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
                "scanEndTimestamp": 1583082072000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 0
                    },
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "pointId": "di_point",
                "assetId": "Ps4PViva"
            },
            {
                "scanEndTimestamp": 1583082072000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 0
                    },
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "pointId": "di_point",
                "assetId": "d5CT3dY7"
            }
        ]
    }
}
```

## Sample 3

### Request Sample

Filter the ``status``:

.. note:: After `status` filtering, the status "Unknown" will be not inluded in the response.

```
url: https://{apigw-address}/tsdb-service/v2.1/di/duration?orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva,d5CT3dY7",
  "pointIds": "di_point",
  "startTime": "2020-03-01 00:00:00",
  "endTime": "2020-03-02 00:00:00",
  "status": "1",
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
                "scanEndTimestamp": 1583082072000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "pointId": "di_point",
                "assetId": "Ps4PViva"
            },
            {
                "scanEndTimestamp": 1583082072000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "pointId": "di_point",
                "assetId": "d5CT3dY7"
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
    public void GetAssetStatusDuration() {
        Request request = new Request();
        request.setBodyParams("modelId", "yourModelId");
        request.setBodyParams("assetIds", "yourAssetId1,yourAssetId2");
        request.setBodyParams("pointIds", "di_point");
        request.setBodyParams("startTime", "2020-03-01 00:00:00");
        request.setBodyParams("endTime", "2020-03-02 01:01:12");
        request.setBodyParams("status", "0,1");
        request.setBodyParams("ifWithUnknown", false);
        request.setBodyParams("localTimeFormat", 1);
        request.setBodyParams("itemFormat", 0);

        JSONObject response = poseidon
                .url(API_Gateway_URL + "/tsdb-service/v2.1/di/duration")
                .queryParam("orgId", "yourOrgId")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
