# Search Thing Model

Search thing models by orgId.

## Request Format

```
https://{apigw-address}/model-service/v2.1/thing-models?action=search
```

## Request Parameters (Body)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|:-----------|:-----------------|:---------|:----------|:-----------------------------------------------------------------------------------------|
| orgId   | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)|
| scope   | Query            | False    | Integer   | Query scope.  0- Only search from the organization specified by the `orgId`; 1 - Search from the organization specified by the `orgId` and the organizations where the public models are located. It is set as 1 by default               |
| expression | Query            | False    | String    | Query expression, which supports for sql-like query. The fields that are supported for query include: `modelId` (supports arithmetic operator "in") and `tags` (supports arithmetic operator "="). The supported logical operators are "and", "or", and "not". [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression) |
| projection | Query            | False    | String Array     | Only eligible fields are returned for eligible searches, and all fields are returned by default if it is not configured. For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|
| pagination | Query            | False    | Pagination request struct       | Random pagination. Sorting field cannot be specified. See [Pagination Request Struct](/docs/api/en/latest/overview.html#pagination-request-struct) |



## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    ThingModel struct  |Thing model list. <br>For the definition of thing models. See [ThingModel Struct](/docs/api/en/latest/model/searchmodel.html#thingmodel-struct-thing) |

### ThingModel Struct  <thing>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| modelId        | String                | Model ID which the asset belongs to|
| modelIdPath   | String| Model inheritance path|
| orgId         | String| Organization ID which the asset belongs to|
| name          | StringI18n | Model name|
| desc          | String| Model description|
| tags          | Map (Key is of String type, and the value is of String type) | User-customized tags  |
| attributes    | Map (Key is of String type and the Value is the `ThingAttribute` struct)| Map-typed static attributes definition. The key is the static attribute ID and the value is the attribute definition. See [ThingAttribute Struct](/docs/api/en/latest/model/searchmodel.html#thingattribute-struct-ta)|
| measurement points   | Map (Key is of String type and the Value is the `ThingMeasurepoint` struct)| Map-typed static attributes definition. The key is the measurement point ID and the value is the measurement point definition. See [ThingMeasurepoint Struct](/docs/api/en/latest/model/searchmodel.html#thingmeasurepoint-struct-tm)|
| services      | Map (Key is of String type and the Value is the `ThingService` struct)    | Map-typed services definition. The key is the service ID, and the value is the service definition. See [ThingService Struct](/docs/api/en/latest/model/searchmodel.html#thingservice-struct-ts)|
| events        | Map (Key is of String type and the Value is the `ThingEvent` struct)    | Map-typed events definition. The key is the event ID, and the value is the event definition. See [ThingEvent Struct](/docs/api/en/latest/model/searchmodel.html#thingevent-struct-te)|


### ThingAttribute Struct  <ta>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| identifier | String| Attribute ID|
| dataType   | String| Data type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE|
| isRequired | Boolean| Required or not. If true, the value of this attribute must be set when the asset is instantiated; otherwise the asset will return a validation failure error when it is created.
| name       | StringI18n| Asset name that supports internationalization|
| desc       | String| Model description|
| tags       | Map (Key is of String type, and the value is of String type) | User-customized tags  |
| unit       | Unit struct| Unit. See [Unit Struct](/docs/api/en/latest/model/searchmodel.html#unit-struct-unit)|



### ThingMeasurepoint Struct  <tm>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| identifier | String| ID of the measurement point|
| dataType   | String| Data type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE|
| name       | StringI18n| Asset name that supports internationalization|
| desc       | String| Model description|
| tags       | Map (Key is of String type, and the value is of String type)| User-customized tags|
|hasQuality|Boolean|Whether it has the quality indicator|
|signalType|String|Signal type. E.g.: Generic, AI, PI, DI|
| unit       | Unit struct| Unit. See [Unit Struct](/docs/api/en/latest/model/searchmodel.html#unit-struct-unit)|

### ThingService Struct  <ts>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| identifier | String| Service ID|
| name       | StringI18n| Asset name that supports internationalization|
| desc       | String| Model description|
| tags       | Map (Key is of String type, and the value is of String type)| User-customized tags|
| intputData | ThingDatapoint struct| Input parameters list of the service. See [ThingDatapoint Struct](/docs/api/en/latest/model/searchmodel.html#thingdatapoint-struct-td)  |
| outputData | ThingDatapoint struct| Returned parameters list of the service. See [ThingDatapoint Struct](/docs/api/en/latest/model/searchmodel.html#thingdatapoint-struct-td) |
| callType   | String| Calling type. <!--SYNC or ASYNC-->|


### ThingEvent Struct  <te>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| identifier | String| Event ID|
| name       | StringI18n| Asset name that supports internationalization|
| desc       | String| Model description|
| tags       | Map (Key is of String type, and the value is of String type)| User-customized tags|
| outputData | ThingDatapoint struct| Returned parameters list of the event. See [ThingDatapoint Struct](/docs/api/en/latest/model/searchmodel.html#thingdatapoint-struct-td) |
| eventType   | String| Event type. E.g.: INFO, WARN, ERROR|


### ThingDatapoint Struct  <td>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| identifier | String| Point ID|
| dataType   | String| Data type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE|
| name       | StringI18n| Asset name that supports internationalization|
| desc       | String| Model description|
| tags       | Map (Key is of String type, and the value is of String type)| User-customized tags|
| unit       | Unit struct| Unit. See [Unit Struct](/docs/api/en/latest/model/searchmodel.html#unit-struct-unit)|




### Unit Struct   <unit>

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| unitId | String| Unit identifier|
| multiplier   | String| Multiplier of unit. See [Multiplier](/docs/api/en/latest/model/searchmodel.html#multiplier-mp)|


### Multiplier   <mp>

The multiplier of unit can take the following values:

```
YOTTA ,//Y     10^24
ZETTA ,//Z     10^21
EXA   ,//E     10^18
PETA  ,//P     10^15
TERA  ,//T     10^12
GIGA  ,//G     10^9
MEGA  ,//M     10^6
KILO  ,//k     10^3
HECTO ,//h     10^2
DECA  ,//da    10^1
ONE   ,//      10^0
DECI  ,//d     10^-1
CENTI ,//c     10^-2
MILLI ,//m     10^-3
MICRO ,//μ     10^-6
NANO  ,//n     10^-9
PICO  ,//p     10^-12
FEMTO ,//f     10^-15
ATTO  ,//a     10^-18
ZEPTO ,//z     10^-21
YOCTO ,//y     10^-24
```

## Error Codes

See [Public Return Codes (Connection Service, etc.)](/docs/api/en/latest/overview.html#public-return-codes-connection-service-etc)


## Sample

### Request Sample

```json
POST https://{apigw-address}/model-service/v2.1/thing-models?action=search
 
{
  "expression": "modelId in ( \"planet\", \"FmodelP2\"  )",
  "pagination": {
    "pageNo": 1,
"pageSize": 10
  },
  "orgId": "yourOrgId"
}

```


### Return Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "c6594307-bc30-4380-9869-b8a88b9494de",
    "data": [
            {
                "modelId": "planet",
                "modelIdPath": "/planet",
                "orgId": "yourOrgId",
                "name": {
                    "defaultValue": "planet",
                    "i18nValue": {
                        "en_US": "planet"
                    }
                },
                "desc": "test",
                "tags": {},
                "attributes": {
                    "starsystem": {
                        "identifier": "starsystem",
                        "name": {
                            "defaultValue": "star system",
                            "i18nValue": {
                                "en_US": "star system"
                            }
                        },
                        "desc": "",
                        "tags": {},
                        "dataType": "STRING",
                        "unit": null,
                        "isRequired": false
                    }
                },
                "measurepoints": {
                    "temperature": {
                        "identifier": "temperature",
                        "name": {
                            "defaultValue": "temperature",
                            "i18nValue": {
                                "en_US": "temperature"
                            }
                        },
                        "desc": "temperature",
                        "tags": {},
                        "dataType": "FLOAT",
                        "hasQuality": false,
                        "signalType": "Generic",
                        "unit": {
                            "unitId": "°C",
                            "multiplier": "ONE"
                        }
                    }
                },
                "services": {
                    "speedup": {
                        "identifier": "speedup",
                        "name": {
                            "defaultValue": "speedup",
                            "i18nValue": {
                                "en_US": "speedup"
                            }
                        },
                        "desc": "t",
                        "tags": {},
                        "outputData": [
                            {
                                "identifier": "delta",
                                "name": {
                                    "defaultValue": "delta",
                                    "i18nValue": {
                                        "en_US": "delta"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": null
                            }
                        ],
                        "inputData": [
                            {
                                "identifier": "delta",
                                "name": {
                                    "defaultValue": "delta",
                                    "i18nValue": {
                                        "en_US": "delta"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": {
                                    "unitId": "rpm",
                                    "multiplier": "ONE"
                                }
                            }
                        ],
                        "callType": "ASYNC"
                    }
                },
                "events": {
                    "alert": {
                        "identifier": "alert",
                        "name": {
                            "defaultValue": "alert",
                            "i18nValue": {
                                "en_US": "alert"
                            }
                        },
                        "desc": "e",
                        "tags": {},
                        "outputData": [
                            {
                                "identifier": "event1",
                                "name": {
                                    "defaultValue": "event1",
                                    "i18nValue": {
                                        "en_US": "event1"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": null
                            }
                        ],
 						"eventType": "ERROR"
                    }
                }
            }，
{
                "modelId": "noiseSensor",
                "modelIdPath": "/noiseSensor",
                "orgId": "yourOrgId",
                "name": {
                    "defaultValue": "Noise Sensor",
                    "i18nValue": {
                        "en_US": "Noise Sensor"
                    }
                },
                "desc": "Noise Sensor",
                "tags": {},
                "attributes": {},
                "measurepoints": {},
                "services": {},
                "events": {}
            }
        ],
    "pagination": {
        "pageNo": 1,
        "pageSize": 10，
		"totalSize": 2
    }
}
```

## Java SDK Sample

```java
public class SearchThingModel {
    private static String accessKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String secretKey = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";
    public static void main(String[] args) {
        SearchThingModelRequest request = new SearchThingModelRequest();
        request.setOrgId(orgId);
        request.setExpression("modelId in ( \"planet\" )");
        Projection projection = new Projection();
        projection.add("modelId");
        projection.add("name.defaultValue");
        request.setProjection(projection);
        SearchThingModelResponse response = Poseidon.config(PConfig.init().accessKey(accessKey).secretKey(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```
