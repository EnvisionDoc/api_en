# Delete Alert Content

An alert content will be deleted. It is required to verify whether the alert content to be deleted is used by any other rules; if yes, no deletion is allowed.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-contents?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)            |
|alertContentId | Query      | true | String | Alert content ID|




## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data  | null | Null |




## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=delete&orgId=1c499110e8800000&alertContentId=planetTemperature
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
