# API FAQs

*Note: This documentation is in the progress of translation. Thanks for your visit!*

## 如何获取`orgId`信息<orgid>

在EnOS Console左边导航栏中点击**身份与授权 > 组织信息**。组织ID即为orgId。

## 如何获取`modeId`信息<modeid>

1. 在EnOS Console左边导航栏中点击资产树，选择目标资产树，搜索想要查询的设备名称。
2. 选择设备，点击右侧概要信息中模型名称后的“查看”，模型标识符即为`modelId`。


## 如何获取`assetId`信息<assetid>

1.	在EnOS Console左边导航栏中点击资产树，选择目标资产树，搜索想要查询的设备名称。
2.	点击设备，右侧概要信息中的“Asset ID”即为`assetId`。


## 如何获取测点（`pointId`）信息<pointid>

1.	在EnOS Console左边导航栏中点击资产树，选择目标资产树，搜索想要查询的设备名称。
2.	点击设备，右侧测点栏中的测点名称对应的标识符即为`pointId`。

## 如何获取`accessKey`信息<accesskey>

`accessKey`是EnOS分配给应用的服务账号，用于对应用进行鉴权。`accessKey`通过注册应用获取。如需获取该信息，执行以下操作：
1.	在EnOS Console左边导航栏中点击应用注册。
2.	选择需调用API的应用，查看基本信息中的“AccessKey”。

## `projection`参数如何对结果集做裁剪

`projection`参数用于对`data`结果集的裁剪，数据类型为`String Array`。其中每个String表示返回结果中需要返回的一个结果字段。没有在`projection`中指定的字段，在结果集中不返回。在指定字段时，可以使用：

|符号|描述|
|------------|--------------|
|`[*]`|	表示一个Array中的每一个对象|
|`*`  |		表示任意字段值|
|`.`	|	表示子字段|

例如有结果集：

```json
[ {
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
    "timezone": "+00:00",
    "name": {
      "i18nValue": {
"en_US": "English name ",
        "zh_CN": "Chinese name"
},
      "defaultValue": "venus!"
    },
    "attributes": {
      "system": "Solar System"
    },
    "modelIdPath": "/planet",
    "orgId": "o15444172373271",
    "desc": null,
    "tags": {}
  },
  {
    "modelId": "planet",
    "assetId": "CZ20AFJX",
    "timezone": "+00:00",
    "name": {
      "i18nValue": {
"en_US": "English name ",
        "zh_CN": "Chinese name"
},
      "defaultValue": "mars!"
    },
    "attributes": {
      "system": "Solar System"
    },
    "modelIdPath": "/planet",
    "orgId": "o15444172373271",
    "desc": null,
    "tags": {}
  }]

```

当用户只希望获取`modelId`，`assetId`和`name`中`defaultValue`字段时，可以使用这样的裁剪参数：

```json
"projection": [ "[*].modelId", "[*].assetId"，"[*].name.defaultValue"]
```

裁剪后的返回结果集为：

```json
[{
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
	"name": {
      "defaultValue": "venus!"
    }
 },
 {
    "modelId": "planet",
    "assetId": "CZ20AFJX",
	"name": {
      "defaultValue": "mars!"
    }
}]
```

## 如何使用查询表达式

API接口中支持以类SQL条件语句方式，指定查询条件，这种语句称为查询表达式。
查询表达式支持以下语法：

|查询条件     |表达式样例        |   描述|
|------------|--------------|------|
|判断一个字段是否等于一个值|`modelId = 'planet'` |`modelId`字段的值为“planet”。|
|判断一个字段的值，是否是一组值中的一个 |`modelId in ('planet', 'orbit')`| `modelId`字段的值为“planet”或“orbit”。|
|判断一个字段是否不等于一个值|`state != 3`|`state`字段的值不等于“3”。       |
|判断一个国际化名称字段是否模糊匹配一个值|`name like '逆变器'`|`name`字段中模糊匹配“逆变器”。“光伏逆变器”、“逆变器2A”都被认作是对“逆变器”的模糊匹配。|
|     	|`name.en_US like 'capacity'`	   |name字段在en_US locale下模糊匹配 “capacity”。|
|使用`and`关键字连接多个查询表达式，表示需要同时满足多个条件|`modelId = 'planet' and state = 2`|`modelId`字段的值为“planet”且`state`字段的值为“2”。 |
|使用`or`关键字连接多个查询表达式，表示满足多个条件中的至少一个 |`modelId = 'planet' or state = 2`	   |`modelId`字段的值为“planet”或`state`字段的值为“2”。|

每个API在查询表达式中能够支持的字段不同，具体请遵照各个API请求参数的说明使用。


## 国际化名称表示方法

在请求参数和返回结果中，使用国际化名称结构体表示国际化的名称。

### 国际化名称结构体

