# Search Flow

Search the basic information of workflows that meet the search criteria (including workflows of other users in the organization (OU)).

## Prerequisite

The user must belong to the OU which the target workflows belong to.

## Request Format

```
POST https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=search
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
   * - expression
     - Optional
     - String
     - The expression for searching the workflows.
   * - pagination
     - Optional
     - Pagination Struct
     - Lists the paging requirements in a request. For more details, see `Pagination Struct <search_flow#pagination-struct>`__

### Pagination Struct

#### Sample
```json
{
    "pagination": {
        "pageNo": 0,
        "pageSize": 10,
        "sorters": [{
            "field": "startTime",
            "order": "ASC"
        }]
    }
}
```

#### Parameters

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - pageNo
     - Mandatory
     - Integer
     - The request pages, starting from 0.
   * - pageSize
     - Mandatory
     - Integer
     - The number of records in each page, which must be greater than 0.
   * - sorters
     - Optional
     - Sorter Struct
     - The pagination sorting method.
   * - sorters.field
     - Mandatory
     - String
     - The pagination field name. Supported fields are `createTime`, `updateTime`, and `startTime`.
   * - sorters.order
     - Optional
     - String
     - + ASC (default) = ascending order
       + DESC = descending order

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of PageFlow Structs
     - The list of PageFlow structs, which contain the basic information of searched workflows. For more details, see `PageFlow Struct <search_flow#pageflow-struct>`__


### PageFlow Struct

#### Sample
```json
{
    "flowId": "21",
    "flowName": "dim_wtg_full"
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


## Error Code

See [Common Error Codes](overview#common-error-codes).


## Samples

### Request Sample
```json
url: https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=search&userId=yourUserId&orgId=yourOrgId
method: POST
requestBody:
{
	"expression": "",
	"pagination":{
		"pageNo": 0,
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
    "status": 0,
    "msg": " Success",
    "data": [
        {
            "flowId": "20",
            "flowName": "vd_text"
        },
        {
            "flowId": "21",
            "flowName": "dim_wtg_full"
        },
        {
            "flowId": "22",
            "flowName": "wenl_dim_fact_downtime"
        }
    ]
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

public void pagingFlowsTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.

        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");

        HashMap<String,Object> bodyMap= new HashMap<String, Object>(2);
        bodyMap.put("expression","");
        HashMap<String,Object> paginationMap= new HashMap<String, Object>(3);
        paginationMap.put("pageNo",0);
        paginationMap.put("pageSize",10);
        List<HashMap<String,Object>> list = new ArrayList<HashMap<String,Object>>();
        HashMap<String,Object> sorterMap= new HashMap<String, Object>(2);
        sorterMap.put("field","updateTime");
        sorterMap.put("order","ASC");
        list.add(sorterMap);
        paginationMap.put("sorters",list);
        bodyMap.put("pagination",paginationMap);
        request.setBodyParam(bodyMap);
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/dataflow-batch-service/v2.0/flows?action=search")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
