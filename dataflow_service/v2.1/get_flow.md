# Get Flow

Get the information of a specified workflow.

## Prerequisite

The user must belong to the organization (OU) which the target workflow belongs to.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/flows?action=get
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
     - The detailed information of the workflow. For more information, see `Flow Struct <#flow-struct>`__

### Flow Struct

#### Sample

```
{
    "virtual": false,
    "freq": "0 0 0 * * ? *",
    "type": 1,
    "cycle": "D",
    "alertMode": 3,
    "hasEditPri": true,
    "startTime": "2019-07-18",
    "locked": false,
    "flowId": 2430,
    "owner": " owner",
    "creator": " creator",
    "active": 0,
    "updateUser": "yourUpdateUser",
    "updateTime": "2019-07-18 07:50:36.0",
    "flowName": "yu",
    "graph": "{
"queue":"","cycle":"D","desc":"","doAs":"yourDoAs","freq":"0 0 0 * * ? *","visitors":"","tasks":[{"taskName":"hello","taskId":"104443","y":0.0071,"x":0.0096,"nodeId":"t_104443"}],"type":1,"creator":"yourCreator","flows":[],"alertMode":3,"relations":[],"name":"yu","startTime":"2019-07-18","active":0,"parameters":"[]","owners":";yourOwners;"
}",
    "isUserLocked": false,
    "entry": 2,
    "doAs": "yourDoAs",
    "createTime": "2019-07-18 07:49:10.0",
    "visitor": ";yourVisitors;",
    "syncType": 1,
    "parameters": "[]",
    "hasReadPri": true,
    "desc": ""
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
     - Integer
     - The workflow ID.
   * - flowName
     - String
     - The workflow name.
   * - active
     - Integer
     - The scheduling status of the workflow.

       + 0: Pause
       + 1: Start

   * - creator
     - String
     - The username of the user who created the workflow instance.
   * - createTime
     - String
     - The time when the workflow is created.
   * - updateUser
     - String
     - The user who updated the workflow.
   * - updateTime
     - String
     - The time when the workflow is updated.
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
   * - owner
     - String
     - The username of the owners of the workflow. The semicolon (;) is used to separate each owner, for example, owners="userNameA;userNameB".
   * - visitor
     - String
     - The username of the vistors who can access the workflow. The semicolon (;) is used to separate each visitor, for example, visitors="userNameA;userNameB".
   * - doAs
     - String
     - The big data account of the organization to which the workflow belongs.
   * - alertMode
     - Integer
     - The alert mode.

       + 0: Not enabled
       + 1: Email
       + 2: SMS
       + 3: Email and SMS

   * - graph
     - FlowGraph Struct
     - The workflow dependency. For more information, see `FlowGraph Struct <get_flow#flowgraph-struct>`__
   * - entry
     - Integer
     - The method used for creating the workflow.

       + 0: Portal
       + 1: API
       + 2: eos

   * - type
     - Integer
     - The scheduling type of the workflow.

       + 0: Manual
       + 1: Periodic
       + 2: Temporary

   * - syncType
     - Integer
     - The sync type of the workflow.

       + 0: File synchronization
       + 1: Data synchronization

   * - desc
     - String
     - The workflow description.
   * - startTime
     - String
     - The effective date of the workflow.
   * - virtual
     - Boolean
     - + true = the workflow is a virtual workflow 
       + false = the workflow is not a virtual workflow
   * - locked
     - Boolean
     - + true = the workflow is locked 
       + false = the workflow is not locked
   * - hasEditPri
     - Boolean
     - + true = the user has editing permission for the workflow 
       + false = the user does not have editing permission for the workflow
   * - hasReadPri
     - Boolean
     - + true = the user has reading permission for the workflow 
       + false = the user does not have reading permission for the workflow
   * - isUserLocked
     - Boolean
     - + true = the user is locked 
       + false = the user is not locked

### FlowGraph Struct

