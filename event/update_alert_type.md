# Update Alert Type

Update an alert type. If the alert type already has a parent alert type, the `parentTypeId` cannot be updated.

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/alert-types?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid) |
|isPatchUpdate|Query|Mandatory|Boolean|<ul><li>true = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.</li><li>false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.</li></ul>|


## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| type |   Mandatory  |  GenerateType Struct   |  The details of the alert type. For more information, see [GenerateType Struct](update_alert_type#generatetype-struct-generatetype). |



### GenerateType Struct <generatetype>

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
     - Specify the alert type's description in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct>> </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - tags
     - Optional
     - Map
     - User-defined tags. (The Key and Value are of String type.) For details, see `How to use tags>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`__
   * - parentTypeId
     - Optional 
     - String
     - The alert type ID of the parent alert.


## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/alert-types?action=update&orgId=yourOrgId&isPatchUpdate=false
method: POST 
requestBody: 
{
  "action": "update",
	"type":{
		"typeId":"planetTemperature",
		"typeDesc":{
			"defaultValue":"OverLimit",
			"parentTypeId":"parent",
			"i18nValue":{
				"en_US":"OverLimit",
				"zh_CN":"超限"
			}
		},
		"tags":{
			"year":"2000",
			"author":"cshan"
		},
    "parentTypeId": "chenchen_test_documentation"
	}
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": null
}
```

### Java SDK Sample

```java
public void testUpdateAlertType() {
    UpdateAlertTypeRequest request = new UpdateAlertTypeRequest();
    request.setOrgId(orgId);
    GenerateType generateType = new GenerateType();
    generateType.setParentTypeId("yourParentTypeId"); //If the alert has a parent alert type, the parent alert type cannot be changed.
    generateType.setTypeId("yourTypeId");
    StringI18n desc = new StringI18n();
    desc.setDefaultValue("default");
    Map < String, String > map = new HashMap < > ();
    map.put("zh_CN", "中文");
    map.put("en_US", "english");
    desc.setI18nValue(map);
    generateType.setTypeDesc(desc);
    Map < String, String > tags = new HashMap < > ();
    tags.put("yourTagKey", "yourTagValue");
    generateType.setTags(tags);
    request.setType(generateType);
    request.setIsPatchUpdate(true);
    try {
        UpdateAlertTypeResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
            .url(url)
            .getResponse(request, UpdateAlertTypeResponse.class);
        Gson gson = new Gson();
        System.out.println(gson.toJson(response));
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
