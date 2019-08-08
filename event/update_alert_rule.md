# Update Alert Rule

An alert rule will be updated. Any parameter (if not being null) included request body  can be updated. The fields required to be verified include: model ID (`modelId`), measurepoint (`measurepointId`), alert severity (`severityId`), alert content (`contentId`) and query scope (`scope`).

## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)               |
|isPatchUpdate|Query|true|Boolean|Whether to update in full; false stands for full update, while true stands for partial update |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
|alertRule|true|alertRule structure|Alert rule. See [alertRule Structure](update_alert_rule#alertrule-structure-alertrule)|


### alertRule Structure <alertrule>

|Name| Required or Not (Specially in case that isPatchUpdate=false) | Data type | Description |
|------|-----------------|-----------|-------------|
| ruleId         | true| String| Alert rule ID, which is specified by the user as the unique identifier to locate the alert rule to be updated. |
| ruleDesc       | true| StringI18n| Internationalized alert description, for which only supports full update. For the structure, see [Internationalized name structure](http://www.envisioniot.com/docs/api/en/latest/api_faqs.html#internationalized-name-structure)|
| modelId| true| String| Model applicable for the alert rule. [How to get modelId](/docs/api/en/latest/api_faqs#how-to-get-model-id-modelid-modelid)|
| measurepointId | true| String                | Asset measurement point. [How to get pointId](/docs/api/en/latest/api_faqs.html#how-to-get-the-measuremet-point-pointid-pointid)|
| condition      | true| String| Expression. A slash "/" is used to express the hierarchical relationship, for which only one downward layer is supported now. [How to use expression](/docs/api/en/latest/api_faqs.html#how-to-use-expression) |
| severityId     | true| String| Alert severity ID|
| contentId      | true| String| Alert content ID|
| tags           | false| tags structure| Rule tags, for which only full update is supported|
| scope          | true         | AssetNode structure | Specify a node on the asset tree to indicate the scope. If the `treeId` is set as "all", it indicates that this is a special node, standing for the globality of the organization. See [AssetNode structure](update_alert_rule#assetnode-structure-assetnode) |
| isEnabled      | false| Boolean| Whether it is allowed to take effect. It is set as "true" by default|

### AssetNode Structure <assetnode>

| Name | Required or Not | Data Type | Description |
|----------|--------------|--------------|----------|
| treeId   | true         | String       | Asset tree ID |
| assetId  | true         | String       | Asset ID. [How to get assetId](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)  |


## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
|data|null|Null|




## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=update&orgId=1c499110e8800000&isPatchUpdate=false
{
	"alertRule": {
		"ruleId": "user BID",
		"ruleDesc": {
            "defaultValue": "Grid is connected from converter",
			"i18nValue": {
				"en_US": "Grid is connected from converter",
				"zh_CN": "电网由变频器连接"
			}
		},
		"modelId": "EnOS_Solar_CombinerBox",
		"measurepointId": "CBX.BranchStateAttr",
		"condition": "CBX.BranchStateAttr = 18",
		"severityId": "WARN",
		"contentId": "planetTemperature",
		"tags": {
			"key1": "v1"
		},
		"orgId": "1c499110e8800000",
		"scope": [{
			"treeId": "ptde66nd",
			"assetId": "FbFy8qyz"
		}],
		"isEenabled": true
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
