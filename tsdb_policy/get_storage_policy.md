# Get Storage Policy

Get the detailed information of the specified storage policy with the storage policy ID, including the storage policy name, stored data type, storage time, and models and measurement points that are configured with the storage policy.

## Request Format

```
GET https://{apigw-address}/tsdb-policy/v2.0/policies/{policyId}
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


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<JSONObject>
     - The detailed information of the storage policy. See `Storage Policy Struct <get_storage_policy#storage-policy-struct>`__


### Storage Policy Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - policyId
     - String
     - The storage policy ID.
   * - policyName
     - String
     - The storage policy name.
   * - policyType
     - String
     - The storage type.
   * - retention
     - String
     - The data storage time.
   * - models
     - List<JSONObject>
     - The list of models and measurement points. See `Model and Point Struct <save_storage_policy#model-and-point-struct>`__

### Sample

```json
{
     "models": [
        {
           "modelId": "model_1",
           "points": [
              "point1",
              "point2"
           ]
        },
        {
           "modelId": "model_2",
           "points": [
              "point1",
              "point2"
           ]
        }
     ],
     "policyId": "policy_ID",
     "policyName": "AI Normalized Data",
     "policyType": "NORMALIZED",
     "retention": "6M"
}
```

## Error Code

For the description of error codes, see [Common Error Codes](overview#common-error-codes).

## Samples

### Request Sample

```
url: https://{apigw-address}/tsdb-policy/v2.0/policies/aa8bbcba-2919-4c78-854c-54984d85d2fa?orgId=yourOrgId

method: GET
```

### Return Sample

```json
{
   "code": 0,
   "msg": "OK",
   "submsg": null,
   "data": {
      "models": [
         {
            "modelId": "model_1",
            "points": [
               "test_point2",
               "test_point1"
            ]
         },
         {
            "modelId": "model_2",
            "points": [
               "test_point2",
               "test_point1"
            ]
         }
      ],
      "policyId": "aa8bbcba-2919-4c78-854c-54984d85d2fa",
      "policyName": "AI Normalized Data",
      "policyType": "NORMALIZED",
      "retention": "6M"
   }
}
```

## Java SDK Sample

```java
import com.alibaba.fastjson.JSONObject;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envision.apim.poseidon.request.PoseidonRequest;
import org.junit.Before;
import org.junit.Test;

public class Sample {
    private static final String APIM_BASE_URL = "https://{domain_url}";
    private Poseidon poseidon;

    @Before
    public void init() {
        poseidon = Poseidon.config(
                PConfig.init()
                .appKey("AccessKey of your APP")
                .appSecret("SecretKey of your APP")
        ).method("GET");
    }

    @Test
    public void GetStoragePolicyData() {
        String policyId = "yourPolicyId";
        String resp = poseidon.url(APIM_BASE_URL + "/tsdb-policy/v2.0/policies/" + policyId)
                .queryParam("orgId", "yourOrgId")
                .sync();

        System.out.println(resp);
    }
}
```
