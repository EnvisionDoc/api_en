# Create Active Alert

An active alert will be created. Except for the mandatory verification, there is no need to verify the legality of other parameters. The parameters used by users such as `contentId` will not be maintained on the EnOS platform.

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)           |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| activeAlert  | true | ActiveAlert structure  | Active alert. See [ActiveAlert Structure](create_active_alert#activealert-structure-activelert) |


### ActiveAlert Structure <activealert>

| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| assetId        | true     | String    | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)    |
| modelId          | true    | String    | ID of the model applicable for the alert. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)  |
| modelIdPath    | false        | String       | Model path|
| measurepointId | true         | String       | Asset measurement point. [How to get pointId](/docs/api/en/latest/api_faqs#how-to-get-the-measuremet-point-pointid-pointid) |
| value          | true         | Object       | Measurement point value|
| occurTime      | true         | Long         | Occurrence time in UTC format. For time formats, see [ISO8601 Standard Time Formats Used by UTC](/docs/api/zh_CN/latest/api_faqs.html#utciso8601)              |
| localOccurTime | false        | String       | Occurrence time in local format. For time formats, see [Data and Time Formats Used by Localtime](/docs/api/zh_CN/latest/api_faqs.html#localtime)|
| severityId     | false        | String       | Alert severity ID                 |
| severityDesc   | false        | StringI18n   | Alert severity description                 |
| typeId         | false        | String       | Alert type ID                 |
| typeDesc       | false        | StringI18n   | Alert type description                 |
| subTypeId      | false        | String       | Alert sub-type ID               |
| subTypeDesc    | false        | StringI18n   | Alert sub-type description               |
| contentId      | false        | String       | Alert content ID                 |
| contentDesc    | false        | StringI18n   | Alert content description                 |
| tags           | false        | tags data type | Tags|




## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | null | Null |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=create&orgId=1c499110e8800000
{
  "activeAlert": {
	 "assetId": "qu5TmJRj",
	 "modelId": "Inverter_Model",
	 "modelIdPath": "/Inverter_Model",
	 "measurepointId": "power",
	 "value": "3.5559796405967736",
	 "occurTime": 1559304899404,
	 "localOccurTime": "2019-06-01 02:14:59",
	 "severityId": "alert_001",
	 "severityDesc": {
        "defaultValue": "Warn",
		 "i18nValue": {
			 "en_US": "alert",
			 "zh_CN": "alert"
		 }
	 },
	 "typeId": "errorType",
	 "typeDesc": {
        "defaultValue": "Warn",
		 "i18nValue": {
			 "en_US": "login failed",
			 "zh_CN": "登录失败"
		 }
	 },
	 "contentId": "planetTemperature",
	 "contentDesc": {
        "defaultValue": "the temperature is too high",
		 "i18nValue": {
			 "en_US": "the temperature is too high",
			 "zh_CN": "温度过高"
		 }
	 },
	 "tags": {
		 "Tag666": "63253w532",
		 "Tag888": "63253w532888",
		 "Tag": "1111"
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
