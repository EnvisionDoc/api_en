# Save Storage Policy

Update and save the configuration of the specified storage policy, including the data storage time and models and measurement points that are configured with it.

## Request Format

```
POST https://{apigw-address}/tsdb-policy/v2.0/policies/{policyId}
```

## Request Parameters (Header)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Content-Type
     - Mandatory
     - String
     - Content or file type. The default value is `application/json`.

## Request Parameters (URI)

.. list-table::
   :widths: 15 25 15 15 30
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - policyId
     - Path
     - Mandatory
     - String
     - The storage policy ID, which can be retrieved through the **EnOS Management Console > Time Series Data Management > Storage Policy** page.
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - retention
     - Optional
     - String
     - The data storage time. If the models and measurement points already have the storage time configured, this parameter is optional.
   * - models
     - Mandatory
     - List<JSONObject>
     - The list of models and measurement points. See `Model and Point Struct <save_storage_policy#model-and-point-struct>`__

### Model and Point Struct

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - modelId
     - Mandatory
     - String
     - Model ID.
   * - points
     - Mandatory
     - List<JSONObject>
     - A list of measurement points in the model that need storage policy configuration.


## Error Code

For the description of error codes, see [Common Error Codes](overview#common-error-codes).

## Sample

### Request Sample

```
url: https://{apigw-address}/tsdb-policy/v2.0/policies/aa8bbcba-2919-4c78-854c-54984d85d2fa

method: POST

requestBody:
{
   "models": [
      {
         "modelId": "model1",
         "points": [
            "test_point2",
            "test_point1"
         ]
      },
      {
         "modelId": "model2",
         "points": [
            "test_point2",
            "test_point1"
         ]
      }
   ],
   "retention": "6M"
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": null
}  
```

## Java SDK Sample

```java
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envision.apim.poseidon.request.PoseidonRequest;
import org.junit.Before;
import org.junit.Test;

public class Sample {
    private static final String APIM_BASE_URL = "https://{domain_url}";
    private Poseidon poseidon;

    private static class Request extends PoseidonRequest {

        public void setBodyParams(String key, Object value) {
            bodyParams().put(key, value);
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

    @Before
    public void init() {
        poseidon = Poseidon.config(
                PConfig.init()
                .appKey("AccessKey of your APP")
                .appSecret("SecretKey of your APP")
        ).method("POST") .header("Content-Type", "application/json");
    }

    @Test
    public void SaveStoragePolicy() {
        Request request = new Request();

        JSONArray models = new JSONArray();
        JSONObject model1 = new JSONObject();
        model1.put("modelId", "yourModelId1");
        model1.put("points", new String[]{"yourPointId1", "yourPointId2"});
        JSONObject model2 = new JSONObject();
        model2.put("modelId", "yourModelId2");
        model2.put("points", new String[]{"yourPointId1", "yourPointId2"});
        models.add(model1);
        models.add(model2);

        request.setBodyParams("models", models);
        request.setBodyParams("retention", "6M");

        String policyId = "yourPolicyId";
        JSONObject resp = poseidon.url(APIM_BASE_URL + "/tsdb-policy/v2.0/policies/" + policyId)
                .queryParam("orgId", "yourOrgId")
                .getResponse(request, JSONObject.class);

        System.out.println(resp);
    }
}
```
