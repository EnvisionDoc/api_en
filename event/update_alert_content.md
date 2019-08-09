# Update Alert Content

Update an alert content. The fields required to be verified include `modelId` and `alertTypeId`.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)              |
|isPatchUpdate|Query|true|Boolean|Whether to update in full; false stands for full update, while true stands for partial update |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| alertContent          | true    | generateContent struct    | Alert content. See [generateContent Struct](update_alert_content#generatecontent-struct-generatecontent)|



### generateContent Struct <generatecontent>

| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
|contentId|true|String|Alert content ID|
|contentDesc|true|String|Alert content description|
| modelId          | true    | String    | ID of the model applicable for the alert content. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)  |
| typeId   |  true        | String       | Associated alert type ID           |
|tags|false|tags data type|Tags, only support full update|

## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data | null  | Null  |




## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update&orgId=1c499110e8800000&isPatchUpdate=false
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
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": ""
}
```