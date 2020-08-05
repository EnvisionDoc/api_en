# Delete Asset Latest Data

Delete the latest data of the specified measurement points of specified devices.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Write

For more information about resources and required permission, see [Policies, Roles and Permissions>>](/docs/enos/en/2.1.0/iam/concept/access_policy.html)

## Request Format

```
POST https://{apigw-address}/tsdb-service/v2.1/latest?action=delete
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
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports deleting the latest data of multiple assets, separated by commas. `How to get asset ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-asset-id-assetid-assetid>`__
   * - pointIds
     - Mandatory
     - String
     - The measurement point ID. Supports deleting the latest data of multiple measurement points, separated by commas. The upper limit of the number of measurement points that can be deleted is 3,000 (number of devices * number of measurement points). `How to get measurement point ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-the-measurement-point-id-pointid-pointid>`__

## Error Code

For the description of error codes, see [Common Error Codes](overview#common-error-codes).

## Smaple

### Request Sample

```
url: https://{apigw-address}/tsdb-service/v2.1/latest?action=delete&orgId=yourOrgId

method: POST

Content-Type: application/json

requestBody:
{
  "assetIds": "Ps4PViva",
  "pointIds": "pi_point"
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "submsg": "",
  "data": null
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
        ).method("POST").header("Content-Type", "application/json");
    }

    @Test
    public void DeleteAssetsLatestData() {
        Request request = new Request();
        request.setBodyParams("assetIds", "yourAssetId1,yourAssetId2");
        request.setBodyParams("pointIds", "yourPointId");

        JSONObject response =  poseidon
                .url(APIM_BASE_URL + "/tsdb-service/v2.1/latest")
                .queryParam("orgId", "yourOrgId")
                .queryParam("action", "delete")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
