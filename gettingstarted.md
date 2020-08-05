# Get Started with EnOS API

<br />

This tutorial will guide you in your first EnOS API request, with the help of examples.

## Prerequisites

The following preparations are required to invoke the EnOS API:

<br />

**Get the service account**

Get the service account that can be used for identity authorization when invoking the API. Refer to [API Authentication](authen_overview) for details.

<br />

**Get resource permissions**

Get the resource permissions by authorizing the service acccount for the applications. Refer to [Managing Service Accounts](/docs/enos/en/2.1.0/iam/howto/service_account/managing_service_account.html) for details.

<br />

**Prepare the development environment**

Install the EnOS SDK and prepare the basic environment for API requests. Refer to the methods below for details.


### Invoking SDK with Access Token


- [Get Access Token](get_access_token)
- [Refresh Access Token](refresh_access_token)
- [Invoke API with Access Token](invoke_api_with_access_token)


### Invoking SDK with Java

To invoke the SDK using Java, install the Java Core SDK (Poseidon). Poseidon supports Java 7 and onwards.

<br />

To invoke Connection Service and Asset Service APIs, install the Device and Asset API Pojo SDK.

#### Installation Method

**Java core SDK (Poseidon)**

Open the [Maven Repository](https://mvnrepository.com/artifact/com.envisioniot/apim-poseidon) of the SDK, download the installation package, and import it to your development environment. If your application uses the `pom` project, add the following dependencies to the `pom.xml` file (you may need to change the version number):

```
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>apim-poseidon</artifactId>
  <version>0.1.12</version>
</dependency>
```

<br />

**Device and Asset API Pojo SDK**

Open the [Maven Repository](https://search.maven.org/artifact/com.envisioniot/enos-dm-api-pojo) of the SDK, download the installation package, and import it to your development environment. If your application uses the `pom` project, add the following dependencies to the `pom.xml` file (you may need to change the version number):

```
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>enos-dm-api-pojo</artifactId>
  <version>0.2.13</version>
</dependency>
```

#### Request Method

**Synchronous Request**

1. For the GET method, if the API logging feature is disabled, only the result is returned after calling the API. The sample code is as follows:

   ```
   Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
        .url("https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
        .method("GET")
        .sync();
   ```

2. For the GET method, if the API logging feature is enabled, both the request parameters with time stamp and response are returned after calling the API. The sample code is as follows:

   ```
   Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
        .url("https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
        .method("GET")
        .sync();
   ```

3. For the POST method, the sample code is as follows:

   ```
   Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey).debug())
               .url("https://{apigw-address}/lily/0.0.1/getPublic")
               .method("POST")
               .header("Content-Type", "application/json")
               .header("Cookie", "global_id=IAM_S_S7Yd5WXssqEBCququgzeR9JLNBnWr99S")
               .requestBody(
                   "{\n" + "  \"op\": \"pl\",\n" + "  \"offset\": 0,\n" + "  \"limit\": 10\n" + "}")
               .sync();
   ```


.. note:: Request header is optional. Specifications such as the type of request content can be included in the header as needed.

<br />

**Asynchronous Request**

The sample code is as follows:

```java
Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
        .url("https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}")
        .method("GET").async( new PoseidonListener() {
              @Override
              public void onFailure(String errorMessage) {
                // TODO
              }

              @Override
              public void onResponse(String body) {
                // TODO
              }
            });
```

<br />

**Support for Request and Response**

Request provides the built-in support for the Header, Query, RequestBody, and Path parameters. For how to use Request and Response, see Sample 3 and Sample 4 below.

<br />

**Exception Handling**

Capture the PoseidonException to view specific API exception issues. For API service errors, refer to the API documentation.

<br />

Common error messages and description returned from PoseidonException are as follows:

.. list-table::
   :widths: 15 25 25 35
   :header-rows: 1

   * - Code
     - Description
     - Message
     - Cause
   * - 400
     - Bad Request
     - Cannot process request body
     - Failed to get request body.
   * - 401
     - Unauthorized
     - Invalid authentication credentials
     - Failed to authenticate the identification.
   * - 403
     - Forbidden
     - Your IP address is not allowed
     - The IP address is not allowed to access.
   * - 413
     - Payload Too Large
     - Request size limit exceeded
     - The request size exceeded the limit.
   * - 429
     - Too Many Requests
     - API rate limit exceeded
     - The number of requests exceeded the API request limit.
   * - 500
     - Internal Server Error
     - An unexpected error occurred
     - Failed to search from cache.
   * - 503
     - Service unavailable
     - Service unavailable
     - The service is not allowed to access.


### Invoking SDK with Python

To invoke the SDK using Python, install the Python core SDK (Athena) V0.1.4 or later. Athena supports Python 3.6 and onwards.

#### Installation Method

Install it by the following pip command:

```
pip install aphrodite
```

#### Request Method

**Query**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}'

req = poseidon.urlopen(accessKey, secretKey, url)
print(req)
```

<br />

**Header**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}'

header={}

req = poseidon.urlopen(accessKey, secretKey, url, None, header)
print(req)
```

<br />

**Body**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/{service-name}/{api-version}/{api_name}?{param1=value1&param2=value2}'

data = {"username": "abc", "password": "123"}

req = poseidon.urlopen(accesskey, secretkey, url, data)
print(req)
```

## Invoking EnOS API

After the development environment is ready, refer to the parameter descriptions and invocation examples in the API documentation to invoke the API.

### Sample 1 - Using Java core SDK (GET Method)

The following sample shows how to get the asset details by using the Java core SDK to invoke the *Get Asset* API (with API logging feature disabled):

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class GetAsset {
    public static void main(String[] args) {

        String accessKey = "{access_key_of_the_application}";
        String secretKey = "{secret_key_of_the_application}";

        String response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey))
                .url("https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId={org_id}&assetId={asset_id}")
                .method("GET")
                .sync();
        System.out.println(response);
        }
    }
```

<br />

The returned data sample is as follows:

```
{
  "msg": OK,
  "code": 0,
  "data": {
    "modelId": "model_id",
    "assetId": "asset_id",
    "timezone": "+08:00",
    "name": {
      "i18nValue": {},
      "defaultValue": "asset_name"
    },
    "attributes": {
      "system": "System"
    },
    "modelIdPath": null,
    "orgId": "yourOrgId",
    "desc": null,
    "tags": {}
  },
  "requestId": "9a5cfbac-b2f8-4a37-b38d-8bccdd77d073"
}
```

### Sample 2 - Using Java core SDK (POST Method)

The following sample shows how to update the name, description, attributes, timezone, and tags of an asset by using the Java core SDK to invoke the *Update Asset* API (with API logging feature enabled):

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class UpdateAsset {
    public static void main(String[] args) {

        String accessKey = "{access_key_of_the_application}";
        String secretKey = "{secret_key_of_the_application}";

        String data = "{\"asset\":{\"assetId\":\"{asset_id}\",\"name\":{\"defaultValue\":\"Device_Name\",\"i18nValue\":{\"en_US\":\"Device_Name\",\"zh_CN\":\"Chinese name\"}},\"description\":\"Device_Description\",\"attributes\":{\"Brand\":\"Brand_Name\"},\"timezone\":\"+07:00\",\"tags\":{\"year\":\"2019\",\"site\":\"Site_Name\"}}}";

        String response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url("https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId={org_id}")
                .method("POST")
                .requestBody(data)
                .sync();
        System.out.println(response);
    }
}
```

<br />

The returned data sample is as follows:

```
2019-7-10 16:35:12 [Poseidon] url: https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId={org_id}
2019-7-10 16:35:12 [Poseidon] method: POST
2019-7-10 16:35:12 [Poseidon] headers: {}
2019-7-10 16:35:12 [Poseidon] requestBody: {"asset":{"assetId":"{asset_id}","name":{"defaultValue":"Device_Name","i18nValue":{"en_US":"Device_Name","zh_CN":"Chinese name"}},"description":"Device_Description","attributes":{"Brand":"Brand_Name"},"timezone":"+07:00","tags":{"year":"2019","site":"Site_Name"}}}
2019-7-10 16:35:13 [Poseidon] responseBody: {"code":0,"msg":"OK","requestId":"9d6b9869-4ffd-4964-a8ff-d150a0d1a91f","data":null}
```

### Sample 3 - Using Java core SDK and Device and Asset API Pojo SDK (GET Method)

The following sample shows how to get the asset details by using the Java core SDK and the Device and Asset API Pojo SDK to invoke the *Get Asset* API (with API logging feature enabled):

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.asset_service.v2_1.GetAssetRequest;
import com.envisioniot.enos.asset_service.v2_1.GetAssetResponse;

public class GetAsset {
    private static String accessKey = "{access_key_of_the_application}";
    private static String secretKey = "{secret_key_of_the_application}";
    private static String orgId = "{org_id}";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        GetAssetRequest request = new GetAssetRequest();
        request.setOrgId(orgId);
        request.setAssetId("{asset_id}");

        GetAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getCode());
    }
}
```

<br />

The returned data sample is as follows:

```
2019-7-10 11:02:27 [Poseidon] url: https://{apigw-address}/asset-service/v2.1/assets?action=get&assetId={asset_id}&orgId={org_id}
2019-7-10 11:02:27 [Poseidon] method: GET
2019-7-10 11:02:27 [Poseidon] headers: {}
2019-7-10 11:02:27 [Poseidon] requestBody: null
2019-7-10 11:02:29 [Poseidon] responseBody:{
  "msg": OK,
  "code": 0,
  "data": {
    "modelId": "model_id",
    "assetId": "asset_id",
    "timezone": "+08:00",
    "name": {
      "i18nValue": {},
      "defaultValue": "asset_name"
    },
    "attributes": {
      "system": "System"
    },
    "modelIdPath": null,
    "orgId": "yourOrgId",
    "desc": null,
    "tags": {}
  },
  "requestId": "39346a7e-1da8-42ec-9620-d44ef6e2e2b6"
}
```

### Sample 4 - Using Java core SDK and Device and Asset API Pojo SDK (POST Method)

The following sample shows how to update the description, attributes, and timezone of an asset by using the Java core SDK and the Device and Asset API Pojo SDK to invoke the *Update Asset* API (with API logging feature enabled):

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.asset_service.v2_1.UpdateAssetRequest;
import com.envisioniot.enos.asset_service.v2_1.UpdateAssetResponse;
import com.envisioniot.enos.asset_service.vo.AssetUpdateVo;

import java.util.HashMap;
import java.util.Map;

public class UpdateAsset {
    private static String accessKey = "{access_key_of_the_application}";
    private static String secretKey = "{secret_key_of_the_application}";
    private static String orgId = "{org_id}";
    private static String url = "https://{apigw-address}";

    public static void main(String[] args) {
        UpdateAssetRequest request = new UpdateAssetRequest();
        request.setOrgId(orgId);

        AssetUpdateVo asset = new AssetUpdateVo();
        asset.setAssetId("{asset_id}");
        Map<String, Object> newAttrs = new HashMap<>();
        newAttrs.put("Brand","Brand_Name");
        asset.setAttributes(newAttrs);
        asset.setDescription("Device_Description");
        asset.setTimezone("+08:00");

        request.setAsset(asset);
        request.setIsPatchUpdate(true);

        UpdateAssetResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response);
    }
}
```

<br />

The returned data sample is as follows:

```
2019-7-10 16:45:00 [Poseidon] url: https://{apigw-address}/asset-service/v2.1/assets?action=update&isPatchUpdate=true&orgId={org_id}
2019-7-10 16:45:00 [Poseidon] method: POST
2019-7-10 16:45:00 [Poseidon] headers: {}
2019-7-10 16:45:00 [Poseidon] requestBody: {"asset":{"assetId":"{asset_id}","attributes":{"Brand":"Brand_Name"},"description":"Device_Description","timezone":"+08:00"}}
2019-7-10 16:45:01 [Poseidon] responseBody: {"code":0,"msg":"OK","requestId":"4c1a6da8-bd89-4001-b8fd-5fa65ab816f2","data":null}
```
