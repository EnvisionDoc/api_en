# Get Gateway

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取子设备对应的网关信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=getGateway
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |



## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|--------------------|----------|-----------|--------------|
| subDevices           | True      | DeviceIdentfier结构体 | 识别子设备的标志信息，见[DeviceIdentfier结构体](/docs/api/en/latest/connect/get_gateway.html#deviceidentifier) |


### DeviceIdentifier结构体

注：以下字段必须提供`assetId`或者`(productKey, deviceKey)`。

| 名称      | 数据类型 |描述|
|----------------|----------------|------------------|
| assetId  | String         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid) |
| productKey | String         | Product Key      |
| deviceKey | String         | 设备key          |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| data | Device结构体                          | 网关设备信息，见[Device结构体](/docs/api/en/latest/connect/get_gateway.html#device-devicetstruc)               |


### Device结构体<devicetstruc>

| 名称  |  数据类型      | 描述               |
|-------|-------|---------------------------|
| orgId |  String | 资产所属的组织ID|
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
| status           | String                            | 设备的状态（online, offline, inactive 或 disable）                         |
| activeTime       | Long                              | 设备的激活时间                                                             |
| lastOnlineTime   | Long                              | 设备最后一次上线时间                                                       |
| lastOfflineTime  | Long                              | 设备最后一次离线时间                                                       |


## 示例 1

### 请求示例

```
POST
https://{apigw-address}/connect-service/v2.1/device-topos?action=getGateway&orgId=o15475450989191
{
"subDevice":{"assetId":"gVRwKQ3C"}
}
```

### 返回示例

```json
responseBody: {
	"code": 0,
	"msg": "OK",
	"requestId": "49ef6c03-02a0-449b-ab1e-92812071de80",
	"data": {
		"orgId": "o15475450989191",
		"assetId": "J1Rqyaqz",
		"modelId": "AlterTest0617",
		"modelIdPath": "/AlterTest0617",
		"productKey": "JvY2tkBD",
		"productName": {
			"defaultValue": "testtopo",
			"i18nValue": {}
		},
		"productType": "Gateway",
		"dataFormat": "Json",
		"deviceKey": "qjndvVkK9E",
		"deviceName": {
			"defaultValue": "testtopo",
			"i18nValue": {}
		},
		"deviceSecret": "mUb5wk5ZylNcHwnhAGUO",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1560759829419,
		"status": "inactive",
		"activeTime": 0,
		"lastOnlineTime": 0,
		"lastOfflineTime": 0
	}
}
```

