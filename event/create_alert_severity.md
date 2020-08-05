# Create Alert Severity

Create a new alert severity.


## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=create
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
   * - severity
     - Mandatory
     - GenerateSeverity Struct
     - The details of the alert severity. For more information, see `GenerateSeverity Struct>> <create_alert_severity#generateseverity-struct-generateseverity>`_



### GenerateSeverity Struct <generateseverity>


.. list-table:: 
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - severityId
     - Mandatory
     - String
     - The alert severity ID.
   * - severityDesc
     - Mandatory
     - StringI18n
     - Specify the alert severity's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`_
   * - tags
     - Optional
     - Map
     - The user-defined tags. (The Key and Value are of String type.) For details, see `How to use tags>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_



## Response Parameters

.. list-table:: 
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - String
     - The alert severity ID.


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-severities?action=create&orgId=yourOrgId
method: POST 
requestBody: 
{
	"severity": {
		"severityId": "planetTemperature",
		"severityDesc": {
			"defaultValue": "Error",
			"i18nValue": {
				"en_US": "Error",
				"zh_CN": "错误"
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
	"requestId": "94e0e6e5-10dd-4fcb-a013-331d5869975a",
	"data": "planetTemperature"
}
```

### Java SDK Sample

```java
public void testCreateAlertSeverity() {
        CreateAlertSeverityRequest request = new CreateAlertSeverityRequest();
        GenerateSeverity generateSeverity = new GenerateSeverity();
        StringI18n desc = new StringI18n();
        desc.setDefaultValue("default");
        Map<String, String> map = new HashMap<>();
        map.put("zh_CN", "中文");
        map.put("en_US", "english");
        desc.setI18nValue(map);
        generateSeverity.setSeverityDesc(desc);
        generateSeverity.setSeverityId("yourSeverityId");
        Map<String, String> tags = new HashMap<>();
        tags.put("yourTagKey", "yourTagValue");
        generateSeverity.setTags(tags);
        request.setSeverity(generateSeverity);
        request.setOrgId(orgId);
        try {
            CreateAlertSeverityResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                    .url(url)
                    .getResponse(request, CreateAlertSeverityResponse.class);
            Gson gson = new Gson();
            System.out.println(gson.toJson(response));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```