# Get Command

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取单个命令信息。

## 请求格式

```
https://{apigw-address}/connect-service/v2.1/commands?action=get
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

| 名称 | 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    getCommand结构体        | 命令的相应信息，见[getCommand结构体](/docs/api/en/latest/connect/get_command.html#id3) |

### getCommand结构体

| 名称 | 数据类型| 描述|
|-----------------|---------------------------|----------------|
| commandId       | String| 命令ID|
| orgId          | String    | 资产所属的组织ID  |
| productKey | String          | Product Key      |
| deviceKey  | String     | 设备key          |
| assetId   | String      | 资产ID|
| createTime      | Long| 创建时间|
| createLocaltime | String| 本地创建时间|
| commandType     | Integer| 命令类型。1. 测点设置 2. 服务调用|
| commandName     | StringI18n| 命令的名称。对于测点设置来说，是测点名称。对于服务调用来说，是服务名称。|
| timeout         | Integer| 命令超时时长，单位是秒 范围[1-60]，默认30|
| pendingTtl      | Long| 命令缓存时长，单位是秒 范围[ 0 - 48 * 60 * 60 ]，默认0，表示即时命令|
| state           | Integer| 命令状态，用1-7的整数表示。 1表示已创建；2表示已取消；3表示已过期；4表示已下发；5表示发送成功；6表示发送失败；7表示响应超时。|
| tslIdentifier   | String| 物模型中的对应identifier。对于测点设置命令来说，是测点identifier。对于服务调用命令来说，是服务identifier。|
| inputData       | Map（Key为String，Value为String，Number，Array或Object） | 输入数据。对于测点设置命令来说，key为测点identifier，value为需要设置的测点值。对于服务调用命令来说，为服务输入参数。value数据类型需要符合物模型的定义 |
| outputData      | Map（Key为String，Value为String，Number，Array或Object） | 输出数据。对于测点设置命令来说，该字段无返回。对于服务调用命令来说，该字段表示服务的输出结果。value数据类型需要符合物模型的定义。|




## 示例 1

### 请求示例

```
https://{apigw-address}/connect-service/v2.1/commands?action=get&deviceKey=WRJ2c1yMa5&productKey=doxkidR0&commandId= 2242591201245044736&orgId=o15541858646501
```

### 返回示例

```json
{
    "code": 0,
    "msg": "Success",
    "submsg": null,
    "requestId": "7d863d517eae4f18a2776452eb1305bb",
    "data": {
        "commandId": "2242591201245044736",
        "orgId": "sysenos2018",
        "productKey": "doxkidR0",
        "deviceKey": "WRJ2c1yMa5",
        "assetId": "KmItYUh4",
        "createTime": 1556172678510,
        "createLocalTime": 1556172678510,
        "commandType": 2,
        "commandName": {
            "defaultValue": "",
            "i18nValue": {
                "en_US": "test_fu_wu"
            }
        },
        "timeout": 30,
        "pendingTtl": 1000,
        "state": 2,
       
        "tslIdentifier": "test_fu_wu",
        "inputData": {
            "can_shu2": 1.3,
            "can_shu": 13
        },
        "outputData": {}
    }
}
```

