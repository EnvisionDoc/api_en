# Write Chunk File

Write file chunks to data source through a specified channel.

## Prerequisites

Write channels are created and started in the organization.

## Request Format

```
POST https://{apigw-address}/data-federation/v2.0/channels/write/{channelId}/chunk-file
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
   * - dataSourceName
     - Query
     - Mandatory
     - String
     - The data source alias. Only HDFS data source is supported.

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - fileName
     - Mandatory
     - String
     - The name of the file to be written to the storage.
   * - totalSize
     - Mandatory
     - Integer
     - The file size.
   * - chunkOffset
     - Mandatory
     - Integer
     - The offset of the current chunk in the file.
   * - chunkSize
     - Mandatory
     - Integer
     - The size of the current chunk (before Base64 encoding).
   * - chunkData
     - Mandatory
     - String
     - The chunk data, with Base64 encoding.


## Error Code


## Samples

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels/write/{channelId}/chunk-file&orgId={}&dataSourceName={}

method: POST

requestBody:
{
  "fileName": "ttt",
  "totalSize": "13",
  "chunkData": "dGVzdHRlc3R0dGVzdA==",
  "chunkSize": "13",
  "chunkOffset": "0"
}
```

### Return Sample

```
{
  "msg": "OK",
  "code": 0,
  "submsg": ""
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
    public void WriteChunkFile() {
        token = getToken();
        Request request = new Request();
        request.setQueryParam("orgId", orgId);
        request.setMethod("POST");
        request.headerParams().put(HttpHeaders.AUTHORIZATION, "Bearer " + token);
        request.headerParams().put(HttpHeaders.CONTENT_TYPE, "application/json");
        request.setBodyParams("fileName", "ttt");
        request.setBodyParams("totalSize", "13");
        request.setBodyParams("chunkData", "dGVzdHRlc3R0dGVzdA==");
        request.setBodyParams("chunkSize", "13");
        request.setBodyParams("chunkData", "0");
        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                    .url(url + "/data-federation/v2.0/channels/write/" + channelId + "/chunk-file")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
