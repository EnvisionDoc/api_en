# Delete Alert Rule

Delete all the rules under the organization as per the alert rule IDs.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query| true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)           |
| ruleId      | Query| true| String| ID of the alert rule to be deleted|
| source |false| String |Customized data source that indicates the data source to which the alert rule applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data|null|Null|



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=delete&orgId=1c499110e8800000&ruleId=windTooFast
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
