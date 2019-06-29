# Get Alert Content

*Note: This documentation is in the progress of translation. Thanks for your visit!*

根据组织ID和内容ID获取告警内容。

## 请求格式

```
GET https://{apigw-address}/event-service/v2.1/alert-contents action=get&orgId=1c499110e8800000
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| contentId         | Query            | true     | String    | 告警内容ID。                |
                                                                 

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | AlertContent结构体 | 告警内容，见[AlertContent结构体](/docs/api/en/latest/event/get_alert_content.html#id3)|

### AlertContent结构体

| 名称  | 数据类型      | 描述               |
|----------------|-----------------------|----------|
| contentId| String           | 内容ID                 |
| contentDesc | StringI18n | 告警内容描述         |
| modelId| String           | 模型ID                 |
| orgId          | String                | 资产所属的组织ID|
| alertType  | AlertType结构体  | 告警类型，见[AlertType结构体](/docs/api/en/latest/event/search_alert_type.html#id4)               |
| subAlertType| AlertType结构体  | 子告警类型，见[AlertType结构体](/docs/api/en/latest/event/search_alert_type.html#id4)             |
| tags| Tag结构体        | 用户自定义告警内容标签 |
| updatePerson| String           | 更新人员名称           |
| updateTime| Long             | 最后一次更新时间       |



## 输入输出示例

### 请求示例

```json
GET https://{apigw-address}/event-service/v2.1/alert-contents?action=get &contentId=doubleContentuid&orgId=1c499110e8800000
```

### 返回示例

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "f40fbb09-ce20-463f-bb18-6659a8bd6926",
	"data": {
		"contentId": "doubleContentuid",
		"contentDesc": {
			"i18nValue": {
				"en_US": "doubleContentuid desc",
				"zh_CN": ""
			}
		},
		"modelId": "ssss",
		"orgId": "1c499110e8800000",
		"updatePerson": "yj_test_customer",
		"updateTime": 1546612131000,
		"alertType": {
			"typeId": "doubleType",
			"typeDesc": {
				"i18nValue": {
					"en_US": "doubleType desc",
					"zh_CN": ""
				}
			},
			"tags": {	
			},
			"updateTime": 0
		},
		"subAlertType": {
			"typeDesc": {
				"i18nValue": {
					"en_US": "doubleType desc",
					"zh_CN": ""
				}
			},
			"tags": {	
			},
			"updateTime": 0
		},
		"tags": {	
		}
	}
}
```

## Java SDK调用示例

```java
public void testGetAlertContent() {  
        final String contentId = "doubleContentuid";  
        GetAlertContentRequest request = new GetAlertContentRequest();  
        request.setOrgId(orgId);  
        request.setContentId(contentId);  
        try {  
            GetAlertContentResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())  
                    .url("https://{apigw-address}")  
	                    .getResponse(request, GetAlertContentResponse.class);  
	            Gson gson = new Gson();  
	            System.out.println(gson.toJson(response));  
	            if (response.getCode() == 0) {  
	                System.out.println(response.getData());  
	            }  
	        } catch (Exception e) {  
	            e.printStackTrace();  
	        }  
}
```