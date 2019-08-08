# Update Alert Type

An alert type will be updated. The field required to be verified include `typeId`.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-types?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid) |
|isPatchUpdate|Query|true|Boolean|Whether to update in full; false stands for full update, while true stands for partial update.


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| type |   true  |  generateType structure   |  Alert type. See [generateType Structure](update_alert_type#generatetype-structure-generatetype) |



### generateType Structure <generatetype>

| Name | Required or Not | Data Type | Description                        |
|----------|--------------|--------------|-------------------------------------|
| typeId   |  true        | String       | Alert type ID|
| typeDesc | true         | StringI18n   | Internationalized description of alert type, for which the default fields are mandatory. For the structure, see [Internationalized name structure](/docs/api/en/latest/api_faqs.html#internationalized-name-structure)|
| tags     | false        | tags data type  | Tags                                |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data |  null |  Null |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-types?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"generateType": {
		"typeId": "planetTemperature",
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
	"data": ""
}
```
