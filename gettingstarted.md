# EnOS API 快速入门

*Note: This documentation is in the progress of translation. Thanks for your visit!*

该教程通过一个例子带着你完成你的第一个EnOS API调用任务。

## 前提条件

调用EnOS API需完成以下准备：

**获取服务账号**

已获取用于调用API时，用于身份授权的服务账号。详细步骤，参考[API鉴权](overview#authentication)。

**获取资源权限**

服务账号已取得系统中相关资源的访问权限。详细信息，参考[管理服务账号](/docs/iam/en/latest/howto/service_account/managing_service_account.html)。

**准备开发环境**

安装EnOS提供的SDK，准备调用API的基础环境。参考以下详细介绍：

### 使用Java调用SDK
使用Java调用SDK，需要安装Java core SDK（Poseidon）。Poseidon支持Java 7及以上版本。

#### 安装方法
访问[Maven仓库](https://mvnrepository.com/artifact/com.envisioniot/apim-poseidon/0.1.7)，下载Poseidon Jar安装包，在应用中引入Jar安装包。如果应用使用`pom`工程，则在`pom.xml`文件中加入以下依赖：

```xml
<dependency>
  <groupId>com.envisioniot</groupId>
  <artifactId>apim-poseidon</artifactId>
  <version>0.1.7</version>
</dependency>
```
#### 使用方法

**同步请求**

1. API无校验，示例代码如下：

   ```
   Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret))
           .url("https://{apigw-address}/fire/1.0.0/getNews?page=1&count=10")
           .method("GET")
           .sync();
   ```

2. 开启API日志，示例代码如下：

   ```
   Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
           .url("https://{apigw-address}/fire/1.0.0/getNews?page=1&count=10")
           .method("GET")
           .sync();
   ```

3. Post请求，示例代码如下：

   ```
   Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
               .url("https://{apigw-address}/lily/0.0.1/getPublic")
               .method("POST")
               .header("Content-Type", "application/json")
               .header("Cookie", "global_id=IAM_S_S7Yd5WXssqEBCququgzeR9JLNBnWr99S")
               .requestBody(
                   "{\n" + "  \"op\": \"pl\",\n" + "  \"offset\": 0,\n" + "  \"limit\": 10\n" + "}")
               .sync();
   ```

**异步请求**

示例代码如下：

```java
Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret))
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

**支持Request和Response**

示例代码如下：

```java
UserRequest userRequest = new UserRequest();
userRequest.setAge("12");
userRequest.setQueryPath("1234");
userRequest.setX_custom_header("ni hao shanghai");

UserResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url("https://{apigw-address}")
            .getResponse(userRequest, UserResponse.class);
```
.. note:: Request内置支持Header，Query，RequestBody，Path参数；异常情况需捕获PoseidonException异常查看具体问题。

### 使用Python调用SDK
使用Python调用SDK，需要安装Python core SDK（Athena）。

#### 安装方法

通过以下pip命令安装：

```
pip install aphrodite
```

#### 使用方法

**Query** 

```python
from poseidon import poseidon

appkey = 'appKey'
appsecret = 'appSecret'

url = 'https://{apigw-address}/tttttttt/v1/tyy?sid=28654780'

req = poseidon.urlopen(appkey, appsecret, url)
print(req)
```
**Header**

```python
from poseidon import poseidon

appkey = 'appKey'
appsecret = 'appSecret'

url = 'https://{apigw-address}/tttttttt/v1/tyy?sid=28654780'

header={}

req = poseidon.urlopen(appkey, appsecret, url, None, header)
print(req)

```

**Body**

```python
from poseidon import poseidon

appkey = 'appKey'
appsecret = 'appSecret'

url = 'https://{apigw-address}/tttttttt/v1/tyy?sid=28654780'

data = {"username": "11111", "password": "11111"}

req = poseidon.urlopen(appkey, appsecret, url, data)
print(req)

```

## 调用EnOS API

开发环境准备完成后，参考各API接口文档中的参数说明和调用示例，调用API。

### 示例

以下示例为使用Java SDK调用*Get Asset* API获取资产详细信息：

```java
import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;

public class demo {
    public static void main(String[] args) {

        String appKey = "app_Key";
        String appSecret = "app_Secret";

        String response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret))
                .url("https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId={org_id}&assetId={asset_id}")
                .method("GET")
                .sync();
        System.out.println(response);
        }
    }
```

以上示例代码运行完成后，返回数据示例为：

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

