# Search Thing Model

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Search thing models by organizationid.

## Request format

```
https://{apigw-address}/model-service/v2.1/thing-models?action=search
```

## Request parameters (Body)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|:-----------|:-----------------|:---------|:----------|:-----------------------------------------------------------------------------------------|
| orgId   | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)|
| scope   | Query            | False    | Integer   | Query scope.  0- Only search from the specified orgId; 1 - Search from the specified orgId and public orgId. It is set as 1 by default               |
| expression | Query            | False    | String    | expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| projection | Query            | False    | String Array     | Only eligible fields are returned for eligible searches, and all fields are returned by default if no search criterion is set. For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|
| pagination | Query            | False    | Pagination request structure       | Random pagination. The default is to sort in descending order by occurTime, and the user can not specify the sorting field. The default pagination size is 10 pages. See [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |



## Response parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    ThingModel structure  |Thing model list. <br>For the definition of thing models, see [ThingModel Structure](/docs/api/en/latest/model/searchmodel.html#id4) |

### ThingModel structure

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| modelId        | String                | Model ID which the asset belongs to|
| modelIdPath   | String| Model inheritance path|
| orgId         | String| Organization ID which the asset belongs to|
| name          | StringI18n | Model name|
| desc          | String| Model description|
| tags          | Map (Key is of String type, and the value is of String type) | User-customized tags  |
| attributes    | Map (Key is of String type and the Value is the `ThingAttribute` structure)| Map-typed value defined by the static attributes. The key is the static attribute id and the value is the attribute definition|
| measurepoints   | Map (Key is of String type and the Value is the `ThingMeasurepoint` structure)| Map-typed value defined by the static attributes. The key is the measurepoint id and the value is the measurepoint definition|
| services      | Map (Key is of String type and the Value is the `ThingService` structure)    | Map-typed value defined by the service. The key is the service id, and the value is the service definition.|
| events        | Map (Key is of String type and the Value is the `ThingEvent` structure)    | Map-typed value defined by the event. The key is the event id, and the value is the event definition.|


### ThingAttribute structure

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| identifier | String| Attribute id|
| dataType   | String| Data Type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE|
| isRequired | Boolean| Required or not. If true, the value of this attribute when the asset is instantiated; otherwise the asset will return a validation failure error when it is created.
| name       | StringI18n| Internationalized asset names are supported|
| desc       | String| Model description|
| tags       | Map (Key is of String type, and the value is of String type) | User-customized tags  |
| unit       | Unit structure| Unit. See [Unit Structure](/docs/api/en/latest/model/searchmodel.html#id6)|


### Unit structure

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| unitId | String| Unit identifier|
| multiplier   | String| Multiplier of unit. See [Multiplier](/docs/api/en/latest/model/searchmodel.html#id7)|


### Multiplier

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

## Error codes

See [Public Return Code (Access Services)](/docs/api/en/latest/overview.html#id8)


## Sample

### Request sample

```json
POST https://{apigw-address}/model-service/v2.1/thing-models?action=search
 
{
  "expression": "modelId in ( \"planet\", \"FmodelP2\"  )",
  "pagination": {
    "pageNo": 1,
"pageSize": 10
  },
  "orgId": "1ad3889266800000"
}

```


### Return sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "c6594307-bc30-4380-9869-b8a88b9494de",
    "data": [
            {
                "modelId": "planet",
                "modelIdPath": "/planet",
                "orgId": "1c499110e8800000",
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
                "orgId": "sysenos2018",
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

## Java SDK invocation sample

```java
public class SearchThingModel {
    private static String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
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
        SearchThingModelResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```
