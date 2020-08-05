# Write Message

Write message to data source through a specified channel.

## Prerequisites

Write channels are created and started in the organization.

## Request Format

```
POST https://{apigw-address}/data-federation/v2.0/channels/write/{channelId}/msg
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

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - dataSourceName
     - Mandatory
     - String
     - The data source alias.
   * - data
     - Mandatory
     - String
     - The data to be written to the storage.
   * - sync
     - Mandatory
     - Boolean
     - Specify the data writing method.

       + true = synchronous data writing (default)
       + false = asynchronous data writing

## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - failures
     - List<Object>
     - The list of data that failed to write to storage. For more information, see `Failure Record Struct <write_message#failure-record-struct>`__

### Failure Record Struct

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - info
     - List<Object>
     - The failure record details. For more information, see `Failure Record Details <write_message#failure-record-details>`__
   * - line
     - List<Object>
     - The failure data.


#### Failure Record Details

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - field
     - String
     - The data field that failed to write to storage.  
   * - reason
     - String
     - The reason for failure.


## Error Code


## Samples

### Request Sample
```
url: https://{apigw-address}/data-federation/v2.0/channels/write/{channelId}/msg&orgId={}

method: POST

requestBody:
{
    "dataSourceName": "mysql_remote",
    "data": "{\"table\":\"data\",\"lines\":[{\"WGEN.GenReactivePW\":\"2.5283\",\"ou_id\":\"o15622268182161\",\"WTUR.TurbineListSts\":\"5\",\"WTUR.TurbineUnionSts\":\"71\",\"WTUR.ConnectionSts\":\"0\",\"WGEN.GenActivePW\":\"45.700001\",\"WROT.TemB2Mot\":\"29.504801\",\"WTUR.TurbineTopSts\":\"2\",\"WGEN.TorqueSetpoint\":\"867.359375\",\"WWPP.PPCurrentDay\":\"0\",\"WCNV.GridFreq\":\"49.971561\",\"WWPP.PPCurrentYear\":\"17896\",\"dev_id\":\"04mmQAEM\",\"WNAC.TemOut\":\"25.691801\",\"WWPP.PPCurrentMonth\":\"33763\",\"WTUR.TurbineHealthSts\":\"0\",\"timeOfDay\":\"2019-09-01 00:00:00\",\"WTUR.TurbineGroupSts\":\"70\"},{\"WGEN.GenReactivePW\":\"2.7037\",\"ou_id\":\"o15622268182161\",\"WTUR.TurbineListSts\":\"5\",\"WTUR.TurbineUnionSts\":\"71\",\"WTUR.ConnectionSts\":\"0\",\"WGEN.GenActivePW\":\"45.439999\",\"WTUR.TurbineTopSts\":\"2\",\"WGEN.TorqueSetpoint\":\"865.127869\",\"WCNV.GridFreq\":\"49.998112\",\"dev_id\":\"04mmQAEM\",\"WTUR.TurbineHealthSts\":\"0\",\"timeOfDay\":\"2019-09-01 00:00:01\",\"WTUR.TurbineGroupSts\":\"70\"}]}"
}
```

### Return Sample

```json
{
   "msg": "OK",
   "code": 0,
   "failures": [
     {
       "line": [],
       "info": [
         {
           "reason": "",
           "field": ""
         }
       ]
     }
   ],
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
    public void WriteMessage() {
        token = getToken();
        Request request = new Request();
        request.setQueryParam("orgId", orgId);
        request.setMethod("POST");
        request.headerParams().put(HttpHeaders.AUTHORIZATION, "Bearer " + token);
        request.headerParams().put(HttpHeaders.CONTENT_TYPE, "application/json");
        request.setBodyParams("data", "");
        request.setBodyParams("dataSourceName", "");
        request.setBodyParams("sync", false);
        try {
            JSONObject response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                    .url(url + "/data-federation/v2.0/channels/write/" + channelId + "/msg")
                    .getResponse(request, JSONObject.class);
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
