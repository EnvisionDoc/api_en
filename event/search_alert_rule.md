# Search Alert Rule

Query alert rule under a specific organization.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)         |


## Request Parameters (Body)
| Name            | Required or Not | Data Type | Description |
|------|-----------------|-----------|-------------|
| modelId        | false         | String                | Model applicable for the alert rule|
| measurepointId | false         | String                | Asset measurement point. [How to get pointId>>](/docs/api/en/latest/api_faqs.html#how-to-get-the-measuremet-point-pointid-pointid) |
| expression      | false         | String | Query expression, which supports for sql-like query. The fields that are supported for query include: `ruleId`, `modelId`, `measurepointId`. The supported arithmetic operators are “=” and “in”, and the logical operator is "and" and "or". [How to use expression>>](/docs/api/en/latest/api_faqs.html#how-to-use-expression) |
| pagination  | false  |Pagination request struct | Random pagination. The default is to sort in descending order by `occurTime`. When not specified, the default pagination size is 10 pages. See [Pagination Request Struct>>](/docs/api/en/latest/overview.html#pagination-request-struct) |



## Response Parameters

| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| data | AlertRule struct | Alert rule information. See [AlertRule Struct](search_alert_rule#alertrule-struct-alertrule). |


### AlertRule Struct <alertrule>

| Name |  Data Type | Description |
|----------------|--------------|-----------------------|----------------------------|
| orgId          | String    | Organization ID|
| ruleId         | String                | Alert rule ID, which is to be defined by the user|
| ruleDesc        | StringI18n            | Alert description|
| modelId           | String                | Model applicable for the alert rule|
| measurepointId   | String                | Asset measurement point. [How to get pointId>>](/docs/api/en/latest/api_faqs.html#how-to-get-the-measuremet-point-pointid-pointid) |
| condition         | String                | Query expression-like statement. For example, "${temperature} = 19" indicates that the value of the measurement point "temperature" is 19. A slash "/" is used to express the hierarchical relationship, for which only one downward layer is supported now. For example, “${pointA/att1} = 18” indicates the "att1" attribute value of the measurement point "A" is 18. |
| isEnabled      | Boolean               | Whether it is allowed to take effect |
| severityId         | String                | Alert severity ID|
| severityDesc     | StringI18n | Internationalized description of alert severity|
| contentId      | String                | Alert content ID|
| contentDesc  |  StringI18n | Internationalized description of alert content |
| tags           | tags struct            | Alert rule tag|
| isRoot           | Boolean| Whether it is a root alert.|
| scope            | AssetNode struct | The scope of the alert rule which is specified by the node on the asset tree. See [AssetNode Struct](search_alert_rule#assetnode-struct-assetnode).  |
| source |false| String |Customized data source that indicates the data source to which the alert rule applies. "null" for applying to EnOS Cloud; "edge" for applying to EnOS Edge.|
| triggeringDelayTimer | false | Integer | Time to delay the alert triggering. The unit is seconds and the range is [60 - 10800]. The alert will be triggered when an anomaly that matches the alert rule occurs, and this anomaly does not return to normal within the set time. When it is 0, trigger the alert immediately. |


### AssetNode Struct <assetnode>

| Name | Required or Not | Data Type | Description |
|----------|--------------|--------------|----------|
| treeId   | true         | String       | Asset tree ID. If it is "all", it indicates that this is a special node, standing for the globality of the organization. |
| assetId  | true         | String       | Asset ID.  |


## Sample

### Request Sample

```json
POST https://{apigw-address}/event-service/v2.1/alert-rules?action=search&orgId=yourOrgId
{
    "modelId": "EnOS_Solar_CombinerBox",
    "measurepointId": "CBX.BranchStateAttr"
}

```

### Return Sample

```json
{
    "pagination": {
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 1,
        "sortedBy": [{
            "field": "updateTime",
            "order": "DESC"
        }]
    },
    "code": 0,
    "msg": "OK",
    "requestId": "a9689b9f-0cb6-4e47-a41c-bd459b687309",
    "data": [{
        "orgId": "yourOrgId",
        "ruleId": "zh_model_struct",
        "ruleDesc": {
            "defaultValue": "Grid is connected from converter",
            "i18nValue": {
                "en_US": "Grid is connected from converter",
                "zh_CN": "电网由变频器连接"
            }
        },
        "modelId": "zh_model",
        "measurepointId": "aa",
        "condition": "${aa} = 18",
        "isEnabled": true,
        "severityId": "WARN",
        "severityDesc": {
            "defaultValue": "WARN"
        },
        "contentId": "planetTemperature",
        "contentDesc": {
            "defaultValue": "连接"
        },
        "typeId": "warning_Type",
        "typeDesc": {
            "defaultValue": "connected"
        },
        "tags": {
            "key1": "v1"
        },
        "isRoot": false,
        "scope": [{
            "treeId": "ptde66nd",
            "assetId": "FbFy8qyz"
        }]
    },{
        "orgId": "yourOrgId",
        "ruleId": "zh_model_struct2",
        "ruleDesc": {
            "defaultValue": "Grid is connected from converter",
            "i18nValue": {
                "en_US": "Grid is connected from converter",
                "zh_CN": "电网由变频器连接"
            }
        },
        "modelId": "zh_model",
        "measurepointId": "aa",
        "condition": "${aa} = 18",
        "isEnabled": true,
        "severityId": "WARN",
        "severityDesc": {
            "defaultValue": "WARN"
        },
        "contentId": "planetTemperature",
        "contentDesc": {
            "defaultValue": "连接"
        },
        "typeId": "warning_Type",
        "typeDesc": {
            "defaultValue": "connected"
        },
        "tags": {
            "key1": "v1"
        },
        "isRoot": false,
        "scope": [{
            "treeId": "ptde66nd",
            "assetId": "FbFy8qyz"
        }]
    }]
}
```
