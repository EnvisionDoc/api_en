# Delete Stage State

Delete the intermediate state data of a specified operator (stage) in a stream processing job.

## Prerequisites

Before calling this API, ensure that the target stream processing job is paused.

## Request Format

```
POST https://{apigw-address}/streaming/v2.0/stage-state?action=delete
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
   * - Authorization
     - Mandatory
     - String
     - The access token (or bearer token). `How to get the Access Token >> <../token/get_access_token>`__


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
     - The organization ID. `How to get the orgId>> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__


## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - pipelineId
     - Mandatory
     - String
     - The stream processing job ID, which can be found on the **EnOS Management Console > Stream Processing > Stream Operation** page.
   * - stageInstanceName
     - Mandatory
     - String
     - The stage instance name, which can be found on the **Stream Development** page. Click the stream processing job name, select the target operator, and copy the stage instance name on the **Info** page.
   * - assetIds
     - Mandatory
     - String
     - The asset ID. Supports the query of multiple asset IDs, separated by commas.
   * - pointIds
     - Mandatory
     - String
     - The measurement point ID. Supports the query of multiple measurement point IDs, separated by commas. The upper limit of the number of measurement points that can be queried is 100,000.


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Boolean
     -
       + true = data is deleted
       + false = failed to delete data


## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 61102
     - Missing param xx
     - The parameter format or value is not valid.
   * - 61105
     - Too many points
     - The number of requested measurement points exceeds the limit.
   * - 61106
     - Wrong pipelineId or OU has no privilege
     - The provided pipeline ID is not valid, or the pipeline ID and organization ID do not match.
   * - 61107
     - Not supported Stage Type
     - The specified stage type is not supported.  
   * - 61199
     - xx
     - Other errors.


## Samples

### Request Sample

```
url: https://{apigw-address}/streaming/v2.0/stage-state?action=delete&orgId=yourOrgId

method: POST

requestBody：
{
	"pipelineId":"yourPipelineId",
	"stageInstanceName":"yourStageInstanceName",
	"assetIds":"yourAssetIds",
	"pointIds":"yourPointIds"
}
```

### Return Sample

```
{
  "code": 0,
  "msg": " OK",
  "data": true
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
    private static final String API_Gateway_URL = "https://{domain_url}";
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
    public void DeleteStageState() {
        Request request = new Request();
        request.setBodyParams("assetIds", "yourAssetId");
        request.setBodyParams("pointIds", "yourPointId");
        request.setBodyParams("pipelineId", "yourPipelineId");
        request.setBodyParams("stageInstanceName", "yourStageInstanceName");

        JSONObject response = poseidon
                .url(APIM_BASE_URL + "/streaming/v2.0/stage-state")
                .queryParam("orgId", "yourOrgId")
                .queryParam("action", "delete")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
