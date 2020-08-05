# Create Alert Content

Create a new alert content. 

## Prerequisite

Ensure the alert type that the alert content would belong to exists. 

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=create
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
   * - alertContent
     - Mandatory
     - GenerateContent Struct
     - The details of the alert content. For more information, see `generateContent Struct>> <create_alert_content#generatecontent-struct-generatecontent>`_



### GenerateContent Struct <generatecontent>

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - contentId
     - Mandatory
     - String
     - The alert content ID.
   * - contentDesc
     - Mandatory
     - StringI18n
     - Specify the alert content's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - modelId
     - Mandatory
     - String
     - The model ID. `How to get modelID>> </docs/api/en/2.1.0/api_faqs#how-to-get-model-id-modelid-modelid>`_
   * - alertTypeId
     - Mandatory
     - String
     - The alert type ID.
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tags>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - The alert content ID.



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-contents?action=create&orgId=yourOrgId 
method: POST 
requestBody: 
{
	"alertContent": {
		"contentId": "planetTemperature",
		"contentDesc": {
			"defaultValue": "Grid is connected from converter",
			"i18nValue": {
				"en_US": "Grid is connected from converter",
				"zh_CN": "风机已并网"
			}
		},
		"modelId": "WindDev-E0",
		"alertTypeId": "9001",
		"tags": {
			"year": "2000",
			"author": "cshan"
		}
	},
  "action": "create"
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "94e0e6e5-10dd-4fcb-a013-331d5869975a",
	"data": "planetTemperature"
}
```

### Java SDK Sample

```java
public void testCreateAlertContent() {
    private static String accessKey = "yourAppAccessKey";
    private static String secretKey = "yourAppSecretKey";
    private static String orgId = "yourOrgId";
    private static String url = "https://{apigw-address}";
    CreateAlertContentRequest request = new CreateAlertContentRequest();
    request.setOrgId(orgId);
    GenerateContent alertContent = new GenerateContent();
    alertContent.setContentId("yourContentId");
    alertContent.setAlertTypeId("yourAlertTypeId");
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文");
    map.put("en_US", "english");
    desc.setI18nValue(map);
    alertContent.setContentDesc(desc);
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    alertContent.setTags(tags);
    alertContent.setModelId("yourModelId");
    request.setAlertContent(alertContent);
    try {
        CreateAlertContentResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, CreateAlertContentResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
