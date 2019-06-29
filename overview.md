# 有关EnOS API

*Note: This documentation is in the progress of translation. Thanks for your visit!*

EnOS开放涵盖系统各个核心业务流程的REST API接口。基于这些接口，开发者可以访问系统内的资源，开发各类应用。

## API 列表

EnOS提供以下API服务：

- [接入服务](/docs/api/en/latest/connect/overview.html)：开放EnOS系统在设备连接和设备管理领域的业务能力，包括产品和设备的创建和管理。
- [模型服务](/docs/api/en/latest/model/overview.html)：支持搜索和获取组织内模型的详细信息。
- [资产服务](/docs/api/en/latest/asset/overview.html)：提供组织内资产的创建、管理、更新等服务。
- [告警服务](/docs/api/en/latest/event/overview.html)：提供资产告警的查询和管理服务。 
- [资产树服务](/docs/api/en/latest/asset_tree/overview.html)：提供组织内资产树的创建、管理、更新、查询等服务。
- [TSDB数据服务](/docs/api/en/latest/tsdb_service/overview.html)：提供获取已存储的资产数据服务。
- [TSDB策略服务](/docs/api/en/latest/tsdb_policy/overview.html)：提供获取TSDB存储策略配置信息的服务。

## API Request结构

EnOS API请求包含以下组成部分：

### Request URI

```
{URI-scheme}://{apigw-address}/{service-name}/{version}/{endpoint-URL}?{query-param=value}
```

其中：

- `URI-sheme`：协议，支持HTTPS协议。
- `apigw-address`：该EnOS环境API服务的地址，其范式为`apim-{enos-environment}.envisioniot.com`，其中`enos-environment`为EnOS的部署环境名称。
- `service-name`：服务名称，如`asset-service`。
- `version`：API版本，如`v2.0`。
- `endpoint-URL`：资源及对资源的操作，如`assets/update`。
- `query-param`：对目标资源的选择条件，如`orgId=1234`。当有多个query参数时，用`&`符号连接。

以获取某OU内某个资产信息为例，API请求格式如下：

```
GET
https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=1234&assetId=abcd
```

### Request Header

Request URI的REST API规范和HTTP规范所需的任何其他字段，绑定在request header中。

常用的request header为`Content-Type`，代表数据提交方式，一般情况下它的值可设为`application/json;charset=UTF-8`；若执行文件上传或其他表单提交，值设为`multipart/form-data;charset=UTF-8`。

### Request Body

用于补充Request URI以提供更加复杂的输入参数，如以下示例request body中包含的参数指定了更新资产的时区、描述、标签等属性：

```
POST
https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId=1234&isPatchUpdate=fasle
{
  "asset": {
    "modelId": "testModel",
    "assetId": "123",
    "timezone": "+08:00",
    "description": "hahdesc",
    "tags": {
      "site": "Shanghai",
      "producer": "ABC"
    }
  }
}
```

## API Response结构

EnOS API的返回为以下格式的JSON结构体：

```
{
  "code": 0,
  "msg": "OK",
  "requestId": "6cb7a013-7f83-4620-97c8-4695a892acdf",
  "data": {
  }
}
```

对返回参数的详细说明如下：

| 名称      | 数据类型        | 是否必需 | 描述                                                         |
| :-------- | --------------- | :------- | ------------------------------------------------------------ |
| code      | Integer         | true     | API请求状态码，0表示请求成功。其它状态码的含义，参考公共返回码和API文档中的错误码解释。 |
| msg       | String          | true     | 对状态码的解释和说明。成功为“OK”。若API请求失败，返回具体错误信息。 |
| requestId | String          | true     | 每次请求获取的id，用于唯一标识一次API请求。                  |
| data      | Array 或 Object | false    | API响应返回结果集，数据类型包括：基本数据类型、复杂类型或数组。 |

## 公共参数说明

对各API服务的公共参数说明如下：

### 公共请求参数（接入服务等）

接入服务、模型服务、资产服务、事件服务、和资产树服务API的公共请求参数为：

