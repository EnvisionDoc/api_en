# Get Points TSDB Meta Data

*Note: This documentation is in the progress of translation. Thanks for your visit!*

Get the TSDB storage policy corresponding to the model measurepoint. A measurepoint may have multiple storage policies, depending on its data type and usage. This API returns all the TSDB storage policy metadata in the current OU for the specified measurepoint.

## Request format

```
https://{apigw-address}/tsdb-service/v2.0/policies?orgId={}&modelIds={}&assetIds={}&measurepoints={}&startTime={}&endTime={}&pageSize={}&accessKey={}
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)|
| modelIds       | Query            | false    | String    |Model ID which the asset belongs to. Multi-model query is supported, and multiple modelIds are separated by commas. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-modeid-information-modeid)|
| measurepoints | Query            | true     | String    | Asset measurepoint. It is supported to query multiple measurepoints, and all the measurepoints are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurepoints). [How to get pointId information](/docs/api/en/latest/api_faqs#how-to-get-the-measurepoint-pointid-information-pointid)                                                                                                                                                                           |
                                              


## Response parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | `List<Object>` | List of asset data. The data returned for a single point of a single device is sorted by time in ascending order. Parameters are stored in the Object structure. See [Items](/docs/api/en/latest/tsdb_policy/get_points_tsdb_meta_data.html#id3). |


### items


| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| modelId     | String    | Model ID|
| tsdb_metadata   |  `List<Object>`    | Set of model measurepoint storage policies. For details, see [Policy](/docs/api/en/latest/tsdb_policy/get_points_tsdb_meta_data.html#id4)。  |

### policy

The following sample shows that the measurepoint opentsdb_ai_point_xxx has the storage policies AI_RAW (AI raw data) and AI_NORMALIZED (AI minute-level normalized data):

```
"opentsdb_ai_point_xxx": [                        				
          "AI_RAW", 									
          "AI_NORMALIZED"
        ]
```
| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| pointId     | Object    | Measurepoint storage policy. One measurepoint can have multiple policies, and the policies are stored in arrays |

## Error codes
For description of error codes, see [Common Error Codes] (overview#errorcode).

## Sample 1

### Request sample
Measurepoint not specified:
```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=o15504722874071&modelIds=opentsdb_model_xxx&measurepoints=
```

### Return sample

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": "success",
  "data": [
    {
      "tsdb_metadata": {
        "opentsdb_di_point_xxx": [
          "DI"
        ],
        "opentsdb_pi_point_xxx": [
          "PI"
        ],
        "opentsdb_ai_point_xxx": [
          "AI_RAW",
          "AI_NORMALIZED"
        ],
        "opentsdb_generic_point_xxx": [
          "GENERIC"
        ]
      },
      "modelId": "opentsdb_model_xxx"
    }
  ]
}
```


## Sample 2

### Request sample
Measurepoint specified:
```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=o15504722874071&modelIds=opentsdb_model_xxx&measurepoints=opentsdb_di_point_xxx
```

### Return sample

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": "success",
  "data": [
    {
      "tsdb_metadata": {
        "opentsdb_di_point_xxx": [
          "DI"
        ]
      },
      "modelId": "opentsdb_model_xxx"
    }
  ]
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
  public void getPointsTSDBMetaDataTest(){
      
      //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
      String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
      String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

      // Create a new request and pass the required parameters into the Query map.
      // The key is the parameter name and the value is the parameter value.
      Request request = new Request();
      request.setQueryParam("orgId", "o15504745674071");
      request.setQueryParam("modelIds", "model_xxx");
      request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");

      request.setMethod("GET");

      try {
          JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                  .url("http://apim-gateway/tsdb-policy/v2.0/policies")
                  .getResponse(request, JSONObject.class);
          System.out.println(response);
      } catch (Exception e) {
          e.printStackTrace();
      }
  }
```
