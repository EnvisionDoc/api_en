# Set Measurepoint

*Note: This documentation is in the progress of translation. Thanks for your visit!*

测点设置接口。

本接口用于执行缓存命令或者即时命令。当执行即时命令时，需要等待设备返回测点设置结果后才返回接口响应数据。如果设备在规定的测点设置超时时间内，未返回测点设置的结果，EnOS测点设置会等待到超时时间后，返回接口超时响应数据。

如果是缓存命令，则直接放入缓存后返回用户。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/commands?action=setMeasurepoint
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/zh_CN/latest/api_faqs#orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/zh_CN/latest/api_faqs.html#assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | 设备key|
| measurepointId      | Query| True | String    | 资产测点。[如何获取测点（pointId）信息](/docs/api/zh_CN/latest/api_faqs#pointid-pointid)|
| pendingTtl     | Query| False| Integer    | 缓存存储时间，单位为秒 范围[0 - 172800（即48小时）]，默认值为0。当pendingTtl为0时，表示命令即时执行。 |
| timeout        | Query| False         | Integer    | 服务执行超时时间，单位为秒 范围[1 - 60]，默认值为30秒|

## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------|---------------|-------------------|----------|
| value | True| String，Number，Array或Object | 测点设置的参数值，需要符合`ThingModel`的定义。 |




## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |  测点设置返回结构体      | 测点设置结果，见[测点设置返回结构体](/docs/api/zh_CN/latest/connect/set_measurepoint.html#id4) |


### 测点设置返回结构体

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| commandId  | String| 命令ID|

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
https://{apigw-address}/connect-service/v2.1/commands?measurepointId=measurepoint1&action=setMeasurepoint&deviceKey=zBAofs6D4s&pendingTtl=1000&productKey=6Bt59ySj&orgId=o15535059999891&timeout=30

{"value":1.0}
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
     }
}
```

