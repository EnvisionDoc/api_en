# Get Asset Current Day Electric Power



Get the accumulated power consumption data of a specified device from 00:00 (local time) to current time.

## Request Format

```
https://{apigw-address}/tsdb-service/v2.0/electric-power/current-day?orgId={}&modelId={}&assetIds={}&measurepoints={}&accessKey={}
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid) |
| modelId       | Query            | false    | String    |Model ID which the asset belongs to. [How to get modelID>>](/docs/api/en/2.0.9/api_faqs#how-to-get-model-id-modelid-modelid) |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| measurepoints | Query            | true     | String    | Asset measurement point. It is supported to query multiple measurement points, and all the measurement points are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurement points). [How to get pointId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-the-measuremet-point-pointid-pointid) |
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-access-key-accesskey-accesskey)|                                                                     

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object struct. See [items](/docs/api/en/2.0.9/tsdb_service/get_asset_current_day_electric_power.html#id3). |

### items

Sample:
```json
{
        "assetId": "4DXYH7nS", 			//asset ID			
        "timestamp": 1560329220000,			//UNIX data timestamp	        
        "opentsdb_pi_point_xxx": "10.615000000000002" //measurement point identifier and the data, here is the daily aggregation of the sum of power pi
}
```

| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| assetId       | Object    | Asset ID |
| pointId | Object    |This parameter is a variable, indicating the identifier and data for the measurement point.  The data here is the daily aggregation of the sum of power pi.                                   |
| timestamp     | Object    | Data timestamp (UNIX time, accurate to second) |

## Error Codes
For description of error codes, see [Common Error Codes](overview#errorcode).

## Sample

### Request Sample
```
https://{apigw-address}/tsdb-service/v2.0/electric-power/current-day?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_pi_point_xxx&accessKey=accessKey
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
        "timestamp": 1560329220000,
        "sum(opentsdb_pi_point_xxx)": "10.615000000000002"
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
public void getAssetsCurrentDayElectricPowerTest(){
    
    //1. Click Application Registration in the left navigation of the EnOS Console.
    //2. Click the application that needs to call the API, and click Basic Information. accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
    String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    //New a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "yourOrgId");
    request.setQueryParam("modelId", "model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", accessKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/electric-power/current-day")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
