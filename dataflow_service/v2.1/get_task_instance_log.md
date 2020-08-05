# Get Task Instance Log

Get the log of a specified task instance.

## Prerequisite

The user must be an EnOS user.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/taskInstances?action=getLog
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
   * - taskInstId
     - Query
     - Mandatory
     - String
     - The ID of the task instance.
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
   * - maxLength
     - Query
     - Optional
     - Integer
     - The maximum length of the queried log.


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - InstanceLog Struct
     - The log information struct. For more information, see `InstanceLog Struct <get_task_instance_log#instancelog-struct>`__

### InstanceLog Struct

#### Sample

```json
{
  "log":"============= ninstance:t104452-201908080322 n "
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - log
     - String
     - The queried log information.


## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62102
     - Instance not found
     - The ``taskInstId`` parameter is invalid.
   * - 62109
     - No log found
     - Internal service exception.


## Samples

### Request Sample
```
url: https://{apigw-address}/batch-processing-service/v2.1/taskInstances?action=getLog&taskInstId=105007-20190812013400&maxLength=&userId=yourUserId&orgId=yourOrgId
method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data":
    {
     "log":"=========================================================================nrun  num:t1ninstance:t104452-201908080322ncmdline:techo "uuu"nsubmitter:tdb_envisionncurrent time:tThu Aug 08 03:22:38 UTC 2019n=======================================nuuun"
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

public void taskInstanceLogTest(){
    //1. Select Application Registration from the left navigation bar of EnOS Console.
    //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";

    //Create a request and save the required parameters in the map of the Query.
    Request request = new Request();
    request.setQueryParam("taskInstId","105007-20190812013400");
    request.setQueryParam("userId","yourUserId");
    request.setQueryParam("orgId","yourOrgId");
    request.setMethod("GET");

    try {
        JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("https://{apigw-address}/batch-processing-service/v2.1/taskInstances?action=getLog")
                .getResponse(request, JSONObject.class);

        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
