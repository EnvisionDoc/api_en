# List Channels

Get the list of channels (Read and Write) to which the application is authorized.

## Prerequisites

The user must be an EnOS user.

## Request Format

```
GET https://{apigw-address}/data-federation/v2.0/channels
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
   * - channelType
     - Query
     - Optional
     - String
     - The channel type, READ or WRITE. If not specified, lists all the channels to which the application is authorized.

       + READ: for querying data from storage systems.
       + WRITE: for writing data to storage systems.

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<Object>
     - The list of channels. For more information, see `Channel Information Struct <list_channels#channel-information-struct>`__

### Channel Information Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - channelType
     - String
     - The channel type (READ or WRITE).
   * - channelId
     - String
     - The channel ID.
   * - dataSourceInfo
     - List<Object>
     - The list of data sources associated with the channel. For more information, see `Data Source Information Struct <list_channels#data-source-information-struct>`__

#### Data Source Information Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - dataSourceName
     - String
     - The data source name.
   * - dataSourceType
     - String
     - The data source type.


## Error Code


## Samples

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels&orgId={}&channelType={}

method: GET
```

### Return Sample

```json
{
  "msg": "OK",
  "code": 0,
  "data": [
    {
      "channelId": "ch-123456",
      "channelType": "WRITE",
      "dataSourceInfo": [
        {
          "dataSourceName": "mysql",
          "dataSourceType": "MYSQL"
        }
      ]
    }
  ]
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
    public void ListChannels() {
        token = getToken();
        Request request = new Request();
        request.setQueryParam("orgId", orgId);
        request.setMethod("GET");
        request.headerParams().put(HttpHeaders.AUTHORIZATION, "Bearer " + token);
        request.headerParams().put(HttpHeaders.CONTENT_TYPE, "application/json");
        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                    .url(url + "/data-federation/v2.0/channels")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
