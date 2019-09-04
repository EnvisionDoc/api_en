# Update Alert Severity

Update an alert severity, for which `severityId` is required to be verified.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid) |
|isPatchUpdate|Query|true|Boolean|Whether to perform partial update. <br>When it is true, only the fields specified in the parameter are updated; <br>when it is false, all the fields will be updated, i.e. the fields without specified value will be left blank. Set as true by default. |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| severity |  true  |  generateSeverity struct  |  Alert severity. See [generateSeverity Struct](update_alert_severity#generateseverity-struct-generateseverity) |


### generateSeverity Struct <generateseverity>

| Name | Required or Not | Data Type | Description                         |
|--------------|--------------|--------------|-------------------------------------|
| severityId   | true         | String       | Alert severity ID                        |
| severityDesc | true         | StringI18n   | Internationalized description of alert severity, for which the default fields are mandatory. For the structure, see [Internationalized name struct>>](/docs/api/en/latest/api_faqs.html#internationalized-name-struct) |
| tags         | false        | tags data type | Tags |
| source |false| String |Customized data source that indicates the data source to which the alert severity applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data   |   null  | Null   |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=update&orgId=1c499110e8800000&isPatchUpdate=false
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
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data": ""
}
```
