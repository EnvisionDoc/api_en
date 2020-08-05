# Get Asset Generic Data

Get the generic data of specified measurement points of specified devices within a certain period.

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
GET https://{apigw-address}/tsdb-service/v2.0/generic
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
     - The organization ID which the asset belongs to. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - modelId
     - Query
     - Optional
     - String
     - The model ID. `How to get model ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Query
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - measurepoints
     - Query
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 3,000 (number of devices * number of measurement points). `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
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
   * - pageSize
     - Query
     - Optional
     - Integer
     - The upper limit of the returned records in a single page for a single measurement point of a single device, which is 1,000 by default. For a single query, the total returned data amount follows the constraint: (Number of devices  * Number of points * pagesize) ≤ 640,000.
   * - accessKey
     - Query
     - Optional
     - String
     - The service account for authentication purposes. `How to get the accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
   * - withQuality
     - Query
     - Optional
     - Boolean
     -      
       + true = the quality indicator is included in the response
       + false = default, the quality indicator is not included in the response
   * - localTimeAccuracy
     - Query
     - Optional
     - Boolean
     -      
       + true = query returns data with millisecond time stamp
       + false (default) = query returns data without millisecond time stamp

### Response Parameters <response>

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<JSONObject>
     - The list of asset data. The data returned for a single point of a single device is sorted by the data time stamp in ascending order. For more information, see   `items <get_asset_generic_data#items>`__

#### items

##### Sample

```json
{
        "assetId": "4DXYH7nS",         
        "timestamp": 1560249312446,   
        "localtime": "6/11/2019 6:35:12 PM",
        "opentsdb_generic_point": 1.1236,
        "quality": "0"
}
```

##### Parameters

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
     - The data timestamp in local time format (accurate to the second). If UTC time format is used when specifying the ``statTime`` and ``endtime``, this value will be null.
   * - quality
     - String
     - The quality indicator of the measurement point data.

### Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

### Sample 1 (GET Method)

#### Request Sample
Local time format:
```
url: https://{apigw-address}/tsdb-service/v2.0/generic?orgId=yourOrgId&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_generic_point&startTime=2019-06-01%2010:18:00&endTime=2019-06-11%2018:37:00&pageSize=&accessKey=accessKey

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
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312446,
        "localtime": "2019-06-11 18:35:12",
        "opentsdb_generic_point": 3.123
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249332446,
        "localtime": "2019-06-11 6:35:32 PM",
        "opentsdb_generic_point": 3.123
      }
    ]
  }
}
```


### Sample 2 (GET Method)

#### Request Sample
UTC time format:
```
url: https://{apigw-address}/tsdb-service/v2.0/generic?assetIds=4DXYH7nS&measurepoints=opentsdb_generic_point&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00&pageSize=100&accessKey=accessKey&orgId=yourOrgId

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
        "data": [
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_generic_point": 3.123,
                "timestamp": 1560249312446
            },
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_generic_point": 3.123,
                "timestamp": 1560249332446
            }
        ]
    }
}
```


### Sample 3 (GET Method)

#### Request Sample

Request with quality indicator:

```
url: https://{apigw-address}/tsdb-service/v2.0/ai?orgId=yourOrgId&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_generic_point&startTime=2019-06-01%2010:00:00&endTime=2019-06-11%2023:00:00&pageSize=&accessKey=accessKey&withQuality=true

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
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312446,
        "opentsdb_generic_point": 1.1236,
        "localtime": "2019-06-11 18:35:12",
        "quality": "0"
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249332446,
        "opentsdb_generic_point": 1.1236,
        "localtime": "2019-06-11 18:35:32",
        "quality": "0"
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
    public void GetAssetGenericDataTest(){

        //1. Click Application Registration in the left navigation of the EnOS Management Console.
        //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
        String accessKey = "yourAccessKey";
        String secretKey = "yourSecretKey";

        //Create a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
        Request request = new Request();
        request.setQueryParam("orgId", "yourOrgId");
        request.setQueryParam("modelId", "opentsdb_model");
        request.setQueryParam("assetIds","4DXYH7nS");
        request.setQueryParam("measurepoints", "opentsdb_generic_point");
        request.setQueryParam("startTime", "2019-06-01 00:00:00"); //For UTC time format: 2019-06-01T00:00:00+08:00
        request.setQueryParam("endTime", "2019-06-11 23:00:00");   //For UTC time format: 2019-06-11T23:00:00+08:00

        request.setMethod("GET");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("http://apim-gateway/tsdb-service/v2.0/generic")
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
POST https://{apigw-address}/tsdb-service/v2.0/generic
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
     - The organization ID which the asset belongs to. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - modelId
     - Optional
     - String
     - The model ID. `How to get model ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - measurepoints
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 3,000 (number of devices * number of measurement points). `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
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
   * - accessKey
     - Optional
     - String
     - The service account for authentication purposes. `How to get the accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
   * - withQuality
     - Optional
     - Boolean
     -      
       + true = the quality indicator is included in the response
       + false = the quality indicator is not included in the response
   * - localTimeAccuracy
     - Optional
     - Boolean
     -      
       + true = query returns data with millisecond time stamp
       + false (default) = query returns data without millisecond time stamp