|名称     |数据类型      |   描述|
|------------|--------------|------|
|defaultValue|String |缺省的名称|
|i18nValue |Map（Key为String，Value为String）| 各个Locale下的名称，key为locale，value为各个locale下的名称。|

`defaultValue`指，当使用的`locale`未在`i18nValue`中指定时，应当采用的名称。`locale`格式遵循**Unicode locale identifier**，例如"en_US"。有关更多信息，请参阅[https://www.unicode.org/reports/tr35/tr35-55/tr35.html#BCP_47_Language_Tag_Conversion](https://www.unicode.org/reports/tr35/tr35-55/tr35.html#BCP_47_Language_Tag_Conversion).

示例：

```json
{
	"defaultValue": "Turbine",
    "i18nValue": {"zh_CN": "风机", "en_US": "Turbine"}
}
```

以上示例表示，当使用的`locale`为“zh_CN”时，名称为“风机”，当使用的`locale`为“en_US”时，名称为“Turbine”，当使用其他`locale`时，名称为“Turbine”。


## 时区表示方法

时区支持两种表示方式。
- 相对于UTC的time offset，例如“+08:00”或“-05:00”。在使用这种表示方式时，不支持夏令时。

- 遵循IANA TZ名称，例如“America / Los_Angeles”。 有关更多信息，请参阅[https://en.wikipedia.org/wiki/List_of_tz_database_time_zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)。


## API中使用的时间戳

API返回结果中的时间戳，为UTC时区的Unix时间戳，单位为毫秒。

## API中使用的时间参数

API请求参数中，以字符串方式指定时间，兼容localtime和UTC两种时间参数格式， localtime为日期时间字符串，UTC时间采用ISO8601标准格式。用户调用接口时，EnOS服务将按照约定的时间格式自动判断是localtime还是UTC时间，无需传入时区信息。

### localtime采用的日期时间格式

|数据类型|示例值|说明|
|----------|----------|---------------|
|String<br>YYYY-MM-DD HH:mm:ss|2019-04-17 10:30:00|   |
|String<br>YYYY-MM-DD HH:mm:ss.SSS|2019-04-17 10:30:00.000|仅当API支持时|

EnOS服务会根据被查询的资产上所配置的时区信息进行转换，如资产时区为UTC+0800，则2019-04-17 10:30:00 = 2019-04-17T10:30:00+0800 =  UNIX时间戳1555468200。

考虑到夏令时的问题，由调用方根据响应结果集中的timestamp自行判断和处理。

平台转换时区需要额外的性能开销，特别是对于大量数据的请求查询，可能存在响应时间较长的情况，部分接口将视性能瓶颈做适当的限制。


### UTC采用的ISO8601标准时间格式

|数据类型|示例值|
|----------|----------|
|String<br>YYYY-MM-DD'T'HH:MM:ss'Z'|2019-04-17T02:30:00Z|

请求格式为UTC格式时，EnOS服务将按照UTC不带时区进行查询，即2019-04-17T02:30:00Z= UNIX时间戳 1555468200000。


## 标签的作用与表示方法

EnOS服务支持使用标签来管理对象，可以基于标签对对象进行搜索。标签采用Map（Key为String，Value为String表示）。

## 模型路径的含义与表示方法

物模型之间可以具有继承关系，如：“双馈风机”物模型继承自“风机”物模型。API的请求参数和返回结果中使用模型路径表示模型之间的继承关系。

模型路径的数据类型为String。以“/”字符开头，同时以“/”字符连接继承路径上的各个模型Id。

例如，物模型`model_x`继承自`model_y`，`model_y`又继承自`root_model_z`，
那么`model_x`的模型路径是：“/root_model_z/model_y/model_x”
`root_model_z`的模型路径是：“/root_model_z”。


## `attributes`的表示方法

资产或设备上具有一组静态属性，在API请求参数或返回结果中这组静态属性表示为Map（Key为String，Value为String、Integer、Number、Array或Object）。其中，key为物模型中定义的属性Id，value为属性的值。value的类型参照物模型定义。

## 如何指定一个设备

在API中可以通过两种方式指定一个设备资产：
- 通过`assetId`

- 通过`productKey`与`deviceKey`

在API的请求参数中，一般会同时提供三个参数供用户指定一个设备资产。三个参数都是非必填参数，但是用户必须选择一种方式指定设备：
- 指定`assetId`
- 同时指定`productKey`与`deviceKey`

|名称|数据类型|是否必须|描述|
|---------|--------|--------|-----------|
|assetId|String|false|资产ID|
|productKey|String|false|Product key|
|deviceKey|String|false|Device key|


## 如何获取资产树ID

每一棵资产树都有一个资产树ID。用户可以在控制台“设备与资产"下的资产树管理页面，查看每棵资产树的资产树ID。用户也可以通过Search Asset Tree接口获取OU下的所有资产树。有关资产树的详细信息，请查看[资产树](/docs/device-connection/en/latest/howto/asset_tree/assettree_overview.html)。