# Search Sub-Device

*Note: This documentation is in the progress of translation. Thanks for your visit!*

搜索网关下的子设备信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevice
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|--------------------|----------|-----------|--------------|
| gateway | True      | DeviceIdentfier结构体 | 需要添加子设备的网关信息，见[DeviceIdentfier结构体](/docs/api/en/latest/connect/search_sub_device.html#deviceidentifier) |
| pagination  | False      | Pagination请求结构体  | 分页参数，如果不填，默认每页10条。目前，不支持排序（忽略排序字段）。见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination) |


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
| data | Device结构体                     | 网关下指定分页的一组子设备信息，见[Device结构体](/docs/api/en/latest/connect/search_sub_device.html#id3)    |


### Device结构体

| 名称| 数据类型 | 描述         |
|------------------|--------------------|-------|
| orgId            | String                            | 资产所属的组织ID|
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



## 错误码

| 代码| 数据类型 | 描述         |
|-------------|-----------------------------------|-----------------------------|
| 11738 |                | 参数gateway不是网关设备                |


## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/device-topos?action=searchSubDevices&orgId=o15475450989191
method: POST
requestBody: {"gateway":{"assetId":"J1Rqyaqz"}}
```

### 返回示例

```json
responseBody: {
		"code": 0,
		"msg": "OK",
		"requestId": "498d1c5b-7c4f-401a-a9ff-9072931bec2e",
		"data": [{
			"orgId": "o15475450989191",
			"assetId": "mAEsF3sm",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "Vu82Agp3",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "96Z711wx5d",
			"deviceName": {
				"defaultValue": "testforCreatedevice",
				"i18nValue": {}
			},
			"deviceSecret": "SlqmFerDkPHvnQW5y8wK",
			"deviceDesc": "test for createdevice",
			"timezone": "+08:00",
			"deviceAttributes": {
				"testatt": 111111
			},
			"deviceTags": {},
			"createTime": 1560755091998,
			"status": "inactive",
			"activeTime": 0,
			"lastOnlineTime": 0,
			"lastOfflineTime": 0
		}, {
			"orgId": "o15475450989191",
			"assetId": "gVRwKQ3C",
			"modelId": "AlterTest0617",
			"modelIdPath": "/AlterTest0617",
			"productKey": "Vu82Agp3",
			"productName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"productType": "Device",
			"dataFormat": "Json",
			"deviceKey": "32412434314",
			"deviceName": {
				"defaultValue": "AlterTest0617_Product",
				"i18nValue": {}
			},
			"deviceSecret": "65hjmU4MwiFiCFjWv588",
			"deviceDesc": null,
			"timezone": "+10:00",
			"deviceAttributes": {},
			"deviceTags": {},
			"createTime": 1560730295671,
			"status": "offline",
			"activeTime": 1560730567958,
			"lastOnlineTime": 1560743932166,
			"lastOfflineTime": 1560744112166
		}],
		"pagination":{"sortedBy":null,"pageNo":1,"pageSize":2,"totalSize":2}}
```

