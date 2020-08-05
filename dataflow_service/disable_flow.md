# Disable Flow

Stop the scheduling of a specified workflow.

## Prerequisites

- The user must be the owner of the workflow.
- Both the user and the workflow are not locked.

## Request Format

```
POST https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=disable
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
   * - userId
     - Query
     - Mandatory
     - String
     - The user ID. `How to get userId>> </docs/api/en/2.1.0/api_faqs#how-to-get-user-id-userid>`__
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the user belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - flowId
     - Mandatory
     - Integer
     - The workflow ID.


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - No results will be returned if the request is successful.

## Error Code

See [Common Error Codes](overview#common-error-codes).

## Samples

### Request Sample

```json
url: https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=disable&userId={}&orgId={}
method: POST
requestBody:
{
  "flowId": 3377
}
```

### Return Sample

```json
{
  "status": 0,
  "msg": " Success",
  "data": ""
}
```



## Java SDK Sample

```java
import com.alibaba.fastjson.JSONObject;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class Request extends PoseidonRequest {
    public void setQueryParam(String key, Object value){
        QueryParams().put(key, value);
    }
    public void setHeaderParam(String key, String value){
        headerParams().put(key, value);
    }
    public void setBodyParam(Map<String, Object> bodyPara){
        bodyParams().putAll(bodyPara);
    }
    public void setMethod(String method) {
        this.method = method;
    }
    private String method;
    public String baseUri() {
        return "";
    }
    public String method() {
        return method;
    }
}

public void disableFlowTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        Map<String,Object> map = new HashMap<>(1);
        map.put("flowId",3377);
        request.setBodyParam(map)
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=disable")
                    .getResponse(request, JSONObject.class);

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
