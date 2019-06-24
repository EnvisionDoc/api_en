# 搜索模型

根据组织id搜索模型

## 请求格式

```
https://apigw-address/xxx/model-service/v2.0/thing-models?action=search
```

## 请求参数（Body）

| Name       | In（Path/Query） | Required | Data Type | Description                                                                              |
|:-----------|:-----------------|:---------|:----------|:-----------------------------------------------------------------------------------------|
| orgId      | Query            | true     | String    | 组织id                                                                                   |
| scope      | Query            | false    | Integer   | 查询范围。 0：只从指定orgId查寻找； 1：从指定orgId和公共orgId查寻。默认为1               |
| expression | Query            | false    | String    | 查询表达式。不可出现一级参数中已经出现的字段,详见[查询表达式](expression)。              |
| projection | Query            | false    | Array     | 对结果进行projection，对于符合条件的搜索仅返回符合条件的字段，不设置则默认返回全部fileds |
| pagination | Query            | false    | Map       | [分页参数](#pagination)                                                                  |

### 查询表达式 <expression>

查询的表达式如下：

```
expr := {expr} or {expr}
    | {expr} and {expr}
    | {id-expr}
    | {tag-expr}

id-expr := modelId = 'xxx'
    | modelId in ('xx1', 'xx2')

tag-expr := tag.key1 = 'xxx' [ and tag.key2 = 'yyy' ] ...

```

示例1:
modelId in ('xx1', 'xx2') and tag.key1 = 'xxx'


示例2:

modelId in ('xx1', 'xx2') and tag.key1 = 'xxx'

### pagination <pagination>

| Name      | Data Type   | Description  |
|:----------|:------------|:-------------|
| pageNo    | **Integer** | 当前页码     |
| pageSize  | **Integer** | 每页的记录数 |
| totalSize | **Integer** | 总记录数     |
| sortedBy  | **Array**   | 排序方式     |

## 响应参数

| Name       | Data Type | Description             |
|:-----------|:----------|:------------------------|
| pagination | **Map**   | [分页参数](#pagination) |
| items      | **Array** | [查询到的模型](#items)  |

### items

| Name    | Data Type  | Description |
|:--------|:-----------|:------------|
| modelId | **String** | 模型id      |
| name    | **String** | 模型名称    |

## 示例

### 请求示例

```json
POST /model-service/v2.0/thing-models?action=search
{
  "expression": "modelId in ( \"cshan_20181120_000\" )",
  "pagination": {
    "pageNo": 1,
"pageSize": 10
"totalSize": 100
"sortedBy":[
   {
	 "field": "modelId",
	 "order": "DESC"
},
{
	 "field": "name",
	 "order": "ASC"
},
]
  },
  "projection": [
    "modelId",
    "name"
  ],
  "orgId": "1ad3889266800000"
}
```


### 返回示例

```json
{
  "msg": "OK",
  "code": 0,
  "data": {
    "pagination": {
      "pageNo": 1,
      "pageSize": 10，
"totalSize": 100,
    },
    "items": [
      {
        "modelId": "<thingModelId>",
        "name": "..."
      },
      {
        "modelId": "<thingModelId>",
        "name": "..."
      }
    ]
  }
}
```
