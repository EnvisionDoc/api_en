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

## Using GET Method

### Request Format

```
GET https://{apigw-address}/tsdb-service/v2.0/latest/filter
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
     - Mandatory
     - String
     - The model ID. `How to get model ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Query
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - measurepoint
     - Query
     - Mandatory
     - String
     - The measurement point ID. `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__
   * - operator
     - Query
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
     - Query
     - Mandatory
     - String
     - The value to filter for. It must be used along with the operator. The operators "eq", "nq", "gt", "ge", "lt", and "le" correspond to a single value; "between" corresponds to 2 values; "in" corresponds to multiple values. Multiple values must be separated by commas, and the data types must be consistent with those of the measurement points. For example: "operator=betwteen&valueFilter=a, b" refers to filtering out the values between a and b.
   * - timeWindow
     - Query
     - Optional
     - Integer
     - Specify the time window for filtering the latest data (by minutes). The minimum value is 0. If not specified, no constrain is applied.
   * - accessKey
     - Query
     - Optional
     - String
     - The service account for authentication purposes. `How to get the accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
   * - ifWithLocalTime
     - Query
     - Optional
     - Boolean
     -      
       + true = returns data in local time format
       + false (default) = does not return data in local time format
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
     - The list of asset data. The data returned for a single point of a single device is sorted by the data timestamp in ascending order. For more information, see `items <filter_asset_latest_data#items>`__


#### items

##### Sample

```json
{
    "assetId": "FGqRJKPM",
    "pointId": 1.5,
    "timestamp": 1559570160000
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

### Error Codes
For description of error codes, see [Common Error Codes](overview#common-error-codes).

### Samples (GET Method)

#### Request Sample
```
url: https://{apigw-address}/tsdb-service/v2.0/latest/filter?orgId=yourOrgId&assetIds=FGqRJKPM&modelId=opentsdb_model&measurepoint=pointId&timeWindow=&operator=le&valueFilter=55673.9&accessKey=accessKey

method: GET
```
In the above example, the request sample will filter out the `pointId` value of the model `opentsdb_model`, which is less than or equals to 55673.9.

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
        "assetId": "FGqRJKPM",
        "pointId": 1.5,
        "timestamp": 1559570160000
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
    public void FilterAssetLatestDataTest(){

        //1. Click Application Registration in the left navigation of the EnOS Management Console.
        //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
        String accessKey = "yourAccessKey";
        String secretKey = "yourSecretKey";

        //Create a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
        Request request = new Request();
        request.setQueryParam("orgId", "yourOrgId");
        request.setQueryParam("timeWindow", 10);
        request.setQueryParam("operator", "le");
        request.setQueryParam("modelId", "opentsdb_model");
        request.setQueryParam("valueFilter", 666.6);
        request.setQueryParam("assetIds","4DXYH7nS");
        request.setQueryParam("measurepoint", "opentsdb_pi_point");

        request.setMethod("GET");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("http://apim-gateway/tsdb-service/v2.0/latest/filter")
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
POST https://{apigw-address}/tsdb-service/v2.0/latest/filter
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
     - Mandatory
     - String
     - The model ID. `How to get model ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`__
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - measurepoint
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
   * - accessKey
     - Optional
     - String
     - The service account for authentication purposes. `How to get the accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
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

### Response Parameters

Refer to the description in [Response Parameters](filter_asset_latest_data#response-parameters-response) of the **Using GET Method** section.

### Error Codes
For the description of error codes, see [Common Error Codes](overview#common-error-codes).

### Samples (POST Method)

#### Request Sample
```
url: https://{apigw-address}/tsdb-service/v2.0/latest/filter

method: POST

Content-Type: multipart/form-data;charset=UTF-8

requestBody:
{
  "orgId": "yourOrgId",
  "modelId": "opentsdb_model",
  "assetIds": "FGqRJKPM",
  "pointId": "pointId",
  "operator": "le",
  "valueFilter": "55673.9",
  "accessKey": "accessKey"
}
```

Where, `operator=le&valueFilter=55673.9` means that: The following sample will filter out the `pointId` value of the model `opentsdb_model`, which is less than or equal to 55673.9.

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
        "assetId": "FGqRJKPM",
        "pointId": 1.5,
        "timestamp": 1559570160000
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
    public void FilterAssetLatestDataTest(){

        //1. Click Application Registration in the left navigation of the EnOS Management Console.
        //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
        String accessKey = "yourAccessKey";
        String secretKey = "yourSecretKey";

        //Create a request and pass the required parameters into the map that exists in the form. The key is the parameter name and the value is the parameter value.
        Request request = new Request();
        request.setFormParam("orgId", "yourOrgId");
        request.setFormParam("timeWindow", "10");
        request.setFormParam("operator", "le");
        request.setFormParam("modelId", "opentsdb_model");
        request.setFormParam("valueFilter", "666.6");
        request.setFormParam("assetIds","4DXYH7nS");
        request.setFormParam("measurepoint", "opentsdb_pi_point");

        request.setMethod("POST");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("http://apim-gateway/tsdb-service/v2.0/latest/filter")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
