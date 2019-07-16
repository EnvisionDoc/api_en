# Get Points TSDB Meta Data



Get the TSDB storage policy corresponding to the model measurement point. A measurement point may have multiple storage policies, depending on its data type and usage. This API returns all the TSDB storage policy metadata in the current OU for the specified measurement point.

## Request Format

```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId={}&modelIds={}&measurepoints={}
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)|
| modelIds       | Query            | true    | String    |Model ID which the asset belongs to. Multi-model query is supported, and multiple modelIds are separated by commas. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)|
| measurepoints | Query            | false     | String    | Asset measurement point. It is supported to query multiple measurement points, and all the measurement points are separated by commas; the upper limit for query is 3000 (Number of devices *Number of measurement points). [How to get pointId](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid)                                                                                                                                                                           |
                                              


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | `List<Object>` | List of asset data. The data returned for a single point of a single device, sorting by time in ascending order. Parameters are stored in the Object structure. See [items](/docs/api/en/latest/tsdb_policy/get_points_tsdb_meta_data.html#id3). |


### items


| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| modelId     | String    | Model ID|
| tsdb_metadata   |  `List<Object>`    | Set of model measurement point storage policies. For details, see [Policy](/docs/api/en/latest/tsdb_policy/get_points_tsdb_meta_data.html#id4)。  |

### policy

The following sample shows that the measurement point opentsdb_ai_point_xxx has the storage policies AI_RAW (AI raw data) and AI_NORMALIZED (AI minute-level normalized data):

```json
"opentsdb_ai_point_xxx": [       	
          "AI_RAW", 						 
          "AI_NORMALIZED"
        ]
```

| Name | Data Type | Description |
|---------------|-----------|--------------------------------------|
| point     | Object    | Measurement point storage policy. One measurement point can have multiple policies, and the policies are stored in arrays |

## Error Codes
For description of error codes, see [Common Error Codes](overview#errorcode).

## Sample 1

### Request Sample
Measurement point is not specified:
```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=o15504722874071&modelIds=opentsdb_model_xxx&measurepoints=
```

### Return Sample

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

### Request Sample
Measurement point is specified:
```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=o15504722874071&modelIds=opentsdb_model_xxx&measurepoints=opentsdb_di_point_xxx
```

### Return Sample

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
  public void getPointsTSDBMetaDataTest(){
      
      //accessKey and secretKey correspond to AccessKey and SecretKey in EnOS.
      String accessKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
      String secretKey = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

      
      //New a request and pass the required parameters into the map that exists in the query. The key is the parameter name and the value is the parameter value.
      Request request = new Request();
      request.setQueryParam("orgId", "yourOrgId");
      request.setQueryParam("modelIds", "model_xxx");
      request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");

      request.setMethod("GET");

      try {
          EnOSResponse<JSONObject> response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                  .url("http://apim-gateway/tsdb-policy/v2.0/policies")
                  .getResponse(request, EnOSResponse.class);
          System.out.println(response);
      } catch (Exception e) {
          e.printStackTrace();
      }
  }
```
