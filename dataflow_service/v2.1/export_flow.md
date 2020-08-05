# Export Flow

Export a workflow configuration.

## Prerequisite

The user must belong to the organization (OU) which the target workflow belongs to.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/flows?action=export
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

```json
{
	"name": "workflow1",
	"cycle": "D",
	"cron": "0 0 0 * * ? *",
	"parameters": "[]",
	"alertMode": 3,
	"submitter": "yourSubmitter",
	"owners": "yourOwners",
	"visitors": "yourVisitors;",
	"type": 1,
	"syncType": 1,
	"desc": "",
	"startTime": "2019-07-25",
	"tasks": [
	  {
		"name": "tass",
		"resource": "default",
		"type": "COMMAND",
    "runMode": "{\"taskMode\":1,\"cpu\":0.5,\"memory\":1,\"maxParallel\":0,\"keyType\":0,\"datasourceId\":0,\"path\":\"\",\"content\":\"\"}",
		"syncType": 1,
		"cmd": "echo "hello"",
		"submitter": "",
		"filePackage": "",
		"cron": "",
		"priorityLevel": 0,
		"timeout": 300,
		"retryLimit": 3,
		"retryInterval": 0,
		"successCode": "0",
		"asLink": false
	  }
	],
	"flowLinks": [],
	"taskLinks": [],
	"relations": [],
	"linkRelations": []
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - name
     - String
     - The name of the workflow.
   * - cycle
     - String
     - The scheduling cycle.

       + M: Month
       + W: Week
       + D: Day
       + H: Hour
       + mi: Minute

   * - cron
     - String
     - If CronTab syntax is used when specifying the time to start the workflow in a scheduling cycle, a 7-character CronTab expression is used. For more information about CronTab, see the `Cron Expression Explainer <http://www.freeformatter.com/cron-expression-generator-quartz.html>`__
   * - parameters
     - Map
     - The global parameters that are configured for the workflow to dynamically adapt to the environment changes (in the format of `key=value`).
   * - alertMode
     - Integer
     - The alert mode.

       + 0: Not enabled
       + 1: Email
       + 2: SMS
       + 3: Email and SMS
   * - submitter
     - String
     - The workflow submission account (the big data account corresponding to the organization).
   * - owners
     - String
     - The username of the owners of the workflow. The semicolon (;) is used to separate each owner, for example, owners="userNameA;userNameB".
   * - visitors
     - String
     - The username of the vistors who can access the workflow. The semicolon (;) is used to separate each visitor, for example, visitors="userNameA;userNameB".
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
   * - tasks
     - Array of Task Structs
     - The collection of task nodes in the workflow, with each element representing a task in the workflow. For more information, see `Task Struct <export_flow#task-struct>`__
   * - flowLinks
     - Array of FlowLink Structs
     - The collection of workflow references, with each element representing a source workflow that the current workflow depends on. (Using the ``linkId`` in the `FlowLink Struct <export_flow#flowlink-struct>`__, you can find the related link relation in the ``linkRelations`` collection. The link relation represents the relationship between a specific task in the current workflow with the source workflow).
   * - taskLinks
     - Array of TaskLink Structs
     - The collection of task references, with each element representing a task in a source workflow that a task in the current workflow depends on. (Using the ``linkId`` in the `TaskLink Struct <export_flow#tasklink-struct>`__, you can find the related link relation in the ``linkRelations`` collection. The link relation represents the relationship between a specific task in the current workflow with the source workflow).  
   * - relations
     - Array of Relation Structs
     - The collection of relations between tasks, with each element representing the upstream and downstream dependency. For more information, see `Relation Struct <export_flow#relation-struct>`__
   * - linkRelations
     - Array of LinkRelation Structs
     - The collection of link relations. For more information, see `LinkRelation Struct <export_flow#linkrelation-struct>`__


### Task Struct

#### Sample
```json
{
    "name": "tass",
    "resource": "default",
    "type": "COMMAND",
    "runMode": "{\"taskMode\":1,\"cpu\":0.5,\"memory\":1,\"maxParallel\":0,\"keyType\":0,\"datasourceId\":0,\"path\":\"\",\"content\":\"\"}",
    "syncType": 1,
    "cmd": "echo 'hello'",
    "submitter": "",
    "filePackage": "",
    "cron": "",
    "priorityLevel": 0,
    "timeout": 300,
    "retryLimit": 3,
    "retryInterval": 0,
    "successCode": "0",
    "asLink": false
 }
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - name
     - String
     - The task name.
   * - resource
     - String
     - The task resource.
   * - type
     - Integer
     - The task type.

       + 0: Data Integration
       + 1: WORMHOLE
       + 2: CALCULATE
       + 3: SHELL
       + 4: CANAAN
       + 5: HIVE
       + 6: MR
   * - syncType
     - Integer
     - The sync type of the task.

       + 0: File synchronization
       + 1: Data synchronization
   * - cmd
     - String
     - The command line.
   * - submitter
     - String
     - The workflow submission account (the big data account corresponding to the organization).
   * - filePackage
     - String
     - The file location.
   * - cron
     - String
     - The time for scheduling the task.
   * - priorityLevel
     - Integer
     - The priority level of the task.
   * - timeout
     - Integer
     - The timeout value.
   * - retryLimit
     - Integer
     - The number of retries.
   * - retryInterval
     - Integer
     - The interval for retry.
   * - successCode
     - String
     - The success returned code.
   * - asLink
     - Boolean
     - + true = the task has a dependency relation with other tasks
       + false = the task does not have a dependency relation with other tasks
   * - runMode
     - String
     - Task running mode. For more information, see `Run Mode Struct <export_flow#run-mode-struct>`__

