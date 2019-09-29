# Create Alert Content

Create a new alert content. The fields required to be verified include the model ID (`modelId`) and the alert type ID (`alertTypeId`).

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid).          |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| alertContent          | true    | generateContent struct    | Alert content. See [generateContent Struct](create_alert_content#generatecontent-struct-generatecontent).|

### generateContent Struct <generatecontent>

| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
|contentId|true|String|Alert content ID.|
|contentDesc|true|StringI18n| Internationalized description of alert content, for which the default fields are mandatory. For the structure, see [Internationalized name struct>>](/docs/api/en/2.0.9/api_faqs.html#internationalized-name-struct)|
| modelId          | true    | String    | ID of the model applicable for the alert content. [How to get modelID>>](/docs/api/en/2.0.9/api_faqs#how-to-get-model-id-modelid-modelid) |
| alertTypeId   |  true        | String       | Associated alert type ID           |
|tags|false|tags data type|Tags of alert content. |
| source |false| String |Customized data source that indicates the data source to which the alert content applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data|String |contentId |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=create&orgId=yourOrgId
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
	}
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea"
}
```
