# Get Asset Latest Data

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Get the latest data of all measurepoints of a specified device.

## Request format

```
https://{apigw-address}/tsdb-service/v2.0/latest?orgId={}&assetIds={}&measurepoints={}&timeWindow={}&accessKey={}
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                                                                                                                                                                                                                            |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId information](/docs/api/en/latest/api_faqs#how-to-get-the-measurepoint-pointid-information-pointid)                                                                                                                                                                           |
| timeWindow | Query            | false     | Integer    | Returns the data schedule setting. Its unit is minute and its minimum value is 0; no constrain is applied in case of no transfer.                                                                                                                                                                            |
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey information](/docs/api/en/latest/api_faqs.html#how-to-get-accesskey-information-accesskey)|                                                                     


## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [Items](/docs/api/en/latest/tsdb_service/get_asset_latest_data.html#id3).

### items

Sample:
```json
{
        "assetId": "4DXYH7nS",  			       
        "opentsdb_pi_point_xxx": "1.1236", 	      
        "timestamp": 1560249312446		     
}
```

| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| assetId       | Object    | Asset ID.                                              |
| pointId | Object    |This parameter is a variable, indicating the identifier and data for the measurepoint.                                     |
| timestamp     | Object    | Data timestamp (UNIX time, accurate to second).                                     |

## Error codes
For description of error codes, see [Common Error Codes] (overview#errorcode).

## Sample 1

### Request sample
Local time format:
```
https://{apigw-address}/tsdb-service/v2.0/latest?orgId=o15528761854851&assetIds=4DXYH7nS&measurepoints=opentsdb_pi_point_xxx&timeWindow=&accessKey=accessKey
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
        "opentsdb_pi_point_xxx": 2.123,
        "timestamp": 1560249532446
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
public void getAssetsLatestDataTest(){
    
    //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
    String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    // Create a new request and pass the required parameters into the Query map.
    // The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("timeWindow", 10);
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", appKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/latest")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
