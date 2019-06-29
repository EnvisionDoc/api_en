# Search Alert Severity

*Note: This documentation is in the progress of translation. Thanks for your visit!*

分页查询告警级别。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-severities?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| expression         | false    | String   | 查询表达式，查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1)|
| pagination     | false     | Pagination请求结构体| 分页的参数。如果不填，默认每页10条。按照`updateTime`降序排序。用户可以指定`AlertSeverity`结构体中的字段作为排序字段。见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)    |

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | AlertSeverity结构体 | 告警级别，见[AlertSeverity结构体](/docs/api/en/latest/event/search_alert_severity.html#id4)|

### AlertSeverity结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| severityId        | String                | 告警级别编号|
| orgId          | String                | 资产所属的组织ID|
| severityDesc   | StringI18n            | 告警级别描述 |
| tags        | Tag结构体          | 标签|
| updatePerson        | String                | 更新人|
| updateTime    | Long                | 更新的UTC时间



## 输入输出示例

### 请求示例

```json
POST  https://{apigw-address}/event-service/v2.1/alert-severities?action=search&orgId=1c499110e8800000
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "severityID",
			"order": "ASC"
		}]
	}
}
```

### 返回示例

```json
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"totalSize": 19,
		"sortedBy": [{
			"field": "severityID",
			"order": "ASC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "bd591868-0eb1-46dc-a989-c1de33cc671e",
	"data": [{
		"severityId": "001",
		"orgId": "1c499110e8800000",
		"severityDesc": {
			"i18nValue": {
				"en_US": "Serious！！！",
				"zh_CN": "严重！！！"
			}
		},
		"tags": {
			"111": "2222"
		},
		"updatePerson": "yj_test_customer",
		"updateTime": 1559204166000
	}]
}
```

## Java SDK调用示例

```java
public void testSearchAlertSeverity() {  
    SearchAlertSeverityRequest request = new SearchAlertSeverityRequest();  
    request.setOrgId("1c499110e8800000");  
    Pagination pagination = new Pagination();  
    pagination.setPageSize(1);  
	    pagination.setPageNo(1);  
    Sorter sorter = new Sorter("severityID", Sorter.Order.ASC);  
    List<Sorter> sorterList = new ArrayList<>();  
    sorterList.add(sorter);  
	    pagination.setSorters(sorterList);  
	    request.setPagination(pagination);  
	    request.headerParams().put("apim-accesskey", "4ced4f38-1ced-476e0a446215-a602-4307");  
	    try {  
	        SearchAlertSeverityResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                .url("https://{apigw-address}")  
	                .getResponse(request, SearchAlertSeverityResponse.class);  
	        Gson gson = new Gson();  
	        System.out.println(gson.toJson(response));  
	    } catch (Exception e) {  
	        System.out.print(e);  
	    }  
}
```