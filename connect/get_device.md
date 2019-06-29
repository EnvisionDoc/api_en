# Get Device

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取设备信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=get
```

## 请求参数（URI）

注：以下字段必须提供`assetId`或者`(productKey, deviceKey)`。

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | 设备key          |
    

## 响应参数

| 名称 | 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    Device结构体        | 网关设备信息，见[Device结构体](/docs/api/en/latest/connect/get_device.html#id3) |


### Device结构体

| 名称 | 数据类型 | 描述         |
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
url:https://{apigw-address}/connect-service/v2.1/devices?action=get&orgId=o15475450989191&assetId=9HhK0YxX
method: GET
headers: {}
requestBody: null
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "835a5cc4-4487-4bf2-961a-55bc0ee77d02",
	"data": {
		"orgId": "o15475450989191",
		"assetId": "9HhK0YxX",
		"modelId": "abc-test",
		"modelIdPath": "/abc-test",
		"productKey": "mJo2gO5u",
		"productName": {
			"defaultValue": "abc-pk",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "VcwTHRvYFb",
		"deviceName": {
			"defaultValue": "testforname",
			"i18nValue": {}
		},
		"deviceSecret": "hOiv7SJAYuyVJp3CXJWJ",
		"deviceDesc": "test for undatedevice",
		"timezone": "+08:00",
		"deviceAttributes": {
			"int11": 617
		},
		"deviceTags": {
			"test": "test for tags"
		},
		"createTime": 1557905107199,
		"status": "offline",
		"activeTime": 1557909526473,
		"lastOnlineTime": 1560743931658,
		"lastOfflineTime": 1560744111658
	}
}
```

