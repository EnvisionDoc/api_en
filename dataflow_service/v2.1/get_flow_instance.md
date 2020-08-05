# Get Flow Instance

Get the information of a specified workflow instance.

## Prerequisite

The user must be an EnOS user.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/flowInstances?action=get
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
   * - flowInstId
     - Query
     - Mandatory
     - String
     - The ID of the workflow instance.
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
     - FlowInstance Struct
     - The detailed information of the workflow instance. For more information, see `FlowInstance Struct <get_flow_instance#flowinstance-struct>`__

### FlowInstance Struct

#### Sample

```
{
    "instanceId": "2438-201907261239",
    "flowId": 2438,
    "flowName": "rew",
    "freq": "0 1/1 * * * ? *",
    "cycle": "mi",
    "parameters": "[]",
    "doAs": "yourDoAs",
    "graph": "{"creator":"yourCreator","freq":"0 1/1 * * * ? *","alertMode":3,"owners":";yourOwners;","cycle":"mi","doAs":"yourDoAs","flows":[],"name":"rew","instId":"2438-201907261239","id":2438,"relations":[],"parameters":"[]","tasks":[{"taskName":"fr","taskInstId":"104452-201907261239","x":0.0198,"y":0.0045,"taskId":104452,"nodeId":"t_104452","status":"SUCCESS"}]}",
    "status": 0,
    "statusDesc": "INIT",
    "triggerTime": "2019-07-26 20:39:00",
    "startTime": "2019-07-26 12:39:37",
    "endTime": "2019-07-26 12:39:42",
    "timestamp": "2019-07-26 12:38:30.0",
    "virtual": false,
    "owner": "yourOwners",
    "alertMode": 3,
    "calDt": "2019-07-25",
    "hasEditPri": false,
    "hasReadPri": true
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - instanceId
     - String
     - The ID of the workflow instance.
   * - flowId
     - Integer
     - The workflow ID.
   * - flowName
     - String
     - The workflow name.
   * - freq
     - String
     - If CronTab syntax is used when specifying the time to start the workflow in a scheduling cycle, a 7-character CronTab expression is used. For more information about CronTab, see the `Cron Expression Explainer <http://www.freeformatter.com/cron-expression-generator-quartz.html>`__
   * - cycle
     - String
     - The scheduling cycle.

       + M: Month
       + W: Week
       + D: Day
       + H: Hour
       + mi: Minute

   * - parameters
     - Map
     - The global parameters that are configured for the workflow to dynamically adapt to the environment changes (in the format of `key=value`).
   * - doAs
     - String
     - The big data account of the organization to which the workflow belongs.
   * - graph
     - InstanceGraph Struct
     - The task dependency of the workflow instance. For more information, see `InstanceGraph Struct <get_flow_instance#instancegraph-struct>`__
   * - status
     - Integer
     - The task running status.
   * - statusDesc
     - String
     - The description of the task running status.
   * - triggerTime
     - String
     - The planned triggering time of the task.
   * - startTime
     - String
     - The start time of the task.
   * - endTime
     - String
     - The end time of the task.
   * - timestamp
     - String
     - The time when the instance was created.
   * - virtual
     - Boolean
     - + true = the workflow instance is a virtual instance 
       + false = the workflow instance is not a virtual instance
   * - owner
     - String
     - The owner of the workflow instance.
   * - alertMode
     - Integer
     - The alert mode.

       + 0: Not enabled
       + 1: Email
       + 2: SMS
       + 3: Email and SMS

   * - calDt
     - String
     - The business date (date from which the data starts to be processed by the workflow).
   * - hasEditPri
     - Boolean
     - + true = the user has editing permission for the workflow 
       + false = the user does not have editing permission for the workflow
   * - hasReadPri
     - Boolean
     - + true = the user has reading permission for the workflow 
       + false = the user does not have reading permission for the workflow

### InstanceGraph Struct

