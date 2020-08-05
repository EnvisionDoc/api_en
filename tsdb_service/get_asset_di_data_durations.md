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

## Using GET Method

### Request Format

```
GET https://{apigw-address}/tsdb-service/v2.0/di/duration
```

### Request Parameters (URI)

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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - modelId
     - Query
     - Optional
     - String
     - The model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Query
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get assetId>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - measurepoints
     - Query
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 10 (Number of devices * Number of measurement points). `How to get pointId>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
   * - startTime
     - Query
     - Mandatory
     - String
     - The start time of the sampling data, where both UTC and local time formats are supported.  

       + For UTC time format, the application will query all the asset data by the unified start timestamp and end timestamp. Timezone information is required for the UTC time format: 2019-06-01T00:00:00+08:00.
       + For local time format, the application will query the asset data by the local time of where the device is located. Its format is: YYYY-MM-DD HH:MM:SS.
   * - endTime
     - Query
     - Mandatory
     - String
     - The end time of the sampling data. Its format must be consistent with ``startTime``.
   * - status
     - Query
     - Optional
     - String
     - Filter results that include multiple status durations. For example, if only the results of status 0 are required, set the value as "0". Multiple status are supported. Separate the status by commas.
   * - ifWithUnknown
     - Query
     - Optional
     - Boolean
     - When the status cannot be confirmed for a certain period of time, the status is “Unknown”.      
         + true (default) = includes the "Unknown" status in the response
         + false = does not include the "Unknown" status in the response

### Response Parameters <response>

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<JSONObject>
     - The list of asset data. The data returned for a single point of a single device is sorted by the data timestamp in ascending order. For more information, see `items <get_asset_di_data_durations#items>`__


#### items

##### Sample

```json
{
    "scanEndTimestamp": 1569859800000,
    "measurepoint": "di_point1",
    "assetId": "f4Bkwc5Q",
    "durations": [
      {
        "duration": 60000,
        "status": 1
      },
      {
        "duration": 60000,
        "status": 2
      }
    ]
}
```

##### Parameters

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
   * - measurepoint
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


### Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

### Sample 1 (GET Method)

#### Request Sample

When ``ifWithUnknown`` is true:

```
url: https://{apigw-address}/tsdb-service/v2.0/di/duration?orgId=yourOrgId&assetIds=f4Bkwc5Q,SSbqxq88&measurepoints=di_point1&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&ifWithUnknown=true

method: GET
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "scanEndTimestamp": 1569859380000,
                "measurepoint": "di_point1",
                "assetId": "f4Bkwc5Q",
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
                    },
                    {
                        "duration": 180000,
                        "status": "Unknown"
                    }
                ]
            },
            {
                "scanEndTimestamp": 1569859380000,
                "measurepoint": "di_point1",
                "assetId": "SSbqxq88",
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
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


### Sample 2 (GET Method)

#### Request Sample

When ``ifWithUnknown`` is false:

```
url: https://{apigw-address}/tsdb-service/v2.0/di/duration?orgId=yourOrgId&assetIds=f4Bkwc5Q,SSbqxq88&measurepoints=di_point1&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&ifWithUnknown=false
method: GET
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "f4Bkwc5Q"
            },
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "SSbqxq88"
            }
        ]
    }
}
```

### Sample 3 (GET Method)

#### Request Sample

Filter the ``status``:

.. note:: After ``status`` filtering, the status "Unknown" will be not inluded in the response.

```
url: https://{apigw-address}/tsdb-service/v2.0/di/duration?orgId=yourOrgId&assetIds=f4Bkwc5Q,SSbqxq88&measurepoints=di_point1&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&status=1
method: GET
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "f4Bkwc5Q"
            },
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "SSbqxq88"
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
import org.junit.Test;

public class GetMethod {

    private static class Request extends PoseidonRequest {

