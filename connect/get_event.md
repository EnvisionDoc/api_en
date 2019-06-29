# Get Event

*Note: This documentation is in the progress of translation. Thanks for your visit!*

通`eventId`获取Event的详细信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/events?action=get
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| eventId        | Query| True         | String    |事件ID |



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |  Event结构体      |Event的具体信息，见[Event结构体](/docs/api/en/latest/connect/get_event.html#id3) |


### Event结构体

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| orgId         | String    | 资产所属的组织ID。|
| eventId         | String    |事件ID |
| productKey   | String         | productKey              |
| deviceKey    | String         | deviceKey               |
| assetId     | String         | 资产id                  |
| tslEventKey  | String         | TSL模型中的事件Key      |
| tslEventType | String         | TSL模型中定义的事件类型 |
| output      | String         | 事件的输出              |
| timestamp   | Long           | 事件发生时间戳          |
| localtime   | String         | 事件发生本地时间        |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/events/get?action=get&id=20190506587247156ca85be5e3422d30e2642dd1&orgId=1c499110e8800000
GET
```

### 返回示例

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"0c45090a-f7c0-476c-8d47-33947d7a57f6",
    "data":{
        "id":"20190506587247156ca85be5e3422d30e2642dd1",
        "orgId":"1c499110e8800000",
        "productKey":"CRJ0mNO1",
        "deviceKey":"99ji8WwMCr",
        "assetId":"wNzx7q3S",
        "tslEventKey":"guzang01",
        "tslEventType":"INFO",
        "output":"{"fioat":116}",
        "timestamp":1557113821000,
        "localTime":"2019-05-06 11:37:01"
    }
}
```

