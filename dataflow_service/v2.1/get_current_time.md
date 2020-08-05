# Get Current Time

Get the current time of the server.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/time?action=getCurrentTime
```


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Long
     - The current time of the server, by UTC format in milliseconds.

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
url: https://{apigw-address}/batch-processing-service/v2.1/time?action=getCurrentTime
method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": 1565251865242
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

public static void getCurrentTimeTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setMethod("GET");

        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url("https://{apigw-address}/batch-processing-service/v2.1/time?action=getCurrentTime")
                    .getResponse(request, JSONObject.class);

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

```
