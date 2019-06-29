# Cancel Command

*Note: This documentation is in the progress of translation. Thanks for your visit!*

取消缓存命令的接口。如果有`commandId`，则取消单个命令，如果无`commandId`，则取消该设备的所有缓存命令。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/commands?action=cancel
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                |
| assetId  | Query            | False   | String         | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid) |
| productKey | Query          | False       | String       | Product Key      |
| deviceKey | Query           | False      | String       | 设备key          |
| commandId | Query            | False    | String        | 命令key          |


## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    getCommand结构体        | 被取消的命令列表。参见[getCommand结构体](/docs/api/en/latest/connect/get_command.html#id3) |




## 示例 1

### 请求示例

```
https://{apigw-address}/connect-service/v2.1/commands?action=cancel&deviceKey=mqtt_01&productKey=bXuuAiku&orgId=o15541858646501
```

### 返回示例

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": [{
        "commandId": "2278935391225618432",
        "orgId": "o15541858646501",
        "productKey": "bXuuAiku",
        "deviceKey": "mqtt_01",
        "assetId": "oxWwM9i5",
        "createTime": 1560505243577,
        "createLocalTime": 1560505243577,
        "commandType": 1,
        "commandName": {
            "defaultValue": "Int_value",
            "i18nValue": {
                "en_US": "Int_value"
            }
        },
        "timeout": 1,
        "pendingTtl": 6000,
        "state": 1,
        "tslIdentifier": "Int_value",
        "inputData": 222
    }]
}
```

