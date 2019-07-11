# Get Thing Model



Get the model based on the model identifier (`modelId`).

## Request format

```
https://{apigw-address}/model-service/v2.1/thing-models?action=get
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|-------|-------------|-----|------|----------|
| orgId   | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid) |
| scope   | Query            | False    | Integer   | Query scope. 0: Search only from the OU specified by `orgId`, 1: Search from the OU specified by `orgId` and the OU where the public model is located. It is set as 1 by default|
| modelId | Query            | True     | String    | Model ID which the asset belongs to. [How to get modelId information](/docs/api/en/latest/api_faqs.html#how-to-get-modeid-information-modeid)|



## Response parameters

| Name | Data Type | Description |
|-----------|-----------|----------|
|data|Object|Thing Model|



## Error codes

See [Public Return Code (Access Services)](/docs/api/en/latest/overview.html#id8)



## Sample

### Request sample

```
GET https://{apigw-address}/model-service/v2.1/thing-models?action=get&orgId=1c499110e8800000&modelId=planet
```

### Return sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "fa11232e-7e45-4176-a382-963c1240a27f",
    "data": {
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
            }
}
```


## Java SDK invocation sample

```java
public class GetThingModel {
    private static String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";
    public static void main(String[] args) {
        GetThingModelRequest request = new GetThingModelRequest();
        request.setOrgId(orgId);
        request.setModelId("planet");
        request.setScope(1);
        GetThingModelResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```