# Aggregate Active Alerts

*Note: This documentation is in the progress of translation. Thanks for your visit!*

对实时告警进行统计。

## 请求格式

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate
```

## 请求参数（URI）

| 名称          | 是否必须 | 数据类型 | 描述      |
|---------------|--------|----------|-----------|
| orgId         | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
                                                                 

## 请求参数（Body）
| 名称 | 是否必须 | 数据类型 | 描述 |
|----------------|----------|--------------------|----|
| expression     | false    | String| 查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1) |
| groupByField   | true     | String             | 分组字段：`contentId`，`assetId`，`modelId`，`measurepointId`，`severityId`，`typeId`，`subTypeId` |
| startOccurTime | false    | String| 告警触发时间的起始时间，见[API在使用的时间参数](/docs/api/en/latest/api_faqs.html#id5)    |
| endOccurTime   | false    | String| 告警触发时间的结束时间，见[API在使用的时间参数](/docs/api/en/latest/api_faqs.html#id5) |



## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | Map（Key为String，Value为Integer） | Key为分组字段的取值，value为对应对象在指定时间段内对象发生告警的数量|


## 输入输出示例

### 请求示例

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=aggregate&orgId=1c499110e8800000

{
	"groupByField": "assetId"
}

```

### 返回示例

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "12995105-514a-4706-9749-5930fd7145f9",
	"data": {
		"uEZPYKL0": 5,
		"J123maMn": 2,
		"Gx5mj2OE": 1,
		"qu5TmJRj": 1,
		"TMET5UCK": 1,
		"IkaNsY3h": 1,
		"L03wWUoU": 1,
		"OAESlCPt": 1
	}
}

```

## Java SDK调用示例

```java
public void testAggregateActiveAlert(){  
       String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";  
       String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";  
       AggregateActiveAlertRequest request = new AggregateActiveAlertRequest();  
       request.setOrgId("1c499110e8800000");  
       request.setGroupByField("assetId");  
       request.headerParams().put("apim-accesskey","4ced4f38-1ced-476e0a446215-a602-4307");  
	       try {  
	           AggregateActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
	                   .url("https://{apigw-address}")  
	                   .getResponse(request, AggregateActiveAlertResponse.class);  
	           Gson gson = new Gson();  
	           System.out.println(gson.toJson(response));  
	       }catch(Exception e){  
	           System.out.print(e);  
	       }  
	   }
```