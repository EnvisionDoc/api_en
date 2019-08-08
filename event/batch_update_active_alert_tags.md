# Batch Update Active Alert Tags

<!--Tested, 99500-->

Batch update the tag data for the specified alerts in current alert library. The returned structure will indicate the update results of each alert. In case that an error occurs with any alert, the error information will be recored and the remaining update process will continue.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=batchUpdateTags
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                 |
|isPatchUpdate|Query|true|Boolean|Whether to update in full; false stands for full update, while true stands for partial update |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| eventIds          | true    | String type list    | Alert ID list |
| tags        | true     | Tags structure    | Tags to be modified |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data|null|Null|





## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=batchUpdateTags&orgId=1c499110e8800000
{
	"eventIds": ["20190531b83331a8549e1e956f2413552eda1ec9",
	"20190615f7b3864b98d80b25e8e9a0affd6ce064"],
	"isPatchUpdate": false,
	"tags": {
		"Tag999": "999"
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
