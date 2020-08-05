# Read Data

Read data by providing SQL query through the specified channel.

## Prerequisites

Read channels are created and started in the organization.

## Request Format

```
POST https://{apigw-address}/data-federation/v2.0/channels/read/{channelId}
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
     - Channel ID

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - sqlQuery
     - Mandatory
     - String
     - SQL query for getting data from storage systems.
   * - queue
     - Optional
     - String
     - Specify the priority of the data query job. Options are Hot, Warm, and Cold.
   * - itemFormat
     - Optional
     - String
     - Reserved parameter for specifying the format of returned JSON.

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - List<Object>
     - Data that is returned by the SQL query. For more information, see `Returned Data Struct <read_data#returned-data-struct>`__

### Returned Data Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - columns
     - String
     - Column name.
   * - metadata
     - String
     - Meta data.
   * - queryState
     - String
     - Data querying state.
   * - rows
     - List<Object>
     - Rows of data. For more information, see `Data Row Struct <read_data#data-row-struct>`__

#### Data Row Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - COLUMN_NAME
     - String
     - Column name.
   * - DATA_TYPE
     - String
     - Data type.
   * - IS_NULLABLE
     - String
     - Data type.


## Error Code


## Sample

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels/read/{channelId}&orgId={}

method: POST

requestBody:
{
  "sqlQuery": "show schemas"
}
```

### Return Sample

```json
{
	"msg": "OK",
	"code": 0,
	"data": {
		"metadata": ["VARCHAR"],
		"columns": ["SCHEMA_NAME"],
		"queryState": "COMPLETED",
		"rows": []
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
    public void ReadData() {
        token = getToken();
        Request request = new Request();
        request.setQueryParam("orgId", orgId);
        request.setMethod("POST");
        request.headerParams().put(HttpHeaders.AUTHORIZATION, "Bearer " + token);
        request.headerParams().put(HttpHeaders.CONTENT_TYPE, "application/json");
        request.setBodyParams("sqlQuery", "show schemas");
        request.setBodyParams("queue", null);
        request.setBodyParams("itemFormat", null);
        JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                .url(url + "/data-federation/v2.0/channels/read/" + channelId)
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    }
}
```