### Response Parameters

See description in [Response Parameters](get_asset_generic_data#response-parameters-response) of the **Using GET Method** section.

### Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

### Sample 1 (POST Method)

#### Request Sample
Local time format:
```
url: https://{apigw-address}/tsdb-service/v2.0/generic

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
{
  "orgId": "yourOrgId",
  "assetIds": "4DXYH7nS",
  "measurepoints": "opentsdb_generic_point",
  "startTime": "2020-04-20 00:00:00",
  "endTime": "2020-04-21 00:00:00",
  "pageSize": 1000,
  "accessKey": "accessKey"
}
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
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312446,
        "localtime": "2019-06-11 18:35:12",
        "opentsdb_generic_point": 3.123
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249332446,
        "localtime": "2019-06-11 6:35:32 PM",
        "opentsdb_generic_point": 3.123
      }
    ]
  }
}
```


### Sample 2 (POST Method)

#### Request Sample
UTC time format:
```
url: https://{apigw-address}/tsdb-service/v2.0/generic

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
{
  "orgId": "yourOrgId",
  "assetIds": "4DXYH7nS",
  "measurepoints": "opentsdb_generic_point",
  "startTime": "2019-06-01T00:00:00%2B08:00",
  "endTime": "2019-06-11T23:00:00%2B08:00",
  "pageSize": 1000,
  "accessKey": "accessKey"
}
```

#### Return Sample

```json
{
    "status": 0,
    "requestId": null,
    "msg": "success",
    "submsg": null,
    "data": {
        "data": [
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_generic_point": 3.123,
                "timestamp": 1560249312446
            },
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_generic_point": 3.123,
                "timestamp": 1560249332446
            }
        ]
    }
}
```


### Sample 3 (POST Method)

#### Request Sample

Request with quality indicator:

```
url: https://{apigw-address}/tsdb-service/v2.0/generic

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
{
  "orgId": "yourOrgId",
  "assetIds": "4DXYH7nS",
  "measurepoints": "opentsdb_generic_point",
  "startTime": "2019-06-01 00:00:00",
  "endTime": "2019-06-11 23:00:00",
  "pageSize": 1000,
  "accessKey": "accessKey",
  "withQuality": true
}
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
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312446,
        "opentsdb_generic_point": 1.1236,
        "localtime": "2019-06-11 18:35:12",
        "quality": "0"
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249332446,
        "opentsdb_generic_point": 1.1236,
        "localtime": "2019-06-11 18:35:32",
        "quality": "0"
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
    public void GetAssetGenericDataTest(){

        //1. Click Application Registration in the left navigation of the EnOS Management Console.
        //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
        String accessKey = "yourAccessKey";
        String secretKey = "yourSecretKeyP";

        //Create a request and pass the required parameters into the map that exists in the form. The key is the parameter name and the value is the parameter value.
        Request request = new Request();
        request.setFormParam("orgId", "yourOrgId");
        request.setFormParam("modelId", "opentsdb_model");
        request.setFormParam("assetIds", "4DXYH7nS");
        request.setFormParam("measurepoints", "opentsdb_generic_point");
        request.setFormParam("startTime", "2019-06-01 00:00:00"); //For UTC time format: 2019-06-01T00:00:00+08:00
        request.setFormParam("endTime", "2019-06-11 23:00:00");   //For UTC time format: 2019-06-11T23:00:00+08:00

        request.setMethod("POST");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("http://apim-gateway/tsdb-service/v2.0/generic")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