### Run Mode Struct

#### Sample

```
{
	"taskMode": 1,
	"cpu": 0.5,
	"memory": 1,
	"maxParallel": 0,
	"keyType": 0,
	"datasourceId": 0,
	"path": "",
	"content": ""
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - taskMode
     - Integer
     - Task running mode (1: Single Task; 2: Multiple Tasks).
   * - cpu
     - Float
     - CPU (unit: core; minimun: 0.1; maximum 2) that is required by running each task (single task or sub-task of multiple tasks).
   * - memory
     - Float
     - Memory (unit: G; minimun: 0.3; maximum 4) that is required by running each task (single task or sub-task of multiple tasks).
   * - maxParallel
     - Integer
     - In multiple tasks mode, the maximum concurrency of sub-tasks.
   * - keyType
     - Integer
     - In multiple tasks mode, the source of the distribution key (1: external files; 2: custom key, specified by the ``content`` parameter).
   * - datasourceId
     - Integer
     - When the source of the distribution key is from external files, the data source ID (generated when registering the data source through the **Data Source Registration** service).
   * - path
     - String
     - When the source of the distribution key is from external files, the path of external data source that stores the distribution key file.
   * - content
     - String
     - When the source of the distribution key is custom key, the content of the distribution key.


### FlowLink Struct

#### Sample

```json
{
    "linkId": "0",
    "sourceFlowName": "jin"
}

```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - linkId
     - String
     - The link ID.
   * - sourceFlowName
     - String
     - The name of the upstream workflow.

### TaskLink Struct

#### Sample
```json
{
    "linkId": "0",
    "sourceFlowName": "dw",
    "sourceTaskName": "tass"
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - linkId
     - String
     - The link ID.
   * - sourceFlowName
     - String
     - The name of the upstream workflow.
   * - sourceTaskName
     - String
     - The name of the upstream task (the exact upstream task can be found when used with ``sourceFlowName``).

### Relation Struct

#### Sample
```json
{
    "sourceTaskName": "tass",
    "targetTaskName": "rf",
    "rerun": true
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - sourceTaskName
     - String
     - The name of the upstream task.
   * - targetTaskName
     - String
     - The name of the downstream task.
   * - rerun
     - Boolean
     - Effective only for task-level re-running.

       + true = the downstream task will be started when re-running
       + false = the downstream task will not be started when re-running

### LinkRelation Struct

#### Sample
```json
{
    "linkId": "0",
    "targetTaskName": "tass",
    "rerun": false
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - linkId
     - String
     - The link ID.
   * - targetTaskName
     - String
     - The name of the downstream task.
   * - rerun
     - Boolean
     - + true = the downstream task will be started when re-running
       + false = the downstream task will not be started when re-running

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62102
     - Flow validation exception
     - The format of the request body is invalid.
   * - 62109
     - Internal server exception
     - Internal server exception.


## Samples

### Request Sample
```
url: https://{apigw-address}/batch-processing-service/v2.1/flows?action=export&flowId=2924&userId=yourUserId&orgId=yourUserId
method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "name": "nFlow",
    "cycle": "D",
    "cron": "0 0 0 * * ? *",
    "parameters": "[]",
    "alertMode": 3,
    "submitter": "yourSubmitter",
    "owners": "yourOwners",
    "visitors": ";yourVisitors;",
    "type": 1,
    "syncType": 1,
    "desc": "ga",
    "startTime": "2019-07-24",
    "tasks": [
      {
        "name": "tass",
        "resource": "default",
        "type": "COMMAND",
        "syncType": 1,
        "cmd": "echo 'hello'",
        "submitter": "",
        "filePackage": "",
        "cron": "",
        "priorityLevel": 0,
        "timeout": 300,
        "retryLimit": 3,
        "retryInterval": 0,
        "successCode": "0",
        "asLink": false,
        "runMode": "{\"taskMode\":1,\"cpu\":0.5,\"memory\":1,\"maxParallel\":0,\"keyType\":0,\"datasourceId\":0,\"path\":\"\",\"content\":\"\"}"
      }
    ],
    "flowLinks": [],
    "taskLinks": [],
    "relations": [],
    "linkRelations": []
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

public void exportFlowTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.

        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("flowId","2924");
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setMethod("GET");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/flows?action=export")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
