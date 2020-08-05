# Search Thing Model

Search thing models via the ``orgId``.

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
POST https://{apigw-address}/model-service/v2.1/thing-models?action=search
```

## Request Parameters (URI)

.. list-table::
   :widths: 15 15 15 15 40
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
     - The organization ID which the asset belongs to. `How to get orgId </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - scope
     - Query
     - Optional
     - Integer
     -
         + 0: Only search from the organization specified by the ``orgId``.
         + 1: (default) = Search from the organization specified by the ``orgId`` as well as the organizations with public models.


## Request Parameters (Body)


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - expression
     - Optional
     - String
     - The query expression, which supports sql-like query.

       The fields that are supported for query include: ``modelId`` (supports arithmetic operator "in") and ``tags`` (supports arithmetic operator "=", "exists", and "not exists"). The supported logical operators are "and" and "or".

       `How to use expression>> </docs/api/en/2.1.0/api_faqs#how-to-use-expression>`_
   * - projection
     - Optional
     - Projection Struct
     - Enables you to crop the data result set returned in the request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see `How does projection crop the result set </docs/api/en/2.1.0/api_faqs#how-does-projection-crop-the-result-set>`_
   * - pagination
     - Optional
     - Pagination Request Struct
     - Lists the paging requirements in a request. ``sorters`` is not supported to sort the response. For more details, see `Pagination Request Struct </docs/api/en/2.1.0/overview.html#pagination-request-struct>`_


     

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of ThingModel Structs
     - A list of the thing models returned. For details of a Thingmodel Struct, see `ThingModel Struct </docs/api/en/2.1.0/model/searchmodel#thingmodel-struct-thing>`_ .


### ThingModel Struct <thing>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - modelId
     - String
     - The model ID which the asset belongs to.
   * - modelIdPath
     - String
     - The model ID path.
   * - orgId
     - String
     - The organization ID which the asset belongs to.
   * - name
     - StringI18n
     - The model name.
   * - desc
     - String
     - The model description.
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - attributes
     - Map
     - The key is the static attribute ID, of String type, and the value is of the ``ThingAttribute`` Struct. For more information, see `ThingAttribute Struct </docs/api/en/2.1.0/model/searchmodel.html#thingattribute-struct-ta>`_
   * - measurepoints
     - Map
     - The key is the measurement point ID, of String type, and the value is of the ``ThingMeasurepoint`` Struct. For more information, see `ThingMeasurepoint Struct </docs/api/en/2.1.0/model/searchmodel.html#thingmeasurepoint-struct-tm>`_
   * - services
     - Map
     - The key is the service ID, of String type, and the value is of the ``ThingService`` Struct. For more information, see `ThingService Struct </docs/api/en/2.1.0/model/searchmodel.html#thingservice-struct-ts>`_
   * - events
     - Map
     - The key is the event ID, of String type, and the value is of the ``ThingEvent`` Struct. For more information, see `ThingEvent Struct </docs/api/en/2.1.0/model/searchmodel.html#thingevent-struct-te>`_


### ThingAttribute Struct  <ta>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - identifier
     - String
     - The attribute ID.
   * - dataType
     - String
     - The data type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE
   * - dataDefinition
     - String
     - The data definition of the ``dataType`` in this structure, which is a JSON string. For example, when the ``dataType`` is "STRING", it defines the string length; when the ``dataType`` is "ENUM", it defines the value and description. `How to use dataDefinition>> <../api_faqs#how-to-use-datadefinition-datadef>`__
   * - isRequired
     - Boolean
     - If true, the value of this attribute must be set when the asset is instantiated; otherwise the asset will return a validation failure error when it is created.
   * - defaultValue
     - As defined in the thing model
     - The default value of the attribute. If the attribute has no default value, ``defaultValue`` would be ``null`` . 
   * - name
     - StringI18n
     - The attribute name.
   * - desc
     - String
     - The attribute description.
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - isStdElement
     - Boolean
     -
       + true = this is an industry standard element
       + false = this is not an industry standard element
   * - stdElementId
     - String
     - The URN of the element if ``isStdElement`` is ``true`` . The format is urn\:enos\:modelelement\:std\: ``<id>`` : ``<version>`` . ``id`` is the element ID. ``<version>`` is the version of the element.

       If ``isStdElement`` is ``false`` , then ``stdElementId`` is ``null``.
   * - unit
     - Unit Struct
     - For more information, see `Unit Struct </docs/api/en/2.1.0/model/searchmodel.html#unit-struct-unit>`__ .


