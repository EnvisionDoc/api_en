# Delete Active Alert

Delete a specified active alert; if the alert does not exist, a failure will be returned with specific information.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)    |
|  eventId  | Query  | true  |  String  |  Alert ID |



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data |  null |  Null  |




## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=delete&orgId=1c499110e8800000&eventId=2019060135b6df70b2de6aa2f2eb1d09e9aa1ae7
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
