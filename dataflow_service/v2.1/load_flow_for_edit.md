# Load Flow For Edit

Load the specified workflow to a temporary workflow to get the workflow information.

## Prerequisite

The user must belong to the organization (OU) which the target workflow belongs to.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/flows?action=loadForEdit
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
   * - flowId
     - Query
     - Mandatory
     - Integer
     - The workflow ID.
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


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Flow Struct
     - The detailed information of the workflow. For more information, see `Flow Struct <get_flow#flow-struct>`__

## Error Code

See [Common Error Codes](overview#common-error-codes).


## Samples

### Request Sample
```
url: https://{apigw-address}/batch-processing-service/v2.1/flows?action=loadForEdit&flowId=2791&userId=yourUserId&orgId=yourOrgId
method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "virtual": false,
    "freq": "0 0 0 * * ? *",
    "type": 1,
    "cycle": "D",
    "alertMode": 3,
    "hasEditPri": true,
    "startTime": "2019-07-23",
    "locked": false,
    "flowId": 2515,
    "owner": ";yourOwners;",
    "creator": "yourCreator",
    "updateUser": "yourUpdateUser",
    "active": 0,
    "updateTime": "2019-08-08 05:51:43.0",
    "flowName": "fpostm",
    "graph": "{"creator":"yourCreator ","freq":"0 0 0 * * ? *","alertMode":3,"active":0,"owners":";yourOwners;","type":1,"cycle":"D","startTime":"2019-07-23","visitors":";yourVisitors;","doAs":"yourDoAs","flows":[{"isVirtual":false,"flowId":"2788","x":0.0186,"flow_name":"jin","y":0.0016999999046325683,"nodeId":"f_2788"},{"isVirtual":true,"flowId":"2819","x":8.0E-4,"flow_name":"104891(tass)","y":0.022100001525878907,"nodeId":"f_2819"}],"name":"fpostm","relations":[{"cycleGap":"D0","source":"t_104575","rerun":true,"target":"t_104590"},{"cycleGap":"D0","source":"f_2788","rerun":false,"target":"t_104575"},{"cycleGap":"D0","source":"f_2819","rerun":false,"target":"t_104590"}],"parameters":"[]","queue":"","tasks":[{"taskName":"tass","x":0.0132,"y":0.008100000381469727,"taskId":"104575","nodeId":"t_104575"},{"taskName":"gg","x":0.0084,"y":0.014199999237060546,"taskId":"104590","nodeId":"t_104590"},{"taskName":"dff","x":0.0352,"y":0.008300002288818359,"taskId":"104901","nodeId":"t_104901"}],"desc":"e"}",
    "isUserLocked": false,
    "entry": 1,
    "doAs": "yourDoAs",
    "createTime": "2019-07-26 05:41:58.0",
    "syncType": 1,
    "visitor": ";yourVisitors;",
    "parameters": "[]",
    "queue": "",
    "hasReadPri": true,
    "desc": "e"
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

ublic void synchronizedFlowTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("flowId",2791);
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setMethod("GET");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/flows?action=loadForEdit")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
