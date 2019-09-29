# Update Alert Type

Update an alert type. The field required to be verified include `typeId`.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-types?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid) |
|isPatchUpdate|Query|true|Boolean|Whether to perform partial update. <br>When it is true, only the fields specified in the parameter are updated; <br>when it is false, all the fields will be updated, i.e. the fields without specified value will be left blank. Set as true by default.|


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| type |   true  |  generateType struct   |  Alert type. See [generateType Struct](update_alert_type#generatetype-struct-generatetype). |



### generateType Struct <generatetype>

| Name | Required or Not | Data Type | Description                        |
|----------|--------------|--------------|-------------------------------------|
| typeId   |  true        | String       | Alert type ID|
| typeDesc | true         | StringI18n   | Internationalized description of alert type, for which the default fields are mandatory. For the struct, see [Internationalized name struct>>](/docs/api/en/2.0.9/api_faqs.html#internationalized-name-struct)|
| tags     | false        | tags data type  | Tags |
| source |false| String |Customized data source that indicates the data source to which the alert type applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|


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
