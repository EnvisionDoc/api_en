# Search Thing Model

*Note: This documentation is in the progress of translation. Thanks for your visit!*

根据组织id搜索物模型。

## 请求格式

```
https://{apigw-address}/model-service/v2.1/thing-models?action=search
```

## 请求参数（Body）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|:-----------|:-----------------|:---------|:----------|:-----------------------------------------------------------------------------------------|
| orgId      | Query            | True     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)|
| scope      | Query            | False    | Integer   | 查询范围。 0：只从指定orgId查寻找； 1：从指定orgId和公共orgId查寻。默认为1               |
| expression | Query            | False    | String    | 查询表达式，支持类sql的查询。目前支持查询的字段是`modelId`，`assetId`，`measurepointId`，`hitRuleId`，`severityId`，`typeId`，`subTypeId`，`contentId`，`eventType`，`eventId`，`tag`。支持的算术运算符是=，in，逻辑运算符是and。[如何使用查询表达式](/docs/api/en/latest/api_faqs.html#id1) |
| projection | Query            | False    | String Array     | 对结果进行projection，对于符合条件的搜索仅返回符合条件的字段，不设置则默认返回全部fields。详见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection)|
| pagination | Query            | False    | Pagination请求结构体       | 随机分页，默认就是按照occurTime倒序排列，用户不能指定排序字段。默认分页大小是10。见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)|



