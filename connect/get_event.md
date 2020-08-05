# Get Event

Get the details of an event via ``eventId``.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Control

## Request Format

```
GET https://{apigw-address}/connect-service/v2.1/events?action=get
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| eventId        | Query| Mandatory         | String    | The event ID |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data | Event Struct | The details of the event. See [Event Struct](/docs/api/en/2.1.0/connect/get_event.html#event-struct-event). |


### Event Struct <event>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| orgId         | String    | The organization ID which the asset belongs to. |
| eventId         | String    |The event ID. |
| productKey   | String         | The product key.             |
| deviceKey    | String         | The device key.              |
| assetId     | String         | The asset ID                 |
| tslEventKey  | String         | The event key in the TSL model.      |
| tslEventType | String         | The event type defined in the TSL model. |
| output      | String         | The event output.              |
| timestamp   | Long           | The event timestamp.          |
| localtime   | String         | The local time when the event occurs.       |


## Samples

### Request Sample

```JSON
url: https://{apigw-address}/connect-service/v2.1/events?action=get&eventId=yourEventId&orgId=yourOrgId
method: GET
```

### Return Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"0c45090a-f7c0-476c-8d47-33947d7a57f6",
    "data":{
        "eventId":"20190506587247156ca85be5e3422d30e2642dd1",
        "orgId":"yourOrgId",
        "productKey":"yourProductKey",
        "deviceKey":"yourDeviceKey",
        "assetId":"wNzx7q3S",
        "tslEventKey":"guzang01",
        "tslEventType":"INFO",
        "output":"{\"float\":116}",
        "timestamp":1557113821000,
        "localtime":"2019-05-06 11:37:01"
    }
}
```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.event;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.event.GetEventRequest;
import com.envisioniot.enos.connect_service.v2_1.event.GetEventResponse;
import com.google.gson.Gson;


public class GetEvent {
    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";

        GetEventRequest request = new GetEventRequest();
        request.setOrgId("yourOrgId");
        request.setEventId("yourEventId");
        try {
            GetEventResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url("yourServerUrl")
                .getResponse(request, GetEventResponse.class);
            Gson gson = new Gson();
            System.out.println(gson.toJson(response));
        } catch (Exception e) {
            System.out.print(e);
        }
    }
}
```