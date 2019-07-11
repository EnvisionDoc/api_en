# Get Asset DI Data



Get the status (DI) data of a specified device within a certain period.

The API captures the state data for a particular asset over a period of time and returns only data that reflects changes in the state of the asset. For example, the raw data within a period is given as follows:

```
Time       Status
10:01:14    0
10:01:30    0
10:03:45    0
10:12:23    1
10:13:34    0
10:15:24    1
10:17:25    1
```

The returned results are given as follows:

```
Time       Status
10:01:14    0
10:12:23    1
10:13:34    0
10:15:24    1
```

## Request format

```
https://{apigw-address}/tsdb-service/v2.0/di?orgId={}&modelId={}&assetIds={}&measurepoints={}&startTime={}&endTime={}&accessKey={}
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    |Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                                                                                                                                                                                                                            |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId information](/docs/api/en/latest/api_faqs#how-to-get-the-measurepoint-pointid-information-pointid)                                                                                                                                                                           |
| startTime     | Query            | true     | String    | Sampling data start time, where UTC time format and local time format are supported.  The local time format is YYYY-MM-DD HH:MM:SS. In case of local time format, the application queries the assets by the local time of the location where the device is.  Timezone information is required for UTC time format, e.g. 2019-06-01T00:00:00+08:00; in case of UTC time format, the application queries all the assets by the unified start timestamp and end timestamp.  |
| endTime       | Query            | true     | String    |Sampling data end time. Its format must be consistent with the start time                                                                                                                                                                                                                                              |
| pageSize      | Query            | false    | Integer   |Upper limit of the returned records in a single page for a single measurepoint of a single device, which is 1000 by default. For a single query, the total returned data amount follows the following constraints:  (Number of devices  * Number of points * pagesize) ≤ 640000.                                                                                                                                                                       |
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey information](/docs/api/en/latest/api_faqs.html#how-to-get-accesskey-information-accesskey)|                                                                     


## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [Items](/docs/api/en/latest/tsdb_service/get_asset_di_data.html#id3).

### items

Sample:
```json
{
        "assetId": "4DXYH7nS",  			      
        "timestamp": 1560249312446,			  
        "opentsdb_ai_point_xxx": "1.1236", 	
        "localtime": "6/11/2019 6:35:12 PM"	 
}
```

| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| localtime     | Object    |  Local time mark of data, which is accurate to seconds. When the incoming time format is UTC, the value is null.  |
| assetId       | Object    | Asset ID.                                              |
| pointId | Object    |This parameter is a variable, indicating the identifier and data for the measurepoint.                                     |
| timestamp     | Object    | Data timestamp (UNIX time, accurate to second).                                     |

## Error codes
For description of error codes, see [Common Error Codes] (overview#errorcode).

## Sample 1

### Request sample
Local time format:
```
https://{apigw-address}/tsdb-service/v2.0/di?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_di_point_xxx&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&accessKey=accessKey
```

### Return sample

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
        "opentsdb_di_point_xxx": "0",
        "timestamp": 1560249312446,
        "localtime": "6/11/2019 6:35:12 PM"
      }
    ]
  }
}

```


## Sample 2

### Request sample
UTC time format:
```
https://{apigw-address}/tsdb-service/v2.0/di?accessKey=accessKey&assetIds=4DXYH7nS&orgId=o15504722874071&measurepoints=opentsdb_di_point_xxx&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00
```

### Return sample

```json
{
    "status": 0,
    "requestId": "088a4bdc14ff4e1a8882a814ab539a9f",
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "localtime": null,
                "opentsdb_di_point_xxx": "0",
                "assetId": "4DXYH7nS",
                "timestamp": 1560249312446
            }
        ]
    }
}

```

## Java SDK invocation sample

```java
private static class Request extends PoseidonRequest{

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
public void getAssetsStatusDataTest(){
    
    //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
    String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    // Create a new request and pass the required parameters into the Query map.
    // The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("modelId", "opentsdb_model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_di_point_xxx"); 
    request.setQueryParam("startTime", "2019-06-01 00:00:00"); //or in UTC format：2019-06-01T00:00:00+08:00
    request.setQueryParam("endTime", "2019-06-11 23:00:00");  //or in UTC format：2019-06-11T00:00:00+08:00
    request.setQueryParam("accessKey", appKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/di")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
