# Save Flow

Save the information of the current workflow.

## Prerequisite

The user must be the owner of the workflow.

## Request Format

```
POST https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=save
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
   * - id
     - Mandatory
     - Integer
     - The workflow ID.
   * - type
     - Mandatory
     - Integer
     - The scheduling type of the workflow.

       + 0: Manual
       + 1: Periodic
       + 2: Temporary

   * - name
     - Mandatory
     - String
     - The workflow name.
   * - freq
     - Mandatory
     - String
     - Use the CronTab syntax to specify the time to start the workflow in a scheduling cycle (specify a 7-character CronTab expression). For more information about CronTab, see the `Cron Expression Explainer <http://www.freeformatter.com/cron-expression-generator-quartz.html>`__
   * - cycle
     - Mandatory
     - String
     - The scheduling cycle.

       + M: Month
       + W: Week
       + D: Day
       + H: Hour
       + mi: Minute

   * - alertMode
     - Mandatory
     - Integer
     - The alert mode.

       + 0: Not enabled
       + 1: Email
       + 2: SMS
       + 3: Email and SMS

   * - doAs
     - Mandatory
     - String
     - The big data account of the organization to which the workflow belongs.
   * - owners
     - Mandatory
     - String
     - The username of the owners of the workflow. The semicolon (;) is used to separate each owner, for example, owners="userNameA;userNameB".
   * - visitors
     - Mandatory
     - String
     - The username of the vistors who can access the workflow. The semicolon (;) is used to separate each visitor, for example, visitors="userNameA;userNameB".
   * - startTime
     - Mandatory
     - String
     - The effective date of the workflow.
   * - active
     - Mandatory
     - Integer
     - The scheduling status of the workflow.

       + 0: Pause
       + 1: Start

   * - parameters
     - false
     - Map
     - The parameters that are configured for the workflow to dynamically adapt to the environment changes (in the format of `key=value`).
   * - desc
     - Optional
     - String
     - The workflow description.
   * - queue
     - Optional
     - String
     - The computing queue.
   * - tasks
     - Optional
     - Array of TaskSimpleInfo Structs
     - The list of all task nodes in the workflow, with each element representing a `TaskSimpleInfo Struct <get_flow#tasksimpleinfo-struct>`__, which contains the basic information of a task node.
   * - flows
     - Optional
     - Array of FlowSimpleInfo Structs
     - The list of workflows that have dependency relations with the workflow. For more information, see `FlowSimpleInfo Struct <get_flow#flowsimpleinfo-struct>`__
   * - relations
     - Optional
     - Array of Relation Structs
     - The list of relations between tasks in the workflow, with each element representing the upstream and downstream dependency. For more information, see `Relation Struct <get_flow#relation-struct>`__


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - FlowID Struct
     - The ID of the workflow that is saved.

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62102
     - graph not found
     - The format of the parameter is invalid.
   * - 62105
     - Your account has been locked
     - The user account is locked. Please contact the administrator.


## Samples

### Request Sample
```json
url: https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=save&userId=yourUserId&orgId=yourOrgId
method: POST
requestBody:
{
	"id":"2515",
	"type":1,
	"name":"fpostm",
	"freq":"0 0 0 * * ? *",
	"cycle":"D",
	"alertMode":3,
	"doAs":"yourDoAs",
	"parameters":"[]",
	"owners":";yourOwners;",
	"desc":"e",
	"startTime":"2019-07-23",
	"visitors":";yourVisitors;",
	"active":0,
	"queue":"",
	"tasks":[
		{
			"taskName":"tass",
			"x":0.0132,
			"y":0.008100000381469727,
			"taskId":"104575",
			"nodeId":"t_104575"
		},
		{
			"taskName":"gg",
			"x":0.0084,
			"y":0.014199999237060546,
			"taskId":"104590",
			"nodeId":"t_104590"
		},
		{
			"taskName":"dff",
			"x":0.0352,"y":0.008300002288818359,
			"taskId":"104901","nodeId":"t_104901"
		}
			],
	"flows":
			[
		{
			"isVirtual":false,
			"flowId":"2788",
			"x":0.0186,
			"flowName":"jin",
			"y":0.0016999999046325683,
			"nodeId":"f_2788"},
			{"flowId":"2819",
			"flowName":"104891(tass)",
			"nodeId":"f_2819",
			"isVirtual":true,
			"x":0.0125,
			"y":0.023800001525878908}],
	"relations":
	[
		{
			"cycleGap":"D0",
			"source":"t_104575",
			"rerun":true,
			"target":"t_104590"
			},
		{
			"cycleGap":"D0",
			"source":"f_2788",
			"rerun":false,
			"target":"t_104575"
			}
	]
}
```

### Return Sample

```json
{
  "status": 0,
  "msg": "Success",
  "data": {
    "flowId": 2841
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

public void saveFlowTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.

        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        HashMap<String,Object> hashMap = new HashMap<String, Object>(2);
        hashMap.put("type",1);
        hashMap.put("name","testWorkflow");
        hashMap.put("cycle","D");
        hashMap.put("freq","0 0 0 * * ? *");
        hashMap.put("parameters","[]");
        hashMap.put("alertMode",3);
        hashMap.put("alertTo","");
        hashMap.put("id","2515");
        hashMap.put("doAs","yourDoas");
        hashMap.put("visitors","yourVisitors");
        hashMap.put("owners","yourOwners");
        hashMap.put("active",0);
        hashMap.put("queue","");
        hashMap.put("startTime","2019-07-25");
        JSONArray jsonArrayTasks = new JSONArray();
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("taskName","tass");
        jsonObject.put("x",0.0132);
        jsonObject.put("y",0.008100000381469727);
        jsonObject.put("taskId","104575");
        jsonObject.put("nodeId","t_104575");
        jsonArrayTasks.add(jsonObject);
        hashMap.put("tasks",jsonArrayTasks);
        JSONArray jsonArray = new JSONArray();
        hashMap.put("relations",jsonArray);
        hashMap.put("flows",jsonArray);
        request.setQueryParam("userId","yourUserId");
        request.setBodyParam(hashMap);
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=save")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
