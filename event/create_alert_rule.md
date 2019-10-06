# Create Alert Rule

Creates an alert rule. The system will verify the validity of the input parameters:

- Whether the specified model (`modelId`) is available under the organization
- Whether the specified measuring point (`measurepointId`) is valid
- Whether the specified alert severity (`severityId`) exists
- Whether the specified alert content (`contenId`) exists
- Whether the specified scope (`scope`) of asset nodes where the rule takes effect exists


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=create
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)         |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|----------------|--------------|-----------------------|----------------------------|
| ruleId         | true         | String                | Alert rule ID, which is to be defined by the user.|
| ruleDesc       | true         | StringI18n            | Alert description|
| modelId        | true         | String                | Model applicable for the alert rule|
| measurepointId | true         | String                | Asset measurement point. [How to get pointId>>](/docs/api/en/latest/api_faqs.html#how-to-get-the-measuremet-point-pointid-pointid) |
| condition      | true         | String                | Query expression-like statement. For example, "${temperature} = 19" indicates that the value of the measurement point "temperature" is 19. A slash "/" is used to express the hierarchical relationship, for which only one downward layer is supported now. For example, “${pointA/att1} = 18” indicates the "att1" attribute value of the measurement point "A" is 18. [How to use expression>>](/docs/api/en/latest/api_faqs.html#how-to-use-expression) |
| severityId     | true         | String                | Alert severity ID|
| contentId      | true         | String                | Alert content ID|
| tags           | false        | tags struct            | Alert rule tag|
| isEnabled      | false        | Boolean               | Whether it is allowed to take effect. It takes effect ("true") by default. |
|isRoot|false|Boolean|Whether it is a root alert, which is "false" by default.|
| scope          | true         | AssetNode struct | Specify a node on the asset tree to indicate the scope of the alert rule. See [AssetNode Struct](create_alert_rule#assetnode-struct-assetnode). |
| source |false| String |Customized data source that indicates the data source to which the alert rule applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|
| triggeringDelayTimer | false | Integer | Time to delay the alert triggering. The unit is seconds and the range is [60 - 10800]. The alert will be triggered when an anomaly that matches the alert rule occurs, and this anomaly does not return to normal within the set time. When it is 0, trigger the alert immediately. See [Tutorial: Setting Alert Triggering Delay Timer](docs.eniot.io/docs/device-connection/en/latest/howto/alert/setting_alert_triggering_delay_timer.html). |


### AssetNode Struct <assetnode>

| Name | Required or Not | Data Type | Description |
|----------|--------------|--------------|----------|
| treeId   | true         | String       | Asset tree ID. If it is set as "all", it indicates that this is a special node, standing for the globality of the organization.  |
| assetId  | true         | String       | Asset ID. [How to get assetId>>](/docs/api/en/latest/api_faqs.html#how-to-get-asset-id-assetid-assetid)  |



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | String | ruleId |



## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=create&orgId=yourOrgId
{
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
    "condition": "${CBX.BranchStateAttr} = 18",
    "severityId": "WARN",
    "contentId": "planetTemperature",
    "tags": {
        "key1": "v1"
    },
    "orgId": "yourOrgId",
    "scope": [{
        "treeId": "ptde66nd",
        "assetId": "FbFy8qyz"
    }],
    "isEnabled": true,
    "isRoot": true
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
