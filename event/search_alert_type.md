# Search Alert Type

*Note: This documentation is in the progress of translation. Thanks for your visit!*

分页查询告警类型。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/alert-types/search?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|------|-----------------|-----------|-------------|
| expression         | false    | String   | 查询表达式，查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1)|
| pagination     | false     |Pagination请求结构体 | 分页的参数。如果不填，默认每页10条。默认按照`updateTime`降序排序。支持用户使用`AlertType`结构体中的字段指定排序。见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination) |

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | AlertType结构体 | 告警类型，见[AlertType结构体](/docs/api/en/latest/event/search_alert_type.html#id4)|

### AlertType结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| typeId        | String                | 告警类型ID|
| typeDesc   | StringI18n            | 告警类型描述|
| orgId          | String                | 资产所属的组织ID|
| parentTypeId        | String          | 父告警类型编号。如果为空，那么它本身就是父类型告警类型|
| tag        | Tag结构体          | 标签|
| updatePerson        | String                | 更新人|
| updateTime    | Long                | 更新的UTC时间|



## 输入输出示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/alert-types/search?action=search&orgId=1c499110e8800000
{
	"pagination": {
		"pageNo": 1,
		"pageSize": 1,
		"sorters": [{
			"field": "typeId",
			"order": "DESC"
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
		"totalSize": 14,
		"sortedBy": [{
			"field": "typeId",
			"order": "DESC"
		}]
	},
	"code": 0,
	"msg": "OK",
	"requestId": "c1be09d8-a6f2-4647-92e1-3c545fa1b3dd",
	"data": [{
		"typeId": "dateType",
		"orgId": "1c499110e8800000",
		"typeDesc": {
			"i18nValue": {
				"en_US": "dateType desc",
				"zh_CN": ""
			}
		},
		"tags": {		
		},
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612655000
	}]
}
```

## Java SDK调用示例

```java
public void testSearchAlertType() {  
        SearchAlertTypeRequest request = new SearchAlertTypeRequest();  
        request.setOrgId(orgId);  
        Pagination pagination = new Pagination();  
        pagination.setPageNo(1);  
        pagination.setPageSize(1);  
        List<Sorter> sorterList = new ArrayList<>();  
        sorterList.add(new Sorter("typeId", Sorter.Order.DESC));  
        pagination.setSorters(sorterList);  
	        request.setPagination(pagination);  
	        try {  
	            SearchAlertTypeResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                    .url("https://{apigw-address}")  
	                    .getResponse(request, SearchAlertTypeResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	        } catch (Exception e) {  
	            e.printStackTrace();  
	        }  
}
```