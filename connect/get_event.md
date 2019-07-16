# Get Event



Get the details of the Event via `eventId`.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/events?action=get
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| eventId        | Query| True         | String    |Event ID |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data | Event structure | Event-specific information; see [Event Structure](/docs/api/en/latest/connect/get_event.html#id3) |


### Event structure

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| orgId         | String    | Organization ID which the asset belongs to. |
| eventId         | String    |Event ID |
| productKey   | String         | Product Key identifier             |
| deviceKey    | String         | Device Key identifier              |
| assetId     | String         | Asset ID                  |
| tslEventKey  | String         | Event key in TSL model      |
| tslEventType | String         | Event tupe defined in TSL model |
| output      | String         | Event output              |
| timestamp   | Long           | Event timestamp          |
| localtime   | String         | Local time when event occurs       |


## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/events/get?action=get&id=20190506587247156ca85be5e3422d30e2642dd1&orgId=1c499110e8800000
GET
```

### Return Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"0c45090a-f7c0-476c-8d47-33947d7a57f6",
    "data":{
        "id":"20190506587247156ca85be5e3422d30e2642dd1",
        "orgId":"yourOrgId",
        "productKey":"yourProductKey",
        "deviceKey":"yourDeviceKey",
        "assetId":"wNzx7q3S",
        "tslEventKey":"guzang01",
        "tslEventType":"INFO",
        "output":"{"fioat":116}",
        "timestamp":1557113821000,
        "localTime":"2019-05-06 11:37:01"
    }
}
```