        public void setQueryParam(String key, Object value){
            queryEncodeParams().put(key, value);
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

    @Test
    public void GetAssetDIDataTest(){

        //1. Click Application Registration in the left navigation of the EnOS Management Console.
        //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
        String accessKey = "yourAccessKey";
        String secretKey = "yourSecretKey";

        //Create a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
        Request request = new Request();
        request.setQueryParam("orgId", "yourOrgId");
        request.setQueryParam("modelId", "opentsdb_model");
        request.setQueryParam("assetIds","4DXYH7nS");
        request.setQueryParam("measurepoints", "opentsdb_di_point");
        request.setQueryParam("startTime", "2019-06-01 00:00:00"); //For UTC time format: 2019-06-01T00:00:00+08:00
        request.setQueryParam("endTime", "2019-06-11 23:00:00");   //For UTC time format: 2019-06-11T23:00:00+08:00
        request.setQueryParam("ifWithUnknown", false);
        request.setQueryParam("status", "1,2");

        request.setMethod("GET");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("http://apim-gateway/tsdb-service/v2.0/di/duration")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Using POST Method

### Request Format

```
POST https://{apigw-address}/tsdb-service/v2.0/di/duration
```

### Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - modelId
     - Optional
     - String
     - he model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get assetId>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - measurepoints
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 10 (Number of devices * Number of measurement points). `How to get pointId>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
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
   * - status
     - Optional
     - String
     - Filter results that include multiple status durations. For example, if only the results of status 0 are required, set the value as "0". Multiple status are supported. Separate the status by commas.
   * - ifWithUnknown
     - Optional
     - Boolean
     - When the status cannot be confirmed for a certain period of time, the status is “Unknown”.      
         + true (default) = includes the "Unknown" status in the response
         + false = does not include the "Unknown" status in the response

### Response Parameters

See description in [Response Parameters](get_asset_di_data_durations#response-parameters-response) of the **Using GET Method** section.

### Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

### Sample 1 (POST Method)

#### Request Sample

When ``ifWithUnknown`` is true:

```
url: https://{apigw-address}/tsdb-service/v2.0/di/duration

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
orgId:yourOrgId
modelId:xxx
assetIds:f4Bkwc5Q,SSbqxq88
measurepoints:di_point1
startTime:2019-06-01%2010:00:00
endTime:2019-06-11%2023:00:00
ifWithUnknown=true
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "scanEndTimestamp": 1569859380000,
                "measurepoint": "di_point1",
                "assetId": "f4Bkwc5Q",
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
                    },
                    {
                        "duration": 180000,
                        "status": "Unknown"
                    }
                ]
            },
            {
                "scanEndTimestamp": 1569859380000,
                "measurepoint": "di_point1",
                "assetId": "SSbqxq88",
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
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


### Sample 2 (POST Method)

#### Request Sample

When ``ifWithUnknown`` is false:

```
url: https://{apigw-address}/tsdb-service/v2.0/di/duration

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
orgId:yourOrgId
modelId:xxx
assetIds:f4Bkwc5Q,SSbqxq88
measurepoints:di_point1
startTime:2019-06-01%2010:00:00
endTime:2019-06-11%2023:00:00
ifWithUnknown=false
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "f4Bkwc5Q"
            },
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    },
                    {
                        "duration": 60000,
                        "status": 2
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "SSbqxq88"
            }
        ]
    }
}
```

### Sample 3 (POST Method)

#### Request Sample

Filter the ``status``:

.. note:: After `status` filtering, the status "Unknown" will be not inluded in the response.

```
url: https://{apigw-address}/tsdb-service/v2.0/di/duration

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
orgId:yourOrgId
modelId:xxx
assetIds:f4Bkwc5Q,SSbqxq88
measurepoints:di_point1
startTime:2019-06-01%2010:00:00
endTime:2019-06-11%2023:00:00
status=1
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "f4Bkwc5Q"
            },
            {
                "scanEndTimestamp": 1569859380000,
                "durations": [
                    {
                        "duration": 60000,
                        "status": 1
                    }
                ],
                "measurepoint": "di_point1",
                "assetId": "SSbqxq88"
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
import org.junit.Test;

public class PostMethod {

    private static class Request extends PoseidonRequest {

        public void setFormParam(String key, String value){
            formParams().put(key, value);
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

    @Test
    public void GetAssetDIDataTest(){

        //1. Click Application Registration in the left navigation of the EnOS Management Console.
        //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
        String accessKey = "yourAccessKey";
        String secretKey = "yourSecretKey";

        //Create a request and pass the required parameters into the map that exists in the form. The key is the parameter name and the value is the parameter value.
        Request request = new Request();
        request.setFormParam("orgId", "yourOrgId");
        request.setFormParam("modelId", "opentsdb_model");
        request.setFormParam("assetIds","4DXYH7nS");
        request.setFormParam("measurepoints", "opentsdb_di_point");
        request.setFormParam("startTime", "2019-06-01 00:00:00"); //For UTC time format: 2019-06-01T00:00:00+08:00
        request.setFormParam("endTime", "2019-06-11 23:00:00");   //For UTC time format: 2019-06-11T23:00:00+08:00
        request.setFormParam("ifWithUnknown", "false");
        request.setFormParam("status", "1,2");

        request.setMethod("POST");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("http://apim-gateway/tsdb-service/v2.0/di/duration")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