#### Sample
```json
{
  "creator":"yourCreator",
  "freq":"0 0 0 * * ? *",
  "alertMode":3,
  "type":1,
  "owners":"yourOwners",
  "visitors":";yourVisitors; ",
  "startTime":"2019-07-25"
  "cycle":"D",
  "doAs":"yourDoAs",
  "flows":[],
  "name":"21",
  "syncType":1,
  "relations":[],
  "parameters":"[]",
  "tasks":
	  [{
	  "taskName":"tass",
	  "task_inst_id":"104890-20190812080700",
	  "x":0.002,
	  "y":0.002,
	  "taskId":104890,
	  "nodeId":"t_104890",
	  "status":"CANCEL"}],
  "queue":"",
  "desc":"ga"
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

   * - type
     - Integer
     - The scheduling type of the workflow.

       + 0: Manual
       + 1: Periodic
       + 2: Temporary

   * - owners
     - String
     - The username of the owners of the workflow. The semicolon (;) is used to separate each owner, for example, owners="userNameA;userNameB".
   * - visitors
     - String
     - The username of the vistors who can access the workflow. The semicolon (;) is used to separate each visitor, for example, visitors="userNameA;userNameB".
   * - startTime
     - String
     - The effective date of the workflow.
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
     - Array of FlowSimpleInfo Structs
     - The list of workflows that have dependency relations with the workflow. For more information, see `FlowSimpleInfo Struct <get_flow#flowsimpleinfo-struct>`__
   * - name
     - String
     - The workflow name.
   * - syncType
     - Integer
     - The sync type of the workflow.

       + 0: File synchronization
       + 1: Data synchronization

   * - relations
     - Array of Relation Structs
     - The list of the relations between tasks in the workflow, with each element representing the upstream and downstream dependency. For more information, see `Relation Struct <get_flow#relation-struct>`__
   * - parameters
     - Map
     - The parameters that are configured for the task to dynamically adapt to the environment changes (in the format of `key=value`)
   * - tasks
     - Array of TaskSimpleInfo Structs
     - The list of all task nodes in the workflow, with each element representing a TaskSimpleInfo struct, which contains basic information of a task node. For more information, see `TaskSimpleInfo Struct <get_flow#tasksimpleinfo-struct>`__
   * - queue
     - String
     - The computing queue.
   * - desc
     - String
     - The workflow description.

### FlowSimpleInfo Struct

#### Sample
```json
{
    "flowId":"2809",
    "flowName":"21",
    "nodeId":"f_2809",
    "isVirtual":false,
    "x":0.0125,
    "y":0.0015
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

### TaskSimpleInfo Struct

#### Sample
```json
{
  "taskName":"tass",
  "x":0.0132,
  "y":0.008100000381469727,
  "taskId":"104575",
  "nodeId":"t_104575"
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
     - The node ID. (Note: The node ID is not the same as the task ID, because there are task nodes and workflow nodes that have dependency relations in a workflow.)

### Relation Struct

#### Sample
```json
{
    "cycleGap": "D0",
    "rerun": true,
    "source": "t_105048",
    "target": "t_104575"
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - cycleGap
     - String
     - The scheduling time difference between upstream and downstream tasks, with the format of `{cycle}{offset}` (`cycle` is the unit of time different, and `offset` is value).
   * - source
     - String
     - The node ID of the upstream task.
   * - target
     - String
     - The node ID of the downstream task.
   * - rerun
     - Boolean
     - Effective only for task-level re-running.
     
       + true = the downstream task will be started when re-running
       + false = the downstream task will not be started when re-running


## Error Codes

See [Common Error Codes](overview#common-error-codes).


## Sample

### Request Sample
```
url: https://{apigw-address}/batch-processing-service/v2.1/flows?action=get&flowId=2479&userId=yourUserId&orgId=yourOrgId
method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "flowId": 2479,
    "flowName": "test0722-1",
    "active": 0,
    "creator": "yourCreator",
    "createTime": "2019-07-22 08:56:35.0",
    "updateUser": "yourUpdateUser",
    "updateTime": "2019-07-22 08:56:58.0",
    "freq": "0 0 0 * * ? *",
    "cycle": "D",
    "parameters": "[{"key":"ouids","value":"oxxxxxxxx"},{"key":"path","value":"/user/db_henglin/test_0722-1/"},{"key":"overwrite","value":"true"}]",
    "owner": "yourOwners",
    "visitor": ";yourVisitors;",
    "doAs": "yourDoAs",
    "alertMode": 1,
    "graph": "{"queue":"","cycle":"D","desc":"","doAs":"yourDoAs","freq":"0 0 0 * * ? *","visitors":"","tasks":[{"taskName":"MDM-Sync","taskId":"104506","y":0.002,"x":0.002,"nodeId":"t_104506"},{"taskName":"MDMHive","taskId":"104507","y":0.009,"x":0.002,"nodeId":"t_104507"}],"type":0,"creator":"yourCreator","flows":[],"alertMode":1,"relations":[{"cycleGap":"D0","rerun":true,"source":"t_104506","target":"t_104507"}],"name":"test0722-1","startTime":"2019-07-22","active":0,"parameters":"[{"key":"ouids","value":"oxxxxxxxxxxx"},{"key":"path","value":"/user/db_henglin/test_0722-1/"},{"key":"overwrite","value":"true"}]","owners":";yourOwners;"}",
    "entry": 0,
    "type": 0,
    "syncType": 1,
    "desc": "",
    "startTime": "2019-07-22",
    "virtual": false,
    "locked": false,
    "hasEditPri": false,
    "hasReadPri": true,
    "isUserLocked": false
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

public void getFlowTest(){
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
                    .url("https://{apigw-address}/batch-processing-service/v2.1/flows?action=get")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
