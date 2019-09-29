# Delete Alert Severity

Delete an alert severity. It is required to verify whether the alert severity to be deleted is used by any other rules; if yes, no deletion is allowed.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)             |
|severityId      | Query  |  true  |   String  |  Alert severity ID|
| source |false| String |Customized data source that indicates the data source to which the alert severity applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data   |   null  | Null   |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=delete&orgId=1c499110e8800000&severityId=planetTemperature
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
