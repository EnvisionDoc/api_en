# 查询模型

根据模型标识符（`modelId`）查询模型

## 请求格式

```
https://apigw-address/xxx/model-service/v2.0/thing-models?action=get&orgId={}&modelId={}&scope={}
```

## 请求参数（URI）

| Name    | In（Path/Query） | Required | Data Type | Description                                                      |
|:--------|:-----------------|:---------|:----------|:-----------------------------------------------------------------|
| orgId   | Query            | true     | String    | 组织id                                                           |
| scope   | Query            | false    | Integer   | 查询范围。0：只从指定orgId；1：从指定orgId和公有orgId找。默认为1 |
| modelId | Query            | true     | String    | 模型id                                                           |

## 响应参数

| Name    | Data Type  | Description |
|:--------|:-----------|:------------|
| modelId | **String** | 模型id      |
| desc    | **String** | 模型描述    |

## 示例

### 请求示例

```
GET /model-service/v2.0/thing-models?action=get&modelId=xxxx&orgId=xxx
```

### 返回示例

```json
{
  "msg": "OK",
  "code": 0,
  "data": {
    "modelId": "<thingmodelId>",
    "desc": "..."
  }
}

```
