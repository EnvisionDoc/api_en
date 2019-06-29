# Invoke Service

*Note: This documentation is in the progress of translation. Thanks for your visit!*


向设备下发服务调用接口。

这个接口可以执行缓存命令或者即时命令。当执行即时命令时，需要等待设备返回服务调用的结果后，才返回接口响应数据。如果设备在规定的服务执行超时时间内，未返回服务调用的结果，EnOS服务调用会等待到超时时间后，返回接口超时响应数据。

如果是缓存命令，则直接放入缓存后返回用户。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/commands?action=invokeService
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID。[如何获取assetId信息](/docs/api/zh_CN/latest/api_faqs.html#assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | 设备key|
| serviceId      | Query| True | String    | 被调用服务Id|
| pendingTtl     | Query| False| Integer    | 缓存存储时间，单位为秒 范围[0 - 172800（即48小时）]，默认值为0。当pendingTtl为0时，表示命令即时执行。 |
| timeout        | Query| False         | Integer    | 服务执行超时时间，单位为秒 范围[1 - 60]，默认值为30秒|

## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------|---------------|-------------------|----------|
| inputData | True| Map（Key为String，Value为String，Number，Array或Object） | 服务调用的输入参数，key为参数标识符，value值类型需要符合`ThingModel`的定义。 |




## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |  服务调用返回结构体       | 服务调用结果，见[服务调用返回结构体](/docs/api/zh_CN/latest/connect/invoke_service.html#id4) |


### 服务调用返回结构体

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| commandId  | String| 命令ID|
| outputData | Map（Key为String，Value为String，Number，Array或Object） | 当请求的pendingTtl为0，即请求命令即时执行时，返回设备服务调用结果，需要符合`ThingModel`的定义。当请求的`pendingTtl`不为0，即请求命令缓存执行时，该参数不返回。 |

## 错误码

| 代码  | 描述                                                     |
|-------|------------------------------------------------------------------|
| 11904 | 命令未发送，即时命令超时                         |
| 11915 | 命令已发送，但是响应超时                  |
| 11902 | 缓存命令已达上限                                   |
| 11900 | 设备不在线，即时命令无法发送                                     |
| 11810 | 当Product支持自定义数据格式时，无法将命令编码成Product自定义格式 |
| 11888 | 设备未激活，即时命令无法发送                        |


## 示例 1

### 请求示例

```
https://{apigw-address}/connect-service/v2.1/commands?action=invokeService&deviceKey=zBAofs6D4s&pendingTtl=1000&productKey=6Bt59ySj&serviceId=identifier&orgId=o15535059999891&timeout=30

requestBody:
{"inputData":{"canshu2":22.2,"canshu1":11}}
```

### 返回示例

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": {
        "commandId": "2078724684846989312",
        "outputData": {
        }
    }
}
```

