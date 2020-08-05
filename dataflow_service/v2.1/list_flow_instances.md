# List Flow Instances

Search workflow instances that meet the search criteria.

## Prerequisite

The user must be an EnOS user.

## Request Format

```
POST https://{apigw-address}/batch-processing-service/v2.1/flowInstances?action=search
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
   * - type
     - Mandatory
     - Integer
     - The scheduling type of the workflow.

       + 0: Manual
       + 1: Periodic
       + 2: Temporary

   * - expression
     - Mandatory
     - String
     - The search criteria, supporting fuzzy matching query for the ``flowInstanceId`` and ``flowName`` parameters (if not specified, all workflows related to the user will be returned).
   * - owner
     - Mandatory
     - String
     - The username of the owner of the workflow instance.
   * - fromTriggerTime
     - Mandatory
     - Long
     - The starting trigger time range for the query. The workflow instances with a trigger time that falls between ``fromTriggerTime`` and ``toTriggerTime`` will be returned.
   * - toTriggerTime
     - Mandatory
     - Long
     - The ending trigger time range for the query. The workflow instances with a trigger time that falls between ``fromTriggerTime`` and ``toTriggerTime`` will be returned.
   * - status
     - Mandatory
     - String
     - The status of the flow instance. You can search for multiple status at the same time, separated by commas, such as status = "1,2,3". For a description of the status, see `FlowInstanceStatus <list_flow_instances#flowinstancestatus>`__
   * - pagination
     - Optional
     - Pagination Struct
     - Lists the paging requirements in a request. For more details, see `Pagination Struct <search_flow#pagination-struct>`__

### FlowInstanceStatus

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Status
     - Description
   * - -1
     - FAIL
   * - 0
     - INIT
   * - 1
     - SUCCESS
   * - 2
     - RUNNING
   * - 3
     - SUSPEND
   * - 4
     - INTERNAL_ERROR
   * - 5
     - WAIT
   * - 6
     - READY
   * - 7
     - TIMEOUT
   * - 8
     - CANCEL
   * - 9
     - RERUN
   * - 10
     - SKIP


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - FlowInstances Struct
     - The number and details of the searched workflow instances. For more information, see `FlowInstances Struct <list_flow_instances#flowinstances-struct>`__

### FlowInstances Struct

#### Sample

```json
{
	"flowInsts":[],
	"count":0
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - flowInsts
     - Array of FlowInstance Structs
     - The list of workflow instances. For more information, see `FlowInstance Struct <get_flow_instance.html#flowinstance-struct>`__
   * - count
     - Integer
     - The number of searched workflow instances (number of elements in the FlowInstance struct).

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62102
     - The sorters field parameter is invalid
     - The given ``sorters`` ``field`` parameter is invalid. The valid options are:

       + createTime
       + updateTime
       + startTime
       + triggerTime
       + endTime


## Samples

### Request Sample
```json
url: https://{apigw-address}/batch-processing-service/v2.1/flowInstances?action=search&userId=yourUserId&orgId=yourOrgId
method: POST
requestBody:
{
	"type": 1,
	"fromTriggerTime": 1573648355000,
	"toTriggerTime": 1573698120000,
	"status": 1,
	"owner": "",
	"expression": "",
	"pagination":{
		"pageNo": 1,
		"pageSize": 10,
		"sorters": [{
			"field": "updateTime",
			"order": "ASC"
		}]
	}
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "flowInsts": [{
                "instanceId": "2809-20190812080700",
                "flowId": 2809,
                "flowName": "21",
                "freq": "0 0 0 * * ? *",
                "cycle": "D",
                "parameters": "[]",
                "doAs": "yourDoAs",
                "graph": "{"creator":"yourCreator","freq":"0 0 0 * * ? *","alertMode":3,"owners":"yourOwners","cycle":"D","do_as":"yourDoAs","flows":[],"name":"21","instId":"2809-20190812080700","id":2809,"relations":[],"parameters":"[]","tasks":[{"task_name":"tass","taskInstId":"104890-20190812080700","x":0.002,"y":0.002,"task_id":104890,"nodeId":"t_104890"}]}",
                "status": 1,
                "statusDesc": "SUCCESS",
                "triggerTime": "2019-08-12 08:07:22",
                "startTime": "2019-08-12 08:07:30",
                "endTime": "2019-08-12 08:07:32",
                "timestamp": "2019-08-12 08:09:48.0",
                "virtual": false,
                "owner": "yourOwners",
                "hasEditPri": true,
                "hasReadPri": true,
                "isCancelled": false
            },
            {
                "instanceId": "2957-20190812075600",
                "flowId": 2957,
                "flowName": "fdd",
                "freq": "0 0 0 * * ? *",
                "cycle": "D",
                "parameters": "[]",
                "doAs": "yourDoAs",
                "graph": "{"creator":"yourCreator","freq":"0 0 0 * * ? *","alertMode":3,"owners":";yourOwners;","cycle":"D","do_as":"yourDoAs","flows":[],"name":"fdd","instId":"2957-20190812075600","id":2957,"relations":[],"parameters":"[]","tasks":[{"task_name":"gg","taskInstId":"105040-20190812075600","x":0.0068,"y":0.0071,"task_id":105040,"nodeId":"t_105040"}]}",
                "status": 1,
                "statusDesc": "SUCCESS",
                "triggerTime": "2019-08-12 07:56:56",
                "startTime": "2019-08-12 07:57:00",
                "endTime": "2019-08-12 07:57:02",
                "timestamp": "2019-08-12 08:00:09.0",
                "virtual": false,
                "owner": "yourOwner",
                "hasEditPri": true,
                "hasReadPri": true,
                "isCancelled": false
            }],
    "count": 2
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

public void flowInstancesTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.

        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
		    HashMap<String,Object> bodyMap = new HashMap<>();
		    bodyMap.put("type",0);
        bodyMap.put("owner","");
        bodyMap.put("startTriggerTime",1565568000000L);
        bodyMap.put("endTriggerTime",1565654399999L);
        bodyMap.put("status","");
		    bodyMap.put("expression","");
        HashMap<String,Object> paginationMap= new HashMap<String, Object>(3);
        paginationMap.put("pageNo",1);
        paginationMap.put("pageSize",10);
        List<HashMap<String,Object>> list = new ArrayList<HashMap<String,Object>>();
        HashMap<String,Object> sorterMap= new HashMap<String, Object>(2);
        sorterMap.put("field","updateTime");
        sorterMap.put("order","ASC");
        list.add(sorterMap);
        paginationMap.put("sorters",list );
        bodyMap.put("pagination",paginationMap);
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setBodyParam(bodyMap);
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/flowInstances?action=search")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
