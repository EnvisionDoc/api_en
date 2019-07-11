# Filter Asset Latest Data

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Filter and query the latest data of a single measurepoint for multiple devices Numeric and String supported as the data types for query.

## Request format

```
https://{apigw-address}/tsdb-service/v2.0/latest/filter?orgId={}modelId={}assetIds={}measurepoints={}timeWindow={}operator={}valueFilter={}accessKey={}
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    |Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                                                                                                                                                                                                                            |
| assetIds      | Query            | true     | String    | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId information](/docs/api/en/latest/api_faqs#how-to-get-the-measurepoint-pointid-information-pointid)                                                                                                                                                                           |
| timeWindow     | Query            | false     | Integer  | Returns the data schedule setting. Its unit is minute and its minimum value is 0; no filtering is applied in case of no transfer. |
| operator       | Query            | false     | String    | Operator. It supports: eq: equal to; nq: not equal; gt: greater than; lt: less than; ge: greater than or equal; le: less than or equal; between: interval of 2 values; in: one of multiple values.                                                                                                                                      |
| valueFilter      | Query            | false    | String   |Range value. It needs to be used along with the operator. The operators eq, nq, gt, ge, lt, and le correspond to a single value; between corresponds to 2 values; in corresponds to multiple values. Multiple values should be separated by commas, and the data types must be consistent with those of the measurepoints. For example: operator=betwteen&valueFilter=a, b refers to filtering out the values between a and b.                                                                    |
| accessKey     | Query            | true     | String    |Service account of the application. The application authenticates with `accessKey` to obtain the data that it is authorized to access. [How to get accessKey information](/docs/api/en/latest/api_faqs.html#how-to-get-accesskey-information-accesskey)|                                                                     

## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [Items] (/docs/api/en/latest/tsdb_service/filter_asset_latest_data.html#id2).

### items

Sample:
```json
{
    "assetId": "FGqRJKPM", 		
    "pointId": 1.5,   			
    "timestamp": 1559570160000	
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
```
https://{apigw-address}/tsdb-service/v2.0/latest/filter?orgId=o15528761854851&assetIds=FGqRJKPM&modelId=model_xxx&measurepoint=pointId&timeWindow=&operator=le&valueFilter=55673.9&accessKey=accessKey
```
Where, `operator=le&valueFilter=55673.9` means that: The following sample will filter out the value of the `pointId` data point of the model `model_xxx` that is less than or equal to 55673.9.

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
        "assetId": "FGqRJKPM",
        "pointId": 1.5,
        "timestamp": 1559570160000
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
public void filterAssetsLatestDataTest(){
    
    //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
    String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    // Create a new request and pass the required parameters into the Query map.
    // The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("timeWindow", 10);
    request.setQueryParam("operator", "le");
    request.setQueryParam("modelId", "model_xxx");
    request.setQueryParam("valueFilter", 666.6);
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", appKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/latest/filter")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
