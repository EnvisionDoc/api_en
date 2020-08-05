# Import Flow

Import workflow configuration to create a workflow with the specified name under the specified directory.

## Prerequisite

The user must be the owner of the workflow.

## Request Format

```
POST https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=import
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
     - Optional
     - Integer
     - The workflow ID. If not specified, the system will generate a ``flowId``. If the specified ``flowId`` already exists, the system will generate another ``flowId``).
   * - flowName
     - Mandatory
     - String
     - The workflow name.
   * - desc
     - Mandatory
     - String
     - The workflow description.
   * - dirId
     - Mandatory
     - String
     - The ID of the directory for the workflow.
   * - flowJson
     - Mandatory
     - Flow Struct
     - The details of the workflow. For more information, see `Flow Struct <export_flow#flow-struct>`__


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - FlowId Struct
     - The workflow ID. For more information, see `FlowId Struct <import_flow#flowid-struct>`__

### FlowId Struct

#### Sample
```json
{
  "flowId":2781
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - flowId
     - String
     - The ID of the created workflow.

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62102
     - One of the following messages can be returned:

       + Incorrect parameter
       + Invalid parameter: flowName
       + Directory does not exist
       + Workflow validation failed

     - Invalid parameter
   * - 62109
     - Workflow creating failed: xx
     - Failed to create the workflow because of internal server exception.

## Samples

### Request Sample
```
url: https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=import&userId={}&orgId={}

method: POST

requestBody:
{
  "flowName": "outuser",
  "desc": "",
  "dirId": "dirId",
  "flowJson": {
        "cycle": "D",
        "cron": "0 0 0 * * ? *",
        "parameters": "[{\"key\":\"REPLACE\",\"value\":\"lili1\"}]",
        "submitter": "yourSubmitter",
        "owners": "yourOwners",
        "visitors": "yourVisitors",
        "type": 1,
        "desc": "",
        "tasks": [
            {
                "name": "tass",
                "resource": "default",
                "type": "DATA_INTEGRATION",
                "cmd": "echo "hello"",
                "submitter": "yourSubmitter",
                "filePackage": "",
                "cron": "",
                "priorityLevel": 0,
                "timeout": 300,
                "retryLimit": 3,
                "retryInterval": 0,
                "successCode": "0",
                "waitCode": "",
                "asLink": true,
                "runMode": "{\"taskMode\":1,\"cpu\":0.5,\"memory\":1,\"maxParallel\":0,\"keyType\":0,\"datasourceId\":0,\"path\":\"\",\"content\":\"\"}",
                "syncType": 1
            }
        ],
        "relations": [],
        "startTime": "2019-11-22",
        "flowLinks": [],
        "syncType": 1,
        "linkRelations": [],
        "alertTo": "",
        "alertMode": 3,
        "taskLinks": [],
        "appId": ""
	}
}
```

### Return Sample

```json
{
  "status": 0,
  "msg": "Success",
  "data": {
    "flowId": 2839
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

public void importFlowTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.

        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        HashMap<String,Object> hashMap = new HashMap<String, Object>(20);
        hashMap.put("name","testWorkflow");
        hashMap.put("cycle","D");
        hashMap.put("cron","0 0 0 * * ? *");
        hashMap.put("parameters","[]");
        hashMap.put("alertMode",3);
        hashMap.put("alertTo","");
        hashMap.put("appId","");
        hashMap.put("submitter","yourSubmitter");
        hashMap.put("owners","yourOwners");
        hashMap.put("visitors",";yourVisitors;");
        hashMap.put("type",1);
        hashMap.put("syncType",1);
        hashMap.put("desc","");
        hashMap.put("startTime","2019-07-25");
        JSONArray jsonArrayTasks = new JSONArray();
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("name","tass");
        jsonObject.put("resource","default");
        jsonObject.put("type","COMMAND");
        jsonObject.put("syncType",1);
        jsonObject.put("cmd","echo "hello"");
        jsonObject.put("submitter","");
        jsonObject.put("filePackage","");
        jsonObject.put("cron","");
        jsonObject.put("priorityLevel",0);
        jsonObject.put("timeout",300);
        jsonObject.put("retryLimit",3);
        jsonObject.put("retryInterval",0);
        jsonObject.put("successCode","0");
        jsonObject.put("waitCode","");
        jsonObject.put("runMode","{\"taskMode\":1,\"cpu\":0.5,\"memory\":1,\"maxParallel\":0,\"keyType\":0,\"datasourceId\":0,\"path\":\"\",\"content\":\"\"}");
        jsonObject.put("asLink",false);
        jsonArrayTasks.add(jsonObject);
        hashMap.put("tasks",jsonArrayTasks);
        JSONArray jsonArray = new JSONArray();
        hashMap.put("flowLinks",jsonArray);
        hashMap.put("taskLinks",jsonArray);
        hashMap.put("relations",jsonArray);
        hashMap.put("linkRelations",jsonArray);

        HashMap<String,Object> bodyMap = new HashMap<String, Object>(4);
        bodyMap.put("flowName","myFlow1");
        bodyMap.put("desc","this is flow");
        bodyMap.put("dirId","***************");
        bodyMap.put("flowJson",hashMap );
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setBodyParam(bodyMap);
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=import")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
