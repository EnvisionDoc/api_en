# Search Event

*Note: This documentation is in the progress of translation. Thanks for your visit!*

按条件分页搜索事件。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/events?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|------------------|---------------|----------|---|
| productKey  | False         | String| productKey|
| deviceKey   | False         | String| deviceKey|
| assetId  | False  | String | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid)|
| tslEventKey | False         | String| 事件key|
| tslEventType | False         | String| 事件类型|
| startTime   | False         | String | 开始时间，针对事件的发生时间而言，格式yyyy-MM-dd HH:mm:ss代表查询本地时间,yyyy-MM-ddTHH:mm:ssZ代表utc时间，如果不填，默认最近一周的数据|
| endTime  | False         | String    | 结束时间，针对事件的发生时间而言，格式yyyy-MM-dd HH:mm:ss代表查询本地时间,yyyy-MM-ddTHH:mm:ssZ代表UTC时间，如果不填，默认最近一周的数据|
| expression  | False         | String| 查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1) |
| pagination  | False  |Pagination请求结构体 | 随机分页，默认就是按照occurTime倒序排列，用户不能指定排序字段。默认分页大小是10。参见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)  |



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |  Event结构体      |查询得到的事件列表，见[Event结构体](/docs/api/en/latest/connect/get_event.html#id3) |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/events/search?action=search&orgId=1c499110e8800000
method: POST
requestBody: {"pagination":{"pageNo":1,"pageSize":2},"action":"search"}
```

### 返回示例

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"aae68461-f211-406f-9959-d04af12f28b1",
    "data":[
        {
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
    ],
    "pagination":{
        "sortedBy":null,
        "pageNo":1,
        "pageSize":2,
        "totalSize":1
    }
}
```

