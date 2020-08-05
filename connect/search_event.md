# Search Event

Search for events based on the search criteria.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Control

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.1/events?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)

| Name | Mandatory/Optional | Data Type | Description |
|------------------|---------------|----------|---|
| productKey  | Optional         | String| The product key.|
| deviceKey   | Optional         | String| The device key.|
| assetId  | Optional  | String | The asset ID. [How to get assetId>>](/docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid)|
| tslEventKey | Optional         | String| The event key.|
| tslEventType | Optional         | String| The event type.|
| startTime   | Optional         | String | The start time of the event. The format yyyy-MM-dd HH:mm:ss means local time, yyyy-MM-ddTHH:mm:ssZ means UTC time. If not specified, the data within the last week will be searched.|
| endTime  | Optional         | String    | The end time of the event. The format yyyy-MM-dd HH:mm:ss means local time, yyyy-MM-ddTHH:mm:ssZ means UTC time. If not specified, the data within the last week will be searched.|
| expression         | Optional    | String   | The query expression, which supports sql-like query. The fields that are supported for query include: `productKey`, `deviceKey`, `assetId`, `tslEventKey`, and `tslEventType`. The supported arithmetic operators are "=" and "in", and the logical operator is "and" and "or". [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)|
| pagination  | Optional  |Pagination Request Struct | Lists the paging requirements in a request. When not specified, 10 entries are displayed per page by default. `sorters` is not supported to sort the response. The items in the response is arranged in descending order based on `createTime`. See [Pagination Request Struct>>](/docs/api/en/2.1.0/overview.html#pagination-request-struct)  |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |  Array of Event Structs      | A list of the events returned. For details of an Event Struct, see [Event Struct](search_event#event-struct-event) |


### Event Struct <event>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| orgId         | String    | The organization ID which the asset belongs to. |
| eventId         | String    |The event ID. |
| productKey   | String         | The product key.             |
| deviceKey    | String         | The device key.              |
| assetId     | String         | The asset ID.                  |
| tslEventKey  | String         | The event key in TSL model.      |
| tslEventType | String         | The event type defined in TSL model. |
| output      | String         | The event output.              |
| timestamp   | Long           | The event timestamp.         |
| localtime   | String         | The local time when the event occurs.       |





## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/events?action=search&orgId=yourOrgId
method: POST
requestBody:  
{
    "pagination":{
        "pageNo":1,
        "pageSize":2
    },
    "action":"search"
}
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
	"output":"{\"float\":116}",
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

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.event;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.api.common.constant.request.Pagination;
import com.envisioniot.enos.connect_service.v2_1.event.SearchEventRequest;
import com.envisioniot.enos.connect_service.v2_1.event.SearchEventResponse;
import com.google.gson.Gson;

public class SearchEvent {
    public static void main(String[] args) {


        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";

        SearchEventRequest request = new SearchEventRequest();
        Pagination pagination = new Pagination();
        pagination.setPageNo(1);
        pagination.setPageSize(2);
        request.setPagination(pagination);
        request.setOrgId("yourOrgId");
        try {
            SearchEventResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                    .url("yourServerUrl")
                    .getResponse(request, SearchEventResponse.class);
            Gson gson = new Gson();
            System.out.println(gson.toJson(response));
        } catch (Exception e) {
            System.out.print(e);
        }
    }
}
```
