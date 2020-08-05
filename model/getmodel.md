# Get Thing Model

Get the thing model via the ``modelId``.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Model Management
     - Read

## Request Format

```json
GET https://{apigw-address}/model-service/v2.1/thing-models?action=get
```

## Request Parameters (URI)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - scope
     - Query
     - Optional
     - Integer
     - 
         + 0 = Only search from the organization specified by the ``orgId``.
         + 1 (default) = Search from the organization specified by the ``orgId`` as well as the organizations with public models.
   * - modelId
     - Query
     - Mandatory
     - String
     - The model ID which the asset belongs to. `How to get modelID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-model-id-modelid-modelid>`_


## Response Parameters

.. list-table:: 
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - ThingModel Struct
     - The thing model. For more information on ThingModel struct, see `ThingModel Struct>> </docs/api/en/2.1.0/model/searchmodel.html#thingmodel-struct-thing>`_


## Error Codes

See [Public Response Codes (Connection Service, etc.)](../overview#public-response-codes-connection-service-etc)


## Samples

### Request Sample

```json
url: https://{apigw-address}/model-service/v2.1/thing-models?action=get&orgId=yourOrgId&modelId=yourModelId
method: GET
```

### Response Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "fa11232e-7e45-4176-a382-963c1240a27f",
    "data": {
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
            }
}
```


## Java SDK Sample

```java
public class GetThingModel {
    private static String accessKey = "AccessKey of your APP";
    private static String secretKey = "SecretKey of your APP";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    public static void main(String[] args) {
        GetThingModelRequest request = new GetThingModelRequest();
        request.setOrgId(orgId);
        request.setModelId("planet");
        request.setScope(1);
        GetThingModelResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```