## 响应参数

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| data |    ThingModel结构体  |物模型列表。<br>物模型定义请见[ThingModel结构体](/docs/api/en/latest/model/searchmodel.html#id4) |

### ThingModel结构体

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| modelId       | String| 资产所属模型ID|
| modelIdPath   | String| 模型继承路径|
| orgId         | String| 资产所属的组织ID|
| name          | StringI18n | 模型名字|
| desc          | String| 模型描述|
| tags          | Map (Key为String，Value为String)| 用户自定义标签|
| attributes    | Map (Key为String，Value为`ThingAttribute`结构体)| 静态属性定义的map类型值，key为静态属性id，value为属性定义|
| measurepoints | Map (Key为String，Value为`ThingMeasurepoint`结构体)| 静态属性定义的map类型值，key为测点id，value为测点定义|
| services      | Map (Key为String，Value为`ThingService`结构体)     | 服务定义的map类型值，key为服务id，value为服务定义|
| events        | Map (Key为String，Value为`ThingEvent`结构体)       | 事件定义的map类型值，key为事件id，value为事件定义|


### ThingAttribute结构体

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| identifier | String| 属性id|
| dataType   | String| 数据类型。比如：ARRAY，BOOL，DATE，ENUM，INT，FLOAT，DOUBLE，STRUCT，STRING，TIMESTAMP，FILE|
| isRequired | Boolean| 是否是必须的属性。如果为true，则要求资产在实例化的时候必须设置该属性的值，否则资产在创建的时候会返回校验失败的错误|
| name       | StringI18n| 支持国际化的资产名称|
| desc       | String| 模型描述|
| tags       | Map (Key为String，Value为String)| 用户自定义标签|
| unit       | Unit结构体| 单位。见[Unit结构体](/docs/api/en/latest/model/searchmodel.html#id6)|


### Unit结构体

| 名称| 数据类型 | 描述         |
|-------------|-------------------|-----------------------------|
| unitId | String| 单位的标识符|
| multiplier   | String| 单位的乘数。参见[multiplier](/docs/api/en/latest/model/searchmodel.html#id7)|


### Multiplier

单位的乘数有如下取值：

```
YOTTA ,//Y     10^24
ZETTA ,//Z     10^21
EXA   ,//E     10^18
PETA  ,//P     10^15
TERA  ,//T     10^12
GIGA  ,//G     10^9
MEGA  ,//M     10^6
KILO  ,//k     10^3
HECTO ,//h     10^2
DECA  ,//da    10^1
ONE   ,//      10^0
DECI  ,//d     10^-1
CENTI ,//c     10^-2
MILLI ,//m     10^-3
MICRO ,//μ     10^-6
NANO  ,//n     10^-9
PICO  ,//p     10^-12
FEMTO ,//f     10^-15
ATTO  ,//a     10^-18
ZEPTO ,//z     10^-21
YOCTO ,//y     10^-24
```

## 错误码

见[公共返回码（接入服务）](/docs/api/en/latest/overview.html#id8)


## 示例

### 请求示例

```json
POST https://{apigw-address}/model-service/v2.1/thing-models?action=search
 
{
  "expression": "modelId in ( \"planet\", \"FmodelP2\"  )",
  "pagination": {
    "pageNo": 1,
"pageSize": 10
  },
  "orgId": "1ad3889266800000"
}

```


### 返回示例

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "c6594307-bc30-4380-9869-b8a88b9494de",
    "data": [
            {
                "modelId": "planet",
                "modelIdPath": "/planet",
                "orgId": "1c499110e8800000",
                "name": {
                    "defaultValue": "行星",
                    "i18nValue": {
                        "en_US": "planet"
                    }
                },
                "desc": "test",
                "tags": {},
                "attributes": {
                    "starsystem": {
                        "identifier": "starsystem",
                        "name": {
                            "defaultValue": "星系",
                            "i18nValue": {
                                "en_US": "star system"
                            }
                        },
                        "desc": "",
                        "tags": {},
                        "dataType": "STRING",
                        "unit": null,
                        "isRequired": false
                    }
                },
                "measurepoints": {
                    "temperature": {
                        "identifier": "temperature",
                        "name": {
                            "defaultValue": "temperature",
                            "i18nValue": {
                                "en_US": "temperature"
                            }
                        },
                        "desc": "temperature",
                        "tags": {},
                        "dataType": "FLOAT",
                        "hasQuality": false,
                        "signalType": "Generic",
                        "unit": {
                            "unitId": "°C",
                            "multiplier": "ONE"
                        }
                    }
                },
                "services": {
                    "speedup": {
                        "identifier": "speedup",
                        "name": {
                            "defaultValue": "speedup",
                            "i18nValue": {
                                "en_US": "speedup"
                            }
                        },
                        "desc": "t",
                        "tags": {},
                        "outputData": [
                            {
                                "identifier": "delta",
                                "name": {
                                    "defaultValue": "delta",
                                    "i18nValue": {
                                        "en_US": "delta"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": null
                            }
                        ],
                        "inputData": [
                            {
                                "identifier": "delta",
                                "name": {
                                    "defaultValue": "delta",
                                    "i18nValue": {
                                        "en_US": "delta"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": {
                                    "unitId": "rpm",
                                    "multiplier": "ONE"
                                }
                            }
                        ],
                        "callType": "ASYNC"
                    }
                },
                "events": {
                    "alert": {
                        "identifier": "alert",
                        "name": {
                            "defaultValue": "alert",
                            "i18nValue": {
                                "en_US": "alert"
                            }
                        },
                        "desc": "e",
                        "tags": {},
                        "outputData": [
                            {
                                "identifier": "event1",
                                "name": {
                                    "defaultValue": "event1",
                                    "i18nValue": {
                                        "en_US": "event1"
                                    }
                                },
                                "desc": "",
                                "tags": {},
                                "dataType": "INT",
                                "unit": null
                            }
                        ],
 						"eventType": "ERROR"
                    }
                }
            }，
{
                "modelId": "noiseSensor",
                "modelIdPath": "/noiseSensor",
                "orgId": "sysenos2018",
                "name": {
                    "defaultValue": "Noise Sensor",
                    "i18nValue": {
                        "en_US": "Noise Sensor"
                    }
                },
                "desc": "噪声传感器",
                "tags": {},
                "attributes": {},
                "measurepoints": {},
                "services": {},
                "events": {}
            }
        ],
    "pagination": {
        "pageNo": 1,
        "pageSize": 10，
		"totalSize": 2
    }
}
```

## Java SDK调用示例

```java
public class SearchThingModel {
    private static String appKey = "4ced4f38-1ced-476e0a446215-a602-4307";
    private static String appSecret = "0a446215-a602-4307-9ff2-3feed3e983ce";
    private static String orgId = "1c499110e8800000";
    private static String url = "https://{apigw-address}";
    public static void main(String[] args) {
        SearchThingModelRequest request = new SearchThingModelRequest();
        request.setOrgId(orgId);
        request.setExpression("modelId in ( \"planet\" )");
        Projection projection = new Projection();
        projection.add("modelId");
        projection.add("name.defaultValue");
        request.setProjection(projection);
        SearchThingModelResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(url)
                .getResponse(request, request.getResponseClass());
        System.out.println(response.getData());
    }
}
```
