# Search Event



Search for events by page based on criteria.

## Request format

```
https://{apigw-address}/connect-service/v2.1/events?action=search
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|------------------|---------------|----------|---|
| productKey  | False         | String| productKey|
| deviceKey   | False         | String| deviceKey|
| assetId  | False  | String | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid)|
| tslEventKey | False         | String| Event key|
| tslEventType | False         | String| Event type|
| startTime   | False         | String | Start time (with regard to the occurring time of event). The format yyyy-MM-dd HH:mm:ss means local time, yyyy-MM-ddTHH:mm:ssZ means UTC time. If left blank, the data within the last week will be searched|
| endTime  | False         | String    | End time (with regard to the occurring time of event). The format yyyy-MM-dd HH:mm:ss means local time, yyyy-MM-ddTHH:mm:ssZ means UTC time. If left blank, the data within the last week will be searched|
| expression         | False    | String   | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression)|
| pagination  | False  |Pagination request structure | Random pagination. The default is to sort in descending order by occurTime, and the user can not specify the sorting field. The default pagination size is 10 pages. See [Pagination Request Structure](/docs/api/en/latest/overview.html?highlight=pagination#pagination)  |



## Response parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Event structure      |List of events gotten from query; see [Event Structure](/docs/api/en/latest/connect/get_event.html#id3) |


## Sample 1

### Request sample

```
url:https://{apigw-address}/connect-service/v2.1/events/search?action=search&orgId=1c499110e8800000
method:  POST
requestBody:  {"pagination":{"pageNo":1,"pageSize":2},"action":"search"}
```

### Return sample

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

