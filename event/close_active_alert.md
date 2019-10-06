# Close Active Alert

Close an active alert. A closed active alert will become a history alert.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=close
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)           |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| eventId  | true | String  | Alert ID |
| recoverTime      | true         | Long         | Recovery time in UTC format. For time formats, see [ISO8601 Standard Time Formats Used by UTC>>](/docs/api/zh_CN/latest/api_faqs.html#utciso8601)|
| localRecoverTime | false        | String       | Recovery time in local format. For time formats, see [Data and Time Formats Used by Localtime>>](/docs/api/zh_CN/latest/api_faqs.html#localtime)|
| recoverReason    | false        | String       | Recovery reason|




## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | null | Null |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=close&orgId=yourOrgId&eventId=2019060135b6df70b2de6aa2f2eb1d09e9aa1ae7&recoverTime=1559304900404
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea"
}
```
