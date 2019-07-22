# Get Asset Latest Data



Get the latest data of all measurement points of a specified device.

## Request Format

```
https://{apigw-address}/tsdb-service/v2.0/latest?orgId={}&assetIds={}&measurepoints={}&timeWindow={}&accessKey={}
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                                                                                                                                                                                                                            |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | Asset measurement point. It is supported to query multiple measurement points, and all the measurement points are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurement points). [How to get pointId](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)                                                                                                                                                                           |
| timeWindow | Query            | false     | Integer    | Returns the data schedule setting. Its unit is minute and its minimum value is 0; no constrain is applied if it is not in the request|
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey](/docs/api/en/latest/api_faqs.html#how-to-get-access-key-accesskey-accesskey)|                                                                     


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [items](/docs/api/en/latest/tsdb_service/get_asset_latest_data.html#id3).

### items

Sample:
```json
{
        "assetId": "4DXYH7nS",  			//asset ID       
        "opentsdb_pi_point_xxx": "1.1236", 	   //measurement point identifier and the data   
        "timestamp": 1560249312446		//UNIX data timestamp    
}
```

| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| assetId       | Object    | Asset ID.                                              |
| pointId | Object    |This parameter is a variable, indicating the identifier and data for the measurement point.                                     |
| timestamp     | Object    | Data timestamp (UNIX time, accurate to second).                                     |

## Error Codes
For description of error codes, see [Common Error Codes](overview#errorcode).

## Sample 1

### Request Sample
Local time format:
```
https://{apigw-address}/tsdb-service/v2.0/latest?orgId=o15528761854851&assetIds=4DXYH7nS&measurepoints=opentsdb_pi_point_xxx&timeWindow=&accessKey=accessKey
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
        "assetId": "4DXYH7nS",
        "opentsdb_pi_point_xxx": 2.123,
        "timestamp": 1560249532446
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
public void getAssetsLatestDataTest(){
    
    //1. Click Application Registration in the left navigation of the EnOS Console.
    //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    //New a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "yourOrgId");
    request.setQueryParam("timeWindow", 10);
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/latest")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
