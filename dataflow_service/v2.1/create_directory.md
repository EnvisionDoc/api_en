# Create Directory

Create a directory.

## Prerequisite

The user must belong to the organization (OU) of the parent directory of the directory to be created.

## Request Format

```
POST https://{apigw-address}/batch-processing-service/v2.1/directories?action=create
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
   * - parentId
     - Mandatory
     - String
     - The ID of the parent directory.
   * - dirName
     - Mandatory
     - String
     - The name of the directory to be created.


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - DirectoryId Struct
     - A struct that contains the ID of the created directory. For more information, see `DirectoryId Struct <#directoryid-struct>`__

### DirectoryId Struct

#### Sample

```
{
  "dirId": "249a33bd419a4710b1567f5088f8955b"
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - dirId
     - String
     - The ID of the created directory.

## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62102
     - One of the following messages may be returned:

       + param: dirName cannot be empty
       + param: parentId cannot be empty
       + parentId not found
       + A directory of the same name already exists

     - Invalid parameter
   * - 62109
     - Internal server exception
     - Internal server exception.


## Samples

### Request Sample

```json
url: https://{apigw-address}/batch-processing-service/v2.1/directories?action=create&userId=yourUserId&orgId=yourOrgId
method: POST
requestBody:
{
  "dirName": "directory_name",
  "parentId": "249a33bd419a4710b1567f5088f8955b"
}

```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "dirId": "62e3038840514caf9af60ad36878851e"
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

@Test
public void CreateDirTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        HashMap<String,Object> hashMap = new HashMap<String, Object>(2);
        hashMap.put("dirName","strDIR");
        hashMap.put("parentId","**************");
        request.setQueryParam("userId","yourUserId");
        request.setQueryParam("orgId","yourOrgId");
        request.setBodyParam(hashMap);
        request.setMethod("POST");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/directories?action=create")
                    .getResponse(request, JSONObject.class);

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
