# Create Alert Severity

Create a new alert severity.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)             |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| severity |  true  |  generateSeverity strucuture  |  Alert severity. See [generateSeverity Struct](create_alert_severity#generateseverity-struct-generateseverity).   |



### generateSeverity Struct <generateseverity>

| Name | Required or Not | Data Type | Description                           |
|--------------|--------------|--------------|-------------------------------------|
| severityId   | true         | String       | Alert severity ID|
| severityDesc | true         | StringI18n   | Internationalized description of alert severity, for which the default fields are mandatory. For the structure, see [Internationalized name struct>>](/docs/api/en/2.0.9/api_faqs.html#internationalized-name-struct)|
| tags         | false        | tags data type | Tags of alert severity |
| source |false| String |Customized data source that indicates the data source to which the alert severity applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|  data   |  String   |  severityId   |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=create&orgId=yourOrgId
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
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea"
}
```
