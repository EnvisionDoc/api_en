# Create Device

*Note: This documentation is in the progress of translation. Thanks for your visit!*

创建设备。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/devices?action=create
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|----------------|---------------|--------------------------|---|
|productKey    | True          | String       | Product Key      |
|timezone | True          | String         | 设备所在时区     |
| deviceName | True          | StringI18n | 设备名称         |
| deviceAttributes | False         | Map       | 设备属性         |
| deviceKey   | False         | String    | 设备key          |
| deviceDesc  | False         | String    | 设备描述信息     |




## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    DeviceCreateResult结构体        | 设备创建返回结果，见[DeviceCreateResult结构体](/docs/api/en/latest/connect/create_device.html#id3) |


### DeviceCreateResult结构体

| 名称| 数据类型 | 描述         |
|------------------|-----------------------|----------------------------|
| productKey       | String                            | Product Key                                                                |
| deviceName       | StringI18n                        | 设备名称                                                                   |
| deviceSecret     | String                            | 设备的连接秘钥                                                             |
| assetId  | String         | 资产ID|


## 错误码

| 代码| 数据类型 | 描述    |
|-----------|----------------|----------------------|
| 11702 |                | deviceKey在数据库中已存在（deviceKey提供的情况下）        |
| 11714 |                | 暂时无法分配设备的key（deviceKey未提供的情况下），请重试 |
| 11739 |                | 该操作将导致超过产品下限定的设备数量                      |




## 示例 1

### 请求示例

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=create&orgId=o15475450989191
method: POST
requestBody: {
    "deviceTags":{
        "test":"test for tags"
    },
    "timezone":"+08:00",
    "source":0,
    "productKey":"Vu82Agp3",
    "deviceAttributes":{
        "testatt":111111
    },
    "deviceName":{
        "defaultValue":"testCreateDevice",
        "i18nValue":{

        }
    },
    "deviceDesc":"test for createdevice"
}
```

### 返回示例

```json
responseBody: {
    "code":0,
    "msg":"OK",
    "requestId":"fd79d0f5-69c5-4fa8-add4-69f5ca1b635f",
    "data":{
        "assetId":"Uvmm5AXU",
        "productKey":"Vu82Agp3",
        "deviceKey":"1115pswxk7",
        "deviceSecrete":"Z5YtZaQpK5IWocakV7zQ"
    }
}
```

