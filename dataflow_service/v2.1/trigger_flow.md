# Trigger Flow

Manually trigger a workflow schedule.

## Prerequisites

- The user must be the owner of the workflow.
- Both the user and the workflow are not locked.

## Request Format

```
POST https://{apigw-address}/batch-processing-service/v2.1/flows?action=trigger
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
   * - triggerTime
     - Mandatory
     - Long
     - Specify the trigger time of the workflow, keeping in mind the following rules:

       + If the triggering time is before the current time, the workflow will be triggered immediately, and the triggering time will be passed into the time parameters for calculation.
       + The workflow only allows one instance to run at any one time. If the pre-run instance conflicts with a running instance, it will be executed in sequence.


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - FlowInstanceId Struct
     - The details of a workflow instance. For more information, see `FlowInstanceId Struct <trigger_flow#flowinstanceid-struct>`__

### FlowInstanceId Struct

#### Sample
```json
{
  "flowInstanceId": "2430-20190718075000"
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - flowInstanceId
     - String
     - The ID of the workflow instance.

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62104
     - This workflow has no task. You cannot trigger it.
     - The workflow does not have any task for you to trigger.
   * - 62109
     - Internal server exception
     - Internal server exception.

## Samples

### Request Sample
```json
url: https://{apigw-address}/batch-processing-service/v2.1/flows?action=trigger&userId=yourUserId&orgId=yourOrgId
method: POST
{
  "flowId":3377,
  "triggerTime":1574385824000
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "flowInstanceId": "2791-19700101000000"
  }
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

public void triggerImmediatelyTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("userId"," yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        HashMap<String,Object> hashMap = new HashMap<String, Object>(2);
        hashMap.put("flowId",3377);
        hashMap.put("triggerTime",1574385824000);
        request.setBodyParam(hashMap);
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/ flows?action=trigger")
                    .getResponse(request, JSONObject.class);

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
