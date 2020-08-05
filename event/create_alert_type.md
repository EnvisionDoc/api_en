# Create Alert Type

Create a new alert type.


## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-types?action=create
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


## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - type
     - Mandatory
     - GenerateType Struct
     - The details of the alert type. For more information, see `GenerateType Struct>> <create_alert_type#generatetype-struct-generatetype>`_



### GenerateType Struct  <generatetype>


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - typeId
     - Mandatory
     - String
     - The alert type ID.
   * - typeDesc
     - Mandatory
     - StringI18n
     - Specify the alert type's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_ 
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tags>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_
   * - parentTypeId
     - Optional
     - String
     - The alert type ID of the parent alert.





## Response Parameters


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - The alert type ID.



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-types?action=create&orgId=yourOrgId
method: POST 
requestBody: 
{
	"type": {
		"typeId": "planetTemperature",
    "parentTypeId" : "parent",
		"typeDesc": {
			"defaultValue": "OverLimit",
			"i18nValue": {
				"en_US": "OverLimit",
				"zh_CN": "超限"
			}
		},
		"tags": {
			"year": "2000",
			"author": "cshan"
		}
	}
}
```

### Return Sample

```json
{
  "code": 0,
  "msg": "OK",
  "requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
  "data": "planetTemperature"
}
```

### Java SDK Sample

```java
public void testCreateAlertType() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    CreateAlertTypeRequest request = new CreateAlertTypeRequest();
    request.setOrgId(orgId);
    GenerateType type = new GenerateType();
    type.setTypeId("yourAlertTypeId");
    type.setParentTypeId("yourParentTypeId");
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文");
    map.put("en_US", "english");
    desc.setI18nValue(map);
    type.setTypeDesc(desc);
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    type.setTags(tags);
    request.setType(type);
    try {
        CreateAlertTypeResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, CreateAlertTypeResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
