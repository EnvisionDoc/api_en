# Get Asset AI Data with Aggregation Logic



Get the original AI data of a specified measurement point of a specified device within a certain period.

## Request Format

```
https://{apigw-address}/tsdb-service/v2.0/ai-normalized?orgId={}&modelId={}&assetIds={}&measurepointsWithLogic={}&interval={}&startTime={}&endTime={}&pageSize={}&accessKey={}
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    |Model ID which the asset belongs to. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)                                                                                                                                                                                                                           |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId](/docs/api/en/latest/api_faqs#how-to-get-asset-id-assetid-assetid)                                                                                                                                                                                |
| measurepointsWithLogic | Query            | true     | String    | Measurement point data aggregation logic. The supported aggregation calculation methods include count, avg, sum, max, min, first, and last. <br>The time interval for the aggregation query is `[startTime, endTime)`, that is, the aggregation operand contains the data at the time of `startTime`, but does not contain the data at the time of `endTime`; <br> The upper limit of the number of measurement points that can be queried is 3000. Format: Function (measurepoint identifier), e.g. sum(pointId). [How to get pointId](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)|
| interval       | Query            | true     | Integer    | Time interval for the aggregation algorithm to work. The effective value is 0-1440, calculated in minutes. If the interval value is 0, the measurement point has no aggregation logic; if the interval value is greater than 0, the measurement point must have the aggregation logic. |
| startTime     | Query            | true     | String    | Time of start sampling data, where UTC time format and local time format are supported. The local time format is YYYY-MM-DD HH:MM:SS. In case of local time format, the application queries the assets by the local time of the location where the device is.  Timezone information is required for UTC time format, e.g. 2019-06-01T00:00:00+08:00; in case of UTC time format, the application queries all the assets by the unified start timestamp and end timestamp.  |
| endTime       | Query            | true     | String    | Time of stop sampling data. Its format must be consistent with the start time|
| pageSize      | Query            | false    | Integer   |Upper limit of the returned records in a single page for a single measurement point of a single device, which is 1000 by default. For a single query, the total returned data amount follows the following constraints: ((Number of devices  * Number of points * pagesize) ≤ 640000.|
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey](/docs/api/en/latest/api_faqs.html#how-to-get-access-key-accesskey-accesskey)|                                                                                                           
## Request Parameters (Body)
| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|------|------------------|----------|-----------|-------------|
|      |                  |          |           |             |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [items](/docs/api/en/latest/tsdb_service/get_asset_ai_data_with_aggregation_logic.html#id3).

### items

Sample:

```json
{
    "sum(opentsdb_ai_point_xxx)": "4.4944",  	 //measurement point identifier (with or without aggregation logic) and the data
    "assetId": "4DXYH7nS",						 //asset ID
    "timestamp": 1560249300000, 				 //UNIX data timestamp
    "localtime": "2019-06-11 18:35:00"			 //local time mark of data
}
```


| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| localtime     | Object    |  Local time mark of data, which is accurate to seconds. When the incoming time format is UTC, the value is null.  |
| assetId       | Object    | Asset ID.                                                       |
| pointIdWithLogic | Object    | Measurement point identifier (with or without aggregation logic)                                    |
| timestamp     | Object    | Data timestamp (UNIX time, accurate to second).                                     |

## Error Codes
For description of error codes, see [Common Error Codes](overview#errorcode).

## Sample 1

### Request Sample
Local time format:
```
https://{apigw-address}/tsdb-service/v2.0/ai-normalized?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepointsWithLogic=sum(opentsdb_ai_point_xxx)&interval=10&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&pageSize=&accessKey=accessKey
```

### Return Sample

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": null,
  "data": {
    "items": [
      {
        "sum(opentsdb_ai_point_xxx)": "4.4944",
        "assetId": "4DXYH7nS",
        "timestamp": 1560249300000,
        "localtime": "6/11/2019 6:35:00 PM"
      },
      {
        "sum(opentsdb_ai_point_xxx)": "6.0",
        "assetId": "4DXYH7nS",
        "timestamp": 1560257100000,
        "localtime": "6/11/2019 8:45:00 PM"
      }
    ]
  }
}
```


## Sample 2

### Request Sample
UTC time format:
```
https://{apigw-address}/tsdb-service/v2.0/ai-normalized?accessKey=accessKey&assetIds=4DXYH7nS&pageSize=5000&interval=10&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00&orgId=o15504722874071&measurepointsWithLogic=sum(opentsdb_ai_point_xxx)
```

### Return Sample

```json
{
    "status": 0,
    "requestId": "c1389544667049319ac1820517f6f501",
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "localtime": null,
                "sum(opentsdb_ai_point_xxx)": "4.4944",
                "assetId": "4DXYH7nS",
                "timestamp": 1560249300000
            },
            {
                "localtime": null,
                "sum(opentsdb_ai_point_xxx)": "6.0",
                "assetId": "4DXYH7nS",
                "timestamp": 1560257100000
            }
        ]
    }
}
```

## Java SDK Sample

```java
private static class Request extends PoseidonRequest{

    public void setQueryParam(String key, Object value){
        queryParams().put(key, value);
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
public void getAssetsAINormalizedDataTest(){
    
    //1. Click Application Registration in the left navigation of the EnOS Console.
    //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.

    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    //New a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "yourOrgId");
    request.setQueryParam("modelId", "opentsdb_model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepointsWithLogic", "sum(opentsdb_ai_point_xxx)"); //sum() is an aggregate function
    request.setQueryParam("interval", 10);
    request.setQueryParam("startTime", "2019-06-01 00:00:00"); //or in UTC format：2019-06-01T00:00:00%2B08:00
    request.setQueryParam("endTime", "2019-06-11 23:00:00");  //or in UTC format：2019-06-11T23:00:00%2B08:00
    request.setQueryParam("pageSize" , 10);
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        EnOSResponse<JSONObject> response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/ai-normalized")
                .getResponse(request, EnOSResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