#### Pagination请求结构体

Pagination参数表示随机分页。默认分页大小是10。

| 名称     | 数据类型          | 是否必需 | 描述                  |
| -------- | ----------------- | -------- | --------------------- |
| pageNo   | Integer           | true     | 请求页数，从1开始     |
| pageSize | Integer           | true     | 每页记录数，必须大于0 |
| sorters  | Sorter结构体Array | false    | 分页排序方式          |

**Sorter结构体**

| 名称  | 数据类型 | 是否必需 | 描述                                          |
| ----- | -------- | -------- | --------------------------------------------- |
| field | String   | true     | 分页字段名称                                  |
| order | String   | false    | ASC表示正序排序、DESC表示倒序排序，默认为正序 |

**Pagination参数示例**

```
{
    "pagination": {
        "pageNo": 2,
        "pageSize": 100,
        "sorters": [{
            "field": "assetId",
            "order": "ASC"
        }]
    }
}
```

#### Projection参数

Projection参数用于对返回data结果集的裁剪，数据类型为String Array。其中每个String表示返回结果中需要返回的一个结果字段。没有在projection中指定的字段，在结果集中不返回。在指定字段时，可以使用：

|符号|描述|
|------------|--------------|
|`[*]`|	表示一个Array中的每一个对象|
|`*`  |		表示任意字段值|
|`.`	|	表示子字段|


当不提供projection参数时，表示不对data结果集做裁剪。

**Projection参数示例**

```
{
    "projection": [
        "assetPaths”, “assets.*.assetId”
        ]
}
```

### 公共返回参数（接入服务等）<public-response>

接入服务、模型服务、资产服务、事件服务、和资产树服务API的公共返回参数为：

| 名称       | 数据类型             | 是否必需 | 描述                   |
| :--------- | -------------------- | :------- | ---------------------- |
| pagination | Pagination响应结构体 | false    | 当前返回结果的分页信息 |

### 公共返回码（接入服务等）

接入服务、模型服务、资产服务、事件服务、和资产树服务API的公共返回码为：

| **Code**  | **描述**                                                     |
| --------- | ------------------------------------------------------------ |
| **99400** | 请求参数非法，请检查请求参数。                               |
| **99403** | 缺少权限，请检查是否有访问接口和请求资源的权限。             |
| **99404** | 指定的对象不存在。例如，在获取、更新、删除指定的设备时，指定的设备deviceKey不存在。 |
| **99500** | 服务器内部错误，请联系EnOS。                                 |

示例：

```
99400 错误示例：参数缺失
{
    "code": 99400,
    "msg": "Invalid Argument action:action is missing",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99400 错误示例：参数错误
{
    "code": 99400,
    "msg": "Invalid Argument orgId: orgId does not exist",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99403 错误示例：缺少权限 
{
    "code": 99403,
    "msg": “Denied resource: orgId o15589291276361",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99500 错误示例：服务器内部错误
{
    "code": 99500,
    "msg": " Internal Server Error",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}
```

### 公共返回码（TSDB数据服务）

TSDB数据服务API的公共返回码为：

