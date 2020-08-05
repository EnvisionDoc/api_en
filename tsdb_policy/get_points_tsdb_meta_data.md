# Get Measurement Point TSDB Metadata

Get the TSDB storage policy corresponding to the model measurement point. A measurement point may have multiple storage policies, depending on its data type and usage. This API returns all the TSDB storage policy metadata in the current organization for the specified measurement point.

## Request Format

```
GET https://{apigw-address}/tsdb-policy/v2.0/policies
```

## Request Parameters (URI)

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
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__
   * - modelIds
     - Query
     - Mandatory
     - String
     - The model ID. Supports the query of multiple model IDs, separated by commas. `How to get modelId>> </docs/api/en/2.1.0/api_faqs#modelid-modelid>`__
   * - measurepoints
     - Query
     - Optional
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 3,000 (Number of devices * Number of measurement points). `How to get pointId>> </docs/api/en/2.1.0/api_faqs#pointid-pointid>`__                                                                                                                                                                                                   

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<JSONObject>
     - The TSDB storage policy of the specified model and measurement points. For more information, see `TSDB Policy Struct <get_points_tsdb_meta_data#tsdb-policy-struct>`__

### TSDB Policy Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - modelId
     - String
     - The model ID.
   * - tsdb_metadata
     - List<JSONObject>
     - The list of model measurement points. One measurement point can have multiple policies, and the policies are stored in arrays. For more information, see `Policy Struct <get_points_tsdb_meta_data#policy-struct>`__

### Policy Struct

#### Sample

The following sample shows that the measurement point opentsdb_ai_point has the storage policies AI_RAW (AI raw data) and AI_NORMALIZED (AI minute-level normalized data):

```json
"opentsdb_ai_point": [       	
  "AI_RAW", 						 
  "AI_NORMALIZED"
]
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - point
     - Arrary
     - A list of measurement point storage policies.

## Error Codes

For description of error codes, see [Common Error Codes](overview#common-error-codes).

## Sample 1

### Request Sample

Measurement point is not specified:

```
url: https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=yourOrgId&modelIds=opentsdb_model

method: GET
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
        "opentsdb_di_point": [
          "DI"
        ],
        "opentsdb_pi_point": [
          "PI"
        ],
        "opentsdb_ai_point": [
          "AI_RAW",
          "AI_NORMALIZED"
        ],
        "opentsdb_generic_point": [
          "GENERIC"
        ]
      },
      "modelId": "opentsdb_model"
    }
  ]
}
```


## Sample 2

### Request Sample

Measurement point is specified:

```
url: https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=yourOrgId&modelIds=opentsdb_model&measurepoints=opentsdb_di_point

method: GET
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
        "opentsdb_di_point": [
          "DI"
        ]
      },
      "modelId": "opentsdb_model"
    }
  ]
}
```

## Java SDK Sample

```java
import com.alibaba.fastjson.JSONObject;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envision.apim.poseidon.request.PoseidonRequest;
import org.junit.Test;

public class Sample {

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
    public void GetPointsTSDBMetaData(){

        String accessKey = "AccessKey of your APP";
        String secretKey = "SecretKey of your APP";

        Request request = new Request();
        request.setQueryParam("orgId", "yourOrgId");
        request.setQueryParam("modelIds", "opentsdb_model");
        request.setQueryParam("measurepoints", "opentsdb_pi_point");

        request.setMethod("GET");

        try {
            JSONObject response =  Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://apim-gateway/tsdb-policy/v2.0/policies")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
