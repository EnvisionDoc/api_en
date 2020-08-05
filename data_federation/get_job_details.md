# Get Job Details

Get the detailed information of a data reading job or a data writing job.

## Prerequisites

There are running or finished data querying or data writing jobs.

## Request Format

```
GET https://{apigw-address}/data-federation/v2.0/channels/read/{channelId}/jobs/{jobId}
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
     - The access token (or bearer token). `How to get the Access Token >> <../token/get_access_token>`__


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
     - The organization ID. `How to get the orgId>> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__
   * - channelId
     - Path
     - Mandatory
     - String
     - The channel ID.
   * - jobId
     - Path
     - Mandatory
     - String
     - The data querying or writing job ID.

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<Object>
     - The job Details. For more information, see `Job Information Struct <get_job_details#job-information-struct>`__

### Job Information Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - jobId
     - String
     - The job ID.
   * - sqlQuery
     - String
     - The SQL query for getting data from storage systems.
   * - state
     - String
     - The job state.
   * - totalFragments
     - String
     - The total job fragments.
   * - finishedFragments
     - String
     - The finished fragments.
   * - startTime
     - String
     - The time when the job started.
   * - endTime
     - String
     - The time when the job finished.


## Error Code


## Samples

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels/read/{channelId}/jobs/{jobId}&orgId={}

method: GET
```

### Return Sample

```json
{
     "msg": "OK",
     "code": 0,
     "data": {
         "jobId": "2131ceb9-c00d-d42d-33db-c21002b97d16",
         "totalFragments": 1,
         "sqlQuery": "describe hive.db.test1",
         "fragmentProfile": [
             {
                 "minorFragmentProfile": [
                     {
                         "maxMemoryUsed": 6446336,
                         "minorFragmentId": 0,
                         "operatorProfile": [
                             {
                                 "waitNanos": 0,
                                 "setupNanos": 0,
                                 "inputProfile": [
                                     {
                                         "batches": 2,
                                         "records": 8,
                                         "schemas": 1
                                     }
                                 ],
                                 "processNanos": 1096191,
                                 "peakLocalMemoryAllocated": 2445568,
                                 "operatorType": 30,
                                 "operatorId": 4
                             },
                             {
                                 "waitNanos": 0,
                                 "setupNanos": 1982782,
                                 "inputProfile": [
                                     {
                                         "batches": 1,
                                         "records": 8,
                                         "schemas": 1
                                     }
                                 ],
                                 "processNanos": 267596,
                                 "peakLocalMemoryAllocated": 2441232,
                                 "operatorType": 2,
                                 "operatorId": 3
                             },
                             {
                                 "waitNanos": 0,
                                 "setupNanos": 54199,
                                 "inputProfile": [
                                     {
                                         "batches": 1,
                                         "records": 2,
                                         "schemas": 1
                                     }
                                 ],
                                 "processNanos": 397197,
                                 "peakLocalMemoryAllocated": 426072,
                                 "operatorType": 14,
                                 "operatorId": 2
                             },
                             {
                                 "waitNanos": 0,
                                 "setupNanos": 4057163,
                                 "inputProfile": [
                                     {
                                         "batches": 1,
                                         "records": 2,
                                         "schemas": 1
                                     }
                                 ],
                                 "processNanos": 279497,
                                 "peakLocalMemoryAllocated": 159744,
                                 "operatorType": 10,
                                 "operatorId": 1
                             },
                             {
                                 "waitNanos": 328497,
                                 "setupNanos": 0,
                                 "metric": [
                                     {
                                         "metricId": 0,
                                         "longValue": 78
                                     }
                                 ],
                                 "inputProfile": [
                                     {
                                         "batches": 1,
                                         "records": 2,
                                         "schemas": 1
                                     }
                                 ],
                                  "processNanos": 152199,
                                  "peakLocalMemoryAllocated": 159744,
                                  "operatorType": 13,
                                  "operatorId": 0
                             }
                         ],
                         "lastUpdate": 1590571335227,
                         "startTime": 1590571333875,
                         "state": 3,
                         "endTime": 1590571335225,
                         "lastProgress": 1590571335227,
                         "memoryUsed": 0
                     }
                 ],
                 "majorFragmentId": 0
             }
         ],
         "startTime": 1590571333699,
         "state": 2,
         "endTime": 1590571335570,
         "type": 1,
         "planEnd": 1590571333795,
         "queueWaitEnd": 1590571333862,
         "user": "anonymous",
         "finishedFragments": 0
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
  private static String jobId = "yourJobId";
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
    public void GetJobDetails() {
        token = getToken();
        Request request = new Request();
        request.setQueryParam("orgId", orgId);
        request.setMethod("GET");
        request.headerParams().put(HttpHeaders.AUTHORIZATION, "Bearer " + token);
        request.headerParams().put(HttpHeaders.CONTENT_TYPE, "application/json");
        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                    .url(url + "/data-federation/v2.0/channels/read/" + channelId + "/jobs/" + jobId)
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
