# Search Device

*Note: This documentation is in the progress of translation. Thanks for your visit!*

查询设备信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|----------------|---------------|--------------------------|---|
| expression| False         | String               | 查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1) |
| pagination| False         | pagination请求结构体 | 随机分页，默认就是按照occurTime倒序排列，用户不能指定排序字段。默认分页大小是10。[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)|
| projection| False         | Projection结构体    |用于在接口请求中描述待返回的对象projection。详见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection)  |



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    Device结构体        | 网关下指定分页的一组子设备信息，见[Device结构体](/docs/api/en/latest/connect/search_device.html#id4) |


### Device结构体

| 名称| 数据类型 | 描述         |
|------------------|-----------------------|----------------------------|
| orgId |  String | 资产所属的组织ID |
| assetId  | String         | 资产ID|
| modelId             | String                          | 资产所属模型ID|
| modelIdPath      | String                            | 模型ID的路径                                                               |
| productKey       | String                            | Product Key                                                                |
| productName      | StringI18n                        | product名称                                                                |
| productType      | String                            | 产品类型                                                                   |
| dataFormat       | String                            | 数据格式。Custom表示支持用户自定义数据格式，Json表示只支持EnOS设备协议格式 |
| deviceKey        | String                            | 设备key                                                                    |
| deviceName       | StringI18n                        | 设备名称                                                                   |
| deviceSecret     | String                            | 设备的连接秘钥                                                             |
| deviceDesc       | String                            | 设备描述                                                                   |
| timezone         | String                            | 设备所在时区                                                               |
| deviceAttributes | Map（Key为String，Value为String） | 设备的属性                                                                 |
| deviceTags       | Map（Key为String，Value为String） | 设备的标志                                                                 |
| createTime       | Long                              | 设备的创建时间                                                             |
| status           | String                            | 设备的状态（online、offline、inactive或disable）                         |
| activeTime       | Long                              | 设备的激活时间                                                             |
| lastOnlineTime   | Long                              | 设备最后一次上线时间                                                       |
| lastOfflineTime  | Long                              | 设备最后一次离线时间                                                       |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=search&orgId=o15475450989191
method: POST
requestBody: {
	"pagination": {
		"pageNo": 2,
		"pageSize": 5
	}
}
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "59ecd409-7baa-4726-ba10-c0bde35ffb09",
	"data": [{
		"orgId": "o15475450989191",
		"assetId": "7u4bfyO0",
		"modelId": "lxctimelooker",
		"modelIdPath": "/lxctimelooker",
		"productKey": "vzzG0GFg",
		"productName": {
			"defaultValue": "lxcpro",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "TeyRhjOnfh",
		"deviceName": {
			"defaultValue": "time2dev11",
			"i18nValue": {}
		},
		"deviceSecret": "iCp1wixMv843ABrYnD3I",
		"deviceDesc": null,
		"timezone": "+09:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1558421750575,
		"status": "offline",
		"activeTime": 1558482329972,
		"lastOnlineTime": 1560743915454,
		"lastOfflineTime": 1560744095454
	}, {
		"orgId": "o15475450989191",
		"assetId": "Fi0HQ8FO",
		"modelId": "AlterTest0615",
		"modelIdPath": "/AlterTest0615",
		"productKey": "gHuxgR8s",
		"productName": {
			"defaultValue": "AlterTest0615_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "325132545",
		"deviceName": {
			"defaultValue": "AlterTest0615",
			"i18nValue": {}
		},
		"deviceSecret": "V2Ny4NTlt40NZDaF3xj5",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1560564762147,
		"status": "offline",
		"activeTime": 1560564838673,
		"lastOnlineTime": 1560743931247,
		"lastOfflineTime": 1560743931712
	}, {
		"orgId": "o15475450989191",
		"assetId": "6FytqleL",
		"modelId": "AlterTest0614",
		"modelIdPath": "/AlterTest0614",
		"productKey": "zpFCD7pd",
		"productName": {
			"defaultValue": "AlterTest0614_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "324314123431",
		"deviceName": {
			"defaultValue": "AlterTest0614",
			"i18nValue": {}
		},
		"deviceSecret": "R6wPIKHaMrcwnpzOSZYe",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"aaa": 1,
			"76": 0
		},
		"deviceTags": {},
		"createTime": 1560493341919,
		"status": "offline",
		"activeTime": 1560493435761,
		"lastOnlineTime": 1560743930253,
		"lastOfflineTime": 1560743930346
	}, {
		"orgId": "o15475450989191",
		"assetId": "V4TjS0n4",
		"modelId": "AlertTest0613",
		"modelIdPath": "/AAA100/AlertTest0613",
		"productKey": "gTsWB8mX",
		"productName": {
			"defaultValue": "AlertTest0613_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "324132514331",
		"deviceName": {
			"defaultValue": "AlertTest0613",
			"i18nValue": {}
		},
		"deviceSecret": "0u06LivvksMGxtJoSBT5",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"aaa": 1,
			"76": 0
		},
		"deviceTags": {},
		"createTime": 1560389949661,
		"status": "offline",
		"activeTime": 1560390227903,
		"lastOnlineTime": 1560743916848,
		"lastOfflineTime": 1560743929003
	}, {
		"orgId": "o15475450989191",
		"assetId": "wjIXsqTQ",
		"modelId": "zcmx---1",
		"modelIdPath": "/zcmx---1",
		"productKey": "J5GKPipa",
		"productName": {
			"defaultValue": "zccp-----1",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "krL0iNa4as",
		"deviceName": {
			"defaultValue": "zccp-----222",
			"i18nValue": {}
		},
		"deviceSecret": "KUiw16CE4A4QTabkt0QN",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"timestamp1": 1,
			"float1": 1.0,
			"bool11": false,
			"int1": 1,
			"string1": "1",
			"double1": 1.0,
			"12221": false,
			"array1": [1],
			"stuct1": {
				"int11": 1
			},
			"file1": "ftp://a.com/demo.txt",
			"enum": 1,
			"dete1": "2019-05-06"
		},
		"deviceTags": {},
		"createTime": 1559294746435,
		"status": "inactive",
		"activeTime": 0,
		"lastOnlineTime": 0,
		"lastOfflineTime": 0
	}],
	"pagination": {
		"sortedBy": null,
		"pageNo": 2,
		"pageSize": 5,
		"totalSize": 6511
	}
}
```