#### Sample
```json
{
  "creator":"yourCreator",
  "freq":"0 0 0 * * ? *",
  "alertMode":3,
  "owners":"yourOwners",
  "cycle":"D",
  "doAs":"yourDoAs",
  "flows":[],
  "name":"21",
  "instId":"2809-20190812080700",
  "id":2809,
  "relations":[],
  "parameters":"[]",
  "tasks":
	  [{
	  "taskName":"tass",
	  "taskInstId":"104890-20190812080700",
	  "x":0.002,
	  "y":0.002,
	  "taskId":104890,
	  "nodeId":"t_104890",
	  "status":"CANCEL"}]
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - creator
     - String
     - The username of the user who created the workflow instance.
   * - freq
     - String
     - If CronTab syntax is used when specifying the time to start the workflow in a scheduling cycle, a 7-character CronTab expression is used. For more information about CronTab, see the `Cron Expression Explainer <http://www.freeformatter.com/cron-expression-generator-quartz.html>`__
   * - alertMode
     - Integer
     - The alert mode.

       + 0: Not enabled
       + 1: Email
       + 2: SMS
       + 3: Email and SMS

   * - owners
     - String
     - The username of the owners of the workflow. The semicolon (;) is used to separate each owner, for example, owners="userNameA;userNameB".
   * - cycle
     - String
     - The scheduling cycle.

       + M: Month
       + W: Week
       + D: Day
       + H: Hour
       + mi: Minute
       
   * - doAs
     - String
     - The big data account of the organization to which the workflow belongs.
   * - flows
     - Array of FlowInstanceGraph Struct
     - The workflow dependency of the workflow instance. For more information, see `FlowInstanceGraph Struct <get_flow_instance#flowinstancegraph-struct>`__
   * - name
     - String
     - The workflow name.
   * - instId
     - Integer
     - The ID of the workflow instance.
   * - id
     - Integer
     - The workflow ID.
   * - relations
     - Array of Relation Structs
     - The list of relations between tasks in the workflow, with each element representing the upstream and downstream dependency. For more information, see `Relation Struct <get_flow#relation-struct>`__
   * - parameters
     - Array
     - The parameters that are configured for the task to dynamically adapt to the environment changes (in the format of `key=value`)
   * - tasks
     - Array of TaskInstanceGraph Structs
     - The list of all task instances in the workflow instance. For more information, see `TaskInstanceGraph Struct <get_flow_instance#taskinstancegraph-struct>`__


### FlowInstanceGraph Struct

#### Sample
```json
{
  "flowId":"2809",
  "flowName":"21",
  "nodeId":"f_2809",
  "isVirtual":false,
  "x":0.0125,
  "y":0.0015,
  "flowInstId":"2809-20190812101300",
  "status":"NONE"
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
     - The workflow ID.
   * - flowName
     - String
     - The workflow name.
   * - nodeId
     - String
     - The ID of the node that is part of other workflows.
   * - isVirtual
     - Boolean
     - + true = the workflow is a virtual workflow 
       + false = the workflow is not a virtual workflow
   * - x
     - Double
     - The x-axis of the node on the configuration panel of the workflow.
   * - y
     - Double
     - The y-axis of the node on the configuration panel of the workflow.
   * - flowInstId
     - String
     - The ID of the workflow instance.

### TaskInstanceGraph Struct

#### Sample
```json
{
  "taskName":"tass",
  "taskInstId":"105048-20190812101300",
	"x":0.0132,
	"y":0.008100000381469727,
	"taskId":"104575",
	"nodeId":"t_104575",
  "status":"INIT"
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - taskName
     - String
     - The task name.
   * - taskInstId
     - String
     - The ID of the task instance.
   * - x
     - Double
     - The x-axis of the task on the configuration panel.
   * - y
     - Double
     - The y-axis of the task on the configuration panel.
   * - taskId
     - String
     - The task ID.
   * - nodeId
     - String
     - The node ID (Note: The node ID is not the same as the task ID, because there are task nodes and workflow nodes that have dependency relations in a workflow).
   * - status
     - String
     - The status of the task instance.


## Error Code

See [Common Error Codes](overview#common-error-codes).


## Samples

### Request Sample
```
url: https://{apigw-address}/batch-processing-service/v2.1/flowInstances?action=get&flowInstId=2809-20190808093200&userId=yourUserId&orgId=yourOrgId

method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "instanceId": "2809-20190808093200",
    "flowId": 2809,
    "flowName": "21",
    "freq": "0 0 0 * * ? *",
    "cycle": "D",
    "parameters": "[]",
    "doAs": "yourDoAs",
    "graph": "{"creator":"yourCreator","freq":"0 0 0 * * ? *","alertMode":3,"owners":"yourOwners","cycle":"D","doAs":"yourDoAs","flows":[],"name":"21","instId":"2809-20190808093200","id":2809,"relations":[],"parameters":"[]","tasks":[{"taskName":"tass","taskInstId":"104890-20190808093200","x":0.002,"y":0.002,"taskId":104890,"nodeId":"t_104890","status":"SUCCESS"}]}",
    "status": 1,
    "statusDesc": "SUCCESS",
    "triggerTime": "2019-08-08 09:32:12",
    "startTime": "2019-08-08 09:32:30",
    "endTime": "2019-08-08 09:32:32",
    "timestamp": "2019-08-08 09:34:36.0",
    "virtual": false,
    "owner": "yourOwners",
    "alertMode": 3,
    "calDt": "2019-08-07",
    "hasEditPri": true,
    "hasReadPri": true
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

public void flowInstanceTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.

        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("flowInstId","2924-20190812013400");
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setMethod("GET");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/flowInstances?action=get")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
