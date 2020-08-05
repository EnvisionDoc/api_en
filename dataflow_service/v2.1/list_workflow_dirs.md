# List Workflow Directories

Get all the content in the `workflow` directory of the current organization (OU), including workflow files and sub-directories.

## Prerequisite

The user must belong to the OU which the target directories belong to.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/directories?action=listWorkFlowDirs
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


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of WorkFlowDir Structs
     - The list of the workFlowDir structs, including all the workflow files and sub-directories. For more information, see `WorkFlowDir Struct <list_workflow_dirs#workflowdir-struct>`__

### WorkFlowDir Struct

#### Sample

```json
{
  "children": [],
  "title":"Workflow",
  "type": 1, 	
  "key": "249a33bd419a4710b1567f5088f8955b",
  "isDirectory": true
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - children
     - Array of WorkFlowDir Structs
     - The list of the files or sub-directories.
   * - title
     - String
     - The name of the files or sub-directories.
   * - type
     - String
     - The type of directory.

       + 0: Data Integration
       + 1: Workflow
       + 2: Data Resource
       + 3: Hql
       + 4: Common Resource
       
   * - key
     - String
     - The directory ID.
   * - isDirectory
     - Boolean
     - + true = directory
       + false =  file

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62109
     - Internal server exception
     - Internal server exception.


## Samples

### Request Sample
```
url: https://{apigw-address}/batch-processing-service/v2.1/directories?action=listWorkFlowDirs&userId=yourUserId&orgId=yourOrgId
method: GET
```

### Return Sample

```json
  "code": 0,
  "msg": "OK",
  "data": [
    {
      "children": [
        {
          "children": [],
          "title": "String1",
          "type": 1,
          "key": "***************",
          "isDirectory": true
        },
        {
          "children": [
            {
              "editable": true,
              "title": "workflow1",
              "type": 1,
              "key": 2512,
              "isDirectory": false
            }
          ],
          "title": "ffdir",
          "type": 1,
          "key": "**************",
          "isDirectory": true
        },
        {
          "children": [],
          "title": "dirt",
          "type": 1,
          "key": "************",
          "isDirectory": true
        }
      ],
      "title": "Workflow",
      "type": 1,
      "key": "***************",
      "isDirectory": true
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

public void listWorkFlowDirsTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setMethod("GET");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/directories?action=listWorkFlowDirs")
                    .getResponse(request, JSONObject.class);

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