### ThingMeasurepoint Struct  <tm>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - identifier
     - String
     - The ID of the measurement point.
   * - dataType
     - String
     - Data type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE
   * - dataDefinition
     - String
     - The data definition of the ``dataType`` in this structure, which is a JSON string. For example, when the ``dataType`` is "STRING", it defines the string length; when the ``dataType`` is "ENUM", it defines the value and description. `How to use dataDefinition>> <../api_faqs#how-to-use-datadefinition-datadef>`_
   * - name
     - StringI18n
     - The measurement point name.
   * - desc
     - String
     - The measurement point description.
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - isStdElement
     - Boolean
     -
       + true = this is an industry standard element
       + false = this is not an industry standard element
   * - stdElementId
     - String
     - The URN of the element if ``isStdElement`` is ``true`` . The format is urn\:enos\:modelelement\:std\: ``<id>`` : ``<version>`` . ``id`` is the element ID. ``<version>`` is the version of the element.

       If ``isStdElement`` is ``false`` , then ``stdElementId`` is ``null``.
   * - hasQuality
     - Boolean
     -
       + true = has the quality indicator
       + false = does not have the quality indicator
   * - signalType
     - String
     - The signal/point type. E.g.: Generic, AI, PI, DI
   * - unit
     - Unit Struct
     - For more information, see `Unit Struct </docs/api/en/2.1.0/model/searchmodel.html#unit-struct-unit>`_ .


### ThingService Struct  <ts>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - identifier
     - String
     - The service ID.
   * - name
     - StringI18n
     - The service name.
   * - desc
     - String
     - The service description.
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - isStdElement
     - Boolean
     -
       + true = this is an industry standard element
       + false = this is not an industry standard element
   * - stdElementId
     - String
     - The URN of the element if ``isStdElement`` is ``true`` . The format is urn\:enos\:modelelement\:std\: ``<id>`` : ``<version>`` . ``id`` is the element ID. ``<version>`` is the version of the element.

       If ``isStdElement`` is ``false`` , then ``stdElementId`` is ``null``.
   * - intputData
     - ThingDatapoint Struct
     - The service's input parameters list. For more information, see `ThingDatapoint Struct </docs/api/en/2.1.0/model/searchmodel.html#thingdatapoint-struct-td>`__ .
   * - outputData
     - ThingDatapoint Struct
     - The service's returned parameters list. For more information, see `ThingDatapoint Struct </docs/api/en/2.1.0/model/searchmodel.html#thingdatapoint-struct-td>`__ .
   * - callType
     - String
     - The calling type. This parameter will be deprecated.

       + "ASYNC" = asynchronous
       + "SYNC"` = synchronous


### ThingEvent Struct  <te>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - identifier
     - String
     - The event ID.
   * - name
     - StringI18n
     - The event name.
   * - desc
     - String
     - The event description.
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - isStdElement
     - Boolean
     -
       + true = this is an industry standard element
       + false = this is not an industry standard element
   * - stdElementId
     - String
     - The URN of the element if ``isStdElement`` is ``true`` . The format is urn\:enos\:modelelement\:std\: ``<id>`` : ``<version>`` . ``id`` is the element ID. ``<version>`` is the version of the element.

       If ``isStdElement`` is ``false`` , then ``stdElementId`` is ``null``.
   * - outputData
     - ThingDatapoint Struct
     - The event's returned parameters list. For more information, see `ThingDatapoint Struct </docs/api/en/2.1.0/model/searchmodel.html#thingdatapoint-struct-td>`__
   * - eventType
     - String
     - Event type. E.g.: INFO, WARN, ERROR


### ThingDatapoint Struct  <td>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - identifier
     - String
     - The data point ID.
   * - dataType
     - String
     - Data type. E.g.: ARRAY, BOOL, DATE, ENUM, INT, FLOAT, DOUBLE, STRUCT, STRING, TIMESTAMP, FILE
   * - dataDefinition
     - String
     - The data definition of the ``dataType`` in this structure, which is a JSON string. For example, when the ``dataType`` is "STRING", it defines the string length; when the ``dataType`` is "ENUM", it defines the value and description. `How to use dataDefinition>> <../api_faqs#how-to-use-datadefinition-datadef>`__
   * - name
     - StringI18n
     - The data point name.
   * - desc
     - String
     - The data point description.
   * - tags
     - Map
     - User-defined tags. (The Key and Value are of String type.)
   * - isStdElement
     - Boolean
     -
       + true = this is an industry standard element
       + false = this is not an industry standard element
   * - stdElementId
     - String
     - The URN of the element if ``isStdElement`` is ``true`` . The format is urn\:enos\:modelelement\:std\: ``<id>`` : ``<version>`` . ``id`` is the element ID. ``<version>`` is the version of the element.

       If ``isStdElement`` is ``false`` , then ``stdElementId`` is ``null``.
   * - unit
     - Unit Struct
     - For more information, see `Unit Struct </docs/api/en/2.1.0/model/searchmodel.html#unit-struct-unit>`__


