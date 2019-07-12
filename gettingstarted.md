# Get Started EnOS API



This tutorial is intended to guide you through an example of completing your first EnOS API invocation task.

## Prerequisites

The following preparations are required to invoke the EnOS API:

**Get the service account**

You have gotten the service account that can be used for identity authorization when invoking the API. For detailed steps, see [API Authentication] (overview#authentication).

**Get resource permissions**

The service account has the permissions to access to related resources in the system. For details, see [Managing Service Accounts] (/docs/iam/en/latest/howto/service_account/managing_service_account.html).

**Prepare the development environment**

Install the SDK provided by EnOS and prepare the basic environment for API invocation. Refer to the following details:

### Invoking SDK with Java
To invoke the SDK using Java, you need to install the Java core SDK (Poseidon). Poseidon supports Java 7 and above.

#### Installation method
Visit [Maven Warehouse](https://mvnrepository.com/artifact/com.envisioniot/apim-poseidon/0.1.7), and download Poseidon Jar installation package into your application. If the application uses the `pom` project, add the following dependencies to the `pom.xml` file:

```xml
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>apim-poseidon</artifactId>
  <version>0.1.7</version>
</dependency>
```
#### How to use

**Synchronous request**

1. No verification for API. The sample codes are given as follows:

   ```
   Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey))
           .url("https://{apigw-address}/fire/1.0.0/getNews?page=1&count=10")
           .method("GET")
           .sync();
   ```

2. Enable the API log. The sample codes are given as follows:

   ```
   Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey).debug())
           .url("https://{apigw-address}/fire/1.0.0/getNews?page=1&count=10")
           .method("GET")
           .sync();
   ```

3. Post request. The sample codes are given as follows:

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

**Asynchronous request**

The sample codes are given as follows:

```java
Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey))
        .url("https://{apigw-address}/fire/1.0.0/getNews?page=1&count=10")
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

**Request and Response supported**

The sample codes are given as follows:

```java
UserRequest userRequest = new UserRequest();
userRequest.setAge("12");
userRequest.setQueryPath("1234");
userRequest.setX_custom_header("ni hao shanghai");

UserResponse response = Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey).debug())
            .url("https://{apigw-address}")
            .getResponse(userRequest, UserResponse.class);
```
.. note:: Request provides the built-in support for the Header, Query, RequestBody and Path parameters; In case of an exception, it is required to capture the PoseidonException exception to view specific issues.

### Invoke SDK with Python
To invoke the SDK using Python, you need to install the Python core SDK (Athena).

#### Installation method

Install it using the following pip command:

```
pip install aphrodite
```

#### How to use

**Query** 

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/tttttttt/v1/tyy?sid=28654780'

req = poseidon.urlopen(accessKey, secretKey, url)
print(req)
```
**Header**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/tttttttt/v1/tyy?sid=28654780'

header={}

req = poseidon.urlopen(accessKey, secretKey, url, None, header)
print(req)

```

**Body**

```python
from poseidon import poseidon

accessKey = 'accessKey'
secretKey = 'secretKey'

url = 'https://{apigw-address}/tttttttt/v1/tyy?sid=28654780'

data = {"username": "11111", "password": "11111"}

req = poseidon.urlopen(accessKey, secretKey, url, data)
print(req)

```

## Invoking EnOS API

After the development environment is ready, refer to the parameter descriptions and invocation examples in the API interface documentation to invoke the API.

### Sample

The following sample show how to get the asset details using the Java SDK to invoke *Get Asset* API:

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class demo {
    public static void main(String[] args) {

        String accessKey = "app_Key";
        String secretKey = "app_Secret";

        String response = Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey))
                .url("https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId={org_id}&assetId={asset_id}")
                .method("GET")
                .sync();
        System.out.println(response);
        }
    }
```

After the above-mentioned sample codes are executed, the sample of returned data is given as follows:

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
    "orgId": "org_id",
    "desc": null,
    "tags": {}
  },
  "requestId": "9a5cfbac-b2f8-4a37-b38d-8bccdd77d073"
}
```