| Code | Msg / submsg                                                 | 描述                                                         |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 400  | You do not have permission for the   following assets        | 当前App对以下设备没有权限                                    |
| 400  | Exception: Invalid param accessKey                           | 参数accessKey有误                                            |
| 400  | xxx is required                                              | xxx参数不能为空                                              |
| 400  | All asset authentication failed                              | 当前App对查询的所有设备都没有权限                            |
| 400  | Invalid Argument                                             | 参数无效或缺失                                               |
| 400  | [modelId] permission denied                                  | [modelId]无效或无权限访问                                    |
| 430  |                                                              | 请求超出服务内部的网络传输的最大限制                                     |
| 701  |                                                              | 服务出错                                                     |
| 702  | Params startTime or endTime is   invalid, and date format of them should be consistent | 时间格式错误，local时间格式为YYYY-MM-DD HH:MM:SS；UTC时间格式需要加入时区信息，例如：2019-06-01T00:00:00+08:00 |
| 702  | xxx cannot be null or negative                               | 参数xxx不可为空或者为负数                                    |
| 702  | xxx is empty                                                 | 参数xxx不可为空                                              |
| 702  | only one xxx is allowed                                      | 参数xxx至多一个                                              |
| 702  | assetIds size * measurepoints size *   pageSize is too large to query, result size may exceed RPC limit | 单次查询结果集过大,要求设备数\*测点数\*pageSize<=640000                                           |
| 702  | param xxx is invalid                                         | 参数xxx无效                                                  |
| 702  | endTime should not be later than   startTime                 | 查询结束时间应比开始时间晚                                   |
| 702  | is not a valid integer                                       | 参数不是一个有效的整数类型                                   |
| 702  | assetIds or measurepoint does not   match the model          | 设备或测点与模型不匹配                                       |
| 702  | Please config/check storage group for   org[] and model[]    | 未配置存储策略或modelId有误                                  |

## API鉴权<authentication>

EnOS API身份验证采用服务账号SA（service account）作为应用或者开发者的身份，在REST API请求中将SA发送到EnOS服务，通过它验证用户身份并执行所需的授权访问。 

### 获取服务账号

服务账号SA由应用的 `AccessKey` 和 `SecretKey` 组成，需要通过在EnOS控制台注册应用生成，具体步骤如下：

1. 登录EnOS控制台，在左侧导航栏中选择 **应用注册**。
2. 点击 **创建应用** 按钮，输入新应用的详细信息后，点击 **确认**。
3. 应用注册完成之后，在 **组织应用** 标签下，点击应用名称，打开 **应用详情** 页面，查看应用的 `AccessKey` 和 `SecretKey` 。

### 授权服务账号

必须对服务账号进行授权之后，应用程序才有权访问EnOS上被授权的资源。对服务账号授权的详细步骤，请参考[管理服务账号](/docs/iam/en/latest/howto/service_account/managing_service_account.html)。

### API操作权限

在授权服务账号前，需创建相应的权限策略。各API接口需要访问的资源和相应的操作权限说明如下：

| 接口名称                       | 所需授权              | 所需操作权限 |
| ------------------------------ | --------------------- | ------------ |
| Get Electric Power             | Asset                 | read         |
| Get Current Day Electric Power | Asset                 | read         |
| Filter Latest Data             | Asset                 | read         |
| Get Latest Data                | Asset                 | read         |
| Get Generic Data               | Asset                 | read         |
| Get DI Data                    | Asset                 | read         |
| Get AI Normalized Data         | Asset                 | read         |
| Get AI Data                    | Asset                 | read         |
| Get Raw Data                   | Asset                 | read         |
| Get TSDB Storage Policy        | Asset                 | read         |
| UpdateAsset                    | Asset                 | Write        |
| AssociateAssetNode             | Asset Tree Management | Full-Access  |
| DeleteAssetNode                | Asset Tree Management | Full-Access  |
| CreateAssetNode                | Asset Tree Management | Full-Access  |
| Cancel Command                 | Device Management     | Full-Access  |
| Set Measurepoint               | Asset                 | Control      |
| Invoke Service                 | Asset                 | Control      |
| Create Product                 | Device Management     | Full-Access  |
| Update Product                 | Device Management     | Full-Access  |
| Delete Product                 | Device Management     | Full-Access  |
| Disable Device                 | Device Management     | Full-Access  |
| Enable Device                  | Device Management     | Full-Access  |
| Delete Device                  | Device Management     | Full-Access  |
| Create Device                  | Device Management     | Full-Access  |
| Update Device                  | Device Management     | Full-Access  |
| Add Sub-device                 | Device Management     | Full-Access  |
| Remove Sub-device              | Device Management     | Full-Access  |

创建权限策略的详细步骤，请参考[创建和管理策略](/docs/iam/en/latest/howto/managing_policies.html)。