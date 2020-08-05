# Get Timezone

Get the timezone where the server is located.

## Request Format

```
GET https://{apigw-address}/batch-processing-service/v2.1/time?action=getTimeZone
```


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - TimeZone Struct
     - The timezone details. For more information, see `TimeZone Struct <get_time_zone#timezone-struct>`__

### TimeZone Struct

#### Sample

```json
{
  "timezone": "GMT+8"
}
```

#### Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - timezone
     - String
     - The timezone, in the format of `GMT+N`.

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
url: https://{apigw-address}/batch-processing-service/v2.1/time?action=getTimeZone
method: GET
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "data": {
    "timezone": "GMT+8"
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

public static void GetTimeZoneTest(){
        //1. Select Application Registration from the left navigation bar of EnOS Console.
        //2. Open the App Detail page to get the AccessKey and SecretKey of the application.
        String accessKey = "yourAppAccessKey";
        String secretKey = "yourAppSecretKey";

        //Create a request and save the required parameters in the map of the Query.
        Request request = new Request();
        request.setMethod("GET");

        try {
              JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("https://{apigw-address}/batch-processing-service/v2.1/time?action=getTimeZone")
                .getResponse(request, JSONObject.class);

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
