# Get Asset Raw Data by Time Range



Get the original data of a specified measurepoint of a specified device within a certain period (covering AI, DI and common data types) and perform application development.

## Request Format

```
https://{apigw-address}/tsdb-service/v2.0/raw?orgId={}&modelId={}&assetIds={}&measurepoints={}&startTime={}&endTime={}&pageSize={}&accessKey={}
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    |Model ID which the asset belongs to. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)                                                                                                                                                                                                                            |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)                                                                                                                                                                           |
| startTime     | Query            | true     | String    | Sampling data start time, where UTC time format and local time format are supported.  The local time format is YYYY-MM-DD HH:MM:SS. In case of local time format, the application queries the assets by the local time of the location where the device is.  Timezone information is required for UTC time format, e.g. 2019-06-01T00:00:00+08:00; in case of UTC time format, the application queries all the assets by the unified start timestamp and end timestamp.  |
| endTime       | Query            | true     | String    |Sampling data end time. Its format must be consistent with the start time                                                                                                                                                                                                                                              |
| pageSize      | Query            | false    | Integer   |Upper limit of the returned records in a single page for a single measurepoint of a single device, which is 1000 by default. For a single query, the total returned data amount follows the following constraints:  (Number of devices  * Number of points * pagesize) ≤ 640000.                                                                                                                                                                       |
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey](/docs/api/en/latest/api_faqs.html#how-to-get-access-key-accesskey-accesskey)|                                                                     

## Request Parameters (Body)
| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|------|------------------|----------|-----------|-------------|
|      |                  |          |           |             |

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [Items](/docs/api/en/latest/tsdb_service/get_asset_raw_data_by_time_range.html#id3). |

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

## Error Codes
For description of error codes, see [Common Error Codes] (overview#errorcode).

## Sample 1

### Request Sample
Local time format:
```
https://{apigw-address}/tsdb-service/v2.0/raw?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_di_point_xxx,opentsdb_ai_point_xxx,opentsdb_generic_point_xxx&startTime=2019-06-01%2010:00:00&endTime=2019-06-11%2023:00:00&pageSize=&accessKey=accessKey
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
            "localtime": "2019-06-11 18:35:12",
            "assetId": "4DXYH7nS",
            "opentsdb_ai_point_xxx": "1.1236",
            "timestamp": 1560249312446
        },
      {
            "localtime": "6/12/2019 4:49:29 PM",
            "opentsdb_di_point_xxx": "0",
            "assetId": "4DXYH7nS",
            "timestamp": 1560329369735
        }
    ]
  }
}
```


## Sample 2

### Request Sample
UTC time format:
```
https://{apigw-address}/tsdb-service/v2.0/raw?orgId=o15504722874071&accessKey=accessKey&modelId=opentsdb_model&assetIds=4DXYH7nS&measurepoints=opentsdb_di_point_xxx,opentsdb_ai_point_xxx,opentsdb_generic_point_xxx&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00&pageSize=100
```

### Return Sample

```json
{
    "status": 0,
    "requestId": "f1ebd301ff7a4b7f8d53bcfe39ef264e",
    "msg": "success",
    "submsg": null,
    "data": {
        "data": [
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_ai_point_xxx": "1.1236",
                "timestamp": 1560249312446
            },
            {
                "localtime": null,
                "opentsdb_di_point_xxx": "0",
                "assetId": "4DXYH7nS",
                "timestamp": 1560329369735
            }
        ]
    }
}
```

## Java SDK Sample

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
public void getAssetsRawDataByTimeRangeTest(){
    
    //accessKey and secretKey correspond to AccessKey and SecretKey in EnOS
    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    // Create a new request and pass the required parameters into the Query map.
    // The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "yourOrgId");
    request.setQueryParam("modelId", "opentsdb_model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_di_point_xxx,opentsdb_ai_point_xxx,opentsdb_generic_point_xxx");
    request.setQueryParam("startTime", "2019-06-01 00:00:00"); //or in UTC format：2019-06-01T00:00:00+08:00
    request.setQueryParam("endTime", "2019-06-11 23:00:00");  //or in UTC format：2019-06-11T00:00:00+08:00
    request.setQueryParam("pageSize" , 10);
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/raw")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