### Unit Struct <unit>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - unitId
     - String
     - The unit ID.
   * - multiplier
     - String
     - The multiplier of the unit. For more information, see `Multiplier </docs/api/en/2.1.0/model/searchmodel.html#multiplier-mp>`_


### Multiplier   <mp>

The multiplier of the unit can take the following values:

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

See [Public Response Codes (Connection Service, etc.)](../overview#public-response-codes-connection-service-etc)


## Samples

### Request Sample

```json
url: https://{apigw-address}/model-service/v2.1/thing-models?action=search&orgId=yourOrgId&scope=1
method: POST
requestBody:
{
  "expression": "modelId in ( \"planet\", \"noiseSensor\"  )",
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
	"code":0,
	"msg":"OK",
	"requestId":"c6594307-bc30-4380-9869-b8a88b9494de",
	"data":[
		{
			"modelId":"planet",
			"modelIdPath":"/planet",
			"orgId":"yourOrgId",
			"name":{
				"defaultValue":"planet",
				"i18nValue":{
					"en_US":"planet"
				}
			},
			"desc":"test",
			"tags":{

			},
			"attributes":{
				"starsystem":{
					"identifier":"starsystem",
					"name":{
						"defaultValue":"star system",
						"i18nValue":{
							"en_US":"star system"
						}
					},
					"desc":"",
					"tags":{

					},
					"stdElementId":"urn:user:modelelement:std:atom-property-int:1.0",
					"isStdElement":true,
					"dataType":"STRING",
					"unit":null,
					"isRequired":false,
          "defaultValue":null
				}
			},
			"measurepoints":{
				"temperature":{
					"identifier":"temperature",
					"name":{
						"defaultValue":"temperature",
						"i18nValue":{
							"en_US":"temperature"
						}
					},
					"desc":"temperature",
					"tags":{

					},
					"stdElementId":"urn:user:modelelement:std:atom-property-int:1.0",
					"isStdElement":true,
					"dataType":"FLOAT",
					"hasQuality":false,
					"signalType":"Generic",
					"unit":{
						"unitId":"°C",
						"multiplier":"ONE"
					}
				}
			},
			"services":{
				"speedup":{
					"identifier":"speedup",
					"name":{
						"defaultValue":"speedup",
						"i18nValue":{
							"en_US":"speedup"
						}
					},
					"desc":"t",
					"tags":{

					},
					"outputData":[
						{
							"identifier":"delta",
							"name":{
								"defaultValue":"delta",
								"i18nValue":{
									"en_US":"delta"
								}
							},
							"desc":"",
							"tags":{

							},
							"dataType":"INT",
							"unit":null
						}
					],
					"inputData":[
						{
							"identifier":"delta",
							"name":{
								"defaultValue":"delta",
								"i18nValue":{
									"en_US":"delta"
								}
							},
							"desc":"",
							"tags":{

							},
							"dataType":"INT",
							"unit":{
								"unitId":"rpm",
								"multiplier":"ONE"
							}
						}
					],
					"callType":"ASYNC"
				}
			},
			"events":{
				"alert":{
					"identifier":"alert",
					"name":{
						"defaultValue":"alert",
						"i18nValue":{
							"en_US":"alert"
						}
					},
					"desc":"e",
					"tags":{

					},
					"outputData":[
						{
							"identifier":"event1",
							"name":{
								"defaultValue":"event1",
								"i18nValue":{
									"en_US":"event1"
								}
							},
							"desc":"",
							"tags":{

							},
							"dataType":"INT",
							"unit":null
						}
					],
					"eventType":"ERROR"
				}
			}
		},
		{
			"modelId":"noiseSensor",
			"modelIdPath":"/noiseSensor",
			"orgId":"yourOrgId",
			"name":{
				"defaultValue":"Noise Sensor",
				"i18nValue":{
					"en_US":"Noise Sensor"
				}
			},
			"desc":"Noise Sensor",
			"tags":{

			},
			"attributes":{

			},
			"measurepoints":{

			},
			"services":{

			},
			"events":{

			}
		}
	],
	"pagination":{
		"pageNo":1,
		"pageSize":10,
		"totalSize":2
	}
}
```

## Java SDK Sample

```java
public class SearchThingModel {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    public static void main(String[] args) {
        SearchThingModelRequest request = new SearchThingModelRequest();
        request.setOrgId(orgId);
        request.setExpression("modelId in ( \"planet\" )");
        Projection projection = new Projection();
        projection.add("modelId");
        projection.add("name.defaultValue");
        request.setProjection(projection);
        SearchThingModelResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```
