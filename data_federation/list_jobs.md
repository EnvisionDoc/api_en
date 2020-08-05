# List Jobs

Get the data reading jobs or data writing jobs of a specified channel.

## Prerequisites

Channels are created and started in the organization.

## Request Format

```
GET https://{apigw-address}/data-federation/v2.0/channels/read/{channelId}/jobs
```

## Request Parameters (Header)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Content-Type
     - Mandatory
     - String
     - Content or file type. The default value is `application/json`.
   * - Authorization
     - Mandatory
     - String
     - Access Token, by the format of `Bearer xxx`. `How to get the Access Token >> <../token/get_access_token>`__


## Request Parameters (URI)

.. list-table::
   :widths: 15 25 15 15 30
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - Your organization ID. `How to get the orgId>> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__
   * - channelId
     - Path
     - Mandatory
     - String
     - Channel ID.

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<Object>
     - List of returned jobs. For more information, see `Job Data Struct <list_jobs#job-data-struct>`__

### Job Data Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - runningJobs
     - List<Object>
     - List of running jobs. For more information, see `Job Information Struct <list_jobs#job-information-struct>`__
   * - finishedJobs
     - List<Object>
     - List of finished jobs. For more information, see `Job Information Struct <list_jobs#job-information-struct>`__


#### Jon Information Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - jobId
     - String
     - Job ID.
   * - sqlQuery
     - String
     - SQL query for getting data from storage systems.
   * - state
     - String
     - Data querying state. State values can be Failed, Canceled, or Succeeded.
   * - requestTime
     - String
     - Time when the job is submitted.
   * - duration
     - String
     - Running duration of the job.
   * - startTime
     - String
     - Time when the job started.
   * - endTime
     - String
     - Time when the job finished.


## Error Code


## Sample

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels/read/{channelId}/jobs&orgId={}

method: GET
```

### Return Sample

```json
{
   "msg": "OK",
   "code": 0,
   "data": {
   "runningJobs": null,
   "finishedJobs": [
       {
         "jobId": "2131ceb9-c00d-d42d-33db-c21002b97d16",
         "sqlQuery": "show schemas",
         "state": "Succeeded",
         "requestTime": "05/27/2020 09:22:13",
         "duration": "1.871 sec",
         "startTime": 1590571333699,
         "endTime": 1590571335570
       }]
    }
 }
```

## Java SDK Sample

```java
import com.alibaba.fastjson.JSONObject;
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envision.apim.poseidon.request.PoseidonRequest;
import com.google.common.net.HttpHeaders;
import org.apache.commons.codec.binary.Hex;
import org.junit.Test;

import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class Sample {

  private static String accessKey = "AccessKey of your APP";
  private static String secretKey = "SecretKey of your APP";
  private static String orgId = "yourOrgId";
  private static String channelId = "yourChannelId";
  private static String url = "https://{domain_url}";
  private static String token = "";

    private static class Request extends PoseidonRequest {

        public void setQueryParam(String key, Object value) {
            queryEncodeParams().put(key, value);
        }

        public void setMethod(String method) {
            this.method = method;
        }

        public void setBodyParams(String key, Object value) {
            bodyParams().put(key, value);
        }

        private String method;

        @Override
        public String baseUri() {
            return "";
        }

        @Override
        public String method() {
            return method;
        }
    }

    public static String getToken() {
        Request request = new Request();
        request.setMethod("POST");
        long timestamp = System.currentTimeMillis();
        String temp = accessKey + timestamp + secretKey;
        request.bodyParams().put("encryption", string2Sha256(temp).toLowerCase());
        request.bodyParams().put("timestamp", timestamp);
        request.bodyParams().put("appKey", accessKey);
        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                    .url(url + "/apim-token-service/v2.0/token/get")
                    .getResponse(request, JSONObject.class);
            return response.getJSONObject("data").getString("accessToken");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }

    private static String string2Sha256(String str) {
        MessageDigest messageDigest;
        String encodeStr = "";
        try {
            messageDigest = MessageDigest.getInstance("SHA-256");
            byte[] hash = messageDigest.digest(str.getBytes(StandardCharsets.UTF_8));
            encodeStr = Hex.encodeHexString(hash);
        } catch (NoSuchAlgorithmException e) {

        }
        return encodeStr;
    }

    @Test
    public void ListJobs() {
        token = getToken();
        Request request = new Request();
        request.setQueryParam("orgId", orgId);
        request.setMethod("GET");
        request.headerParams().put(HttpHeaders.AUTHORIZATION, "Bearer " + token);
        request.headerParams().put(HttpHeaders.CONTENT_TYPE, "application/json");
        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                    .url(url + "/data-federation/v2.0/channels/read/" + channelId + "/jobs")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
