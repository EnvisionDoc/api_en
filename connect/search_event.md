# Search Event



Search for events by page based on criteria.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/events?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|------------------|---------------|----------|---|
| productKey  | False         | String| Product Key identifier|
| deviceKey   | False         | String| Device Key identifier|
| assetId  | False  | String | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| tslEventKey | False         | String| Event key|
| tslEventType | False         | String| Event type|
| startTime   | False         | String | Start time (with regard to the occurring time of event). The format yyyy-MM-dd HH:mm:ss means local time, yyyy-MM-ddTHH:mm:ssZ means UTC time. If left blank, the data within the last week will be searched|
| endTime  | False         | String    | End time (with regard to the occurring time of event). The format yyyy-MM-dd HH:mm:ss means local time, yyyy-MM-ddTHH:mm:ssZ means UTC time. If left blank, the data within the last week will be searched|
| expression         | False    | String   | Query expression, which supports for sql-like query. The fields that are supported for query include: `productKey`, `deviceKey`, `assetId`, `tslEventKey`, `tslEventType`. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| pagination  | False  |Pagination request struct | Paging parameter; if not specified, 10 entries are displayed per page by default. Currently, sorting is not supported (sorting fields ignored). See [Pagination Request Struct](/docs/api/en/latest/overview.html#pagination-request-struct)  |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Event struct      |List of events from query; see [Event Struct](/docs/api/en/latest/connect/get_event.html#event-struct-event) |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/events/search?action=search&orgId=1c499110e8800000
method:  POST
requestBody:  {"pagination":{"pageNo":1,"pageSize":2},"action":"search"}
```

### Return Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"aae68461-f211-406f-9959-d04af12f28b1",
    "data":[
        {
            "eventId":"20190506587247156ca85be5e3422d30e2642dd1",
            "orgId":"yourOrgId",
            "productKey":"yourProductKey",
            "deviceKey":"yourDeviceKey",
            "assetId":"wNzx7q3S",
            "tslEventKey":"guzang01",
            "tslEventType":"INFO",
            "output":"{"fioat":116}",
            "timestamp":1557113821000,
            "localtime":"2019-05-06 11:37:01"
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

