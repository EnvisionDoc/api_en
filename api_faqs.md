# API FAQs


## How to get `orgId` information <orgid>

In the left navigation bar of the EnOS Console, click **Identity & Authorization > Organization Information** . The Organization ID is the orgld.

## How to get `modeId` information <modeid>

1. In the left navigation bar of the EnOS Console, click Asset Tree, select the target asset tree, and search for the device name you want to query.
2. Select the device and click "View" after the model name in the summary information on the right. The model identifier is `modelId`.


## How to get `assetId` information <assetid>

1. In the left navigation bar of the EnOS Console, click Asset Tree, select the target asset tree, and search for the device name you want to query.
2. Click on the device and the "Asset ID" in the summary information on the right is `assetId`.


## How to get the measurepoint (`pointId`) information <pointid>

1. In the left navigation bar of the EnOS Console, click Asset Tree, select the target asset tree, and search for the device name you want to query.
2. Click on the device and the identifier corresponding to the name of the measurepoint in the measurepoint column on the right is `pointId`.

## How to get `accessKey` information <accesskey>

`accessKey` is the service account that EnOS assigns to the application for authentication purpose. `accessKey` can be gotten by application registration. To get the information, perform the following steps:
1. Click **Application Registration** in the left navigation bar of the EnOS Console.
2. Select the application that needs to invoke the API and view the "AccessKey" in the basic information.

## How does `projection` crop the result set?

The `projection` parameter is used to crop the `data` result set, and its data type is `String Array`. Each of these strings represents a result field that needs to be returned in the returned result. Any fields that are not specified in the `projection` would not be returned in the result set. When specifying a field, you can use:

|Symbol |Description|
|------------|--------------|
|`[*]`|	Stand for each object in an array|
|`*`  |		Stand for any field value|
|`.`	|	Stand for sub-field|

Taking the following result set for example:

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

When you only wants to get the `defaultValue` fields of `modelId`, `assetId` and `name`, you can use such cropping parameters:

```json
"projection": [ "[*].modelId", "[*].assetId"，"[*].name.defaultValue"]
```

The returned result set after cropping is given as follows:

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

## How to use expression

The API interface supports to specify the query criteria in the way of SQL-like conditional statements. This type of statements is called a query expression.
The query expression supports the following syntax:

|Query Criterion|Expression Sample | Description|
|------------|--------------|------|
|Determine whether a field is equal to a value |`modelId = 'planet'` |The value of the `modelId` field is "planet". |
|Determine whether the value of a field is one of a set of values |`modelId in ('planet', 'orbit')`| The value of the `modelId` field is "planet" or "orbit". |
|Determine whether a field is not equal to a value |`state != 3`|The value of the `state` field is not equal to "3".        |
|Determine whether an internationalized name field is fuzzy matching with a value|`name like 'inverter' `|The value of the `name` field is fuzzy matching with "inverter". Both "PV Inverter" and "Inverter 2A" are considered to be fuzzy match of "inverter". |
| |`name.en_US like 'capacity'` |The value of the name field is fuzzy matching with "capacity" under en_US locale. |
|If the `and` keyword is used to link multiple query expressions, it indicates that multiple criteria need to be met at the same time |`modelId = 'planet' and state = 2`|The value of the `modelId` field is "planet" and the value of the `state` field is "2".  |
|If the `or` keyword is used to link multiple query expressions, it indicates that at least one of multiple criteria need to be met |`modelId = 'planet' or state = 2`|The value of the `modelId` field is "planet" or the value of the `state` field is "2". |

Each API can support different fields in the query expression. Please follow the instructions of each API request parameter.


## Internationalized name representation

In the request parameters and return results, the internationalized name structure is used to represent internationalized names.

### Internationalized name structure

| Name | Data Type | Description |
|------------|--------------|------|
|defaultValue|String |Default name|
|i18nValue |Map(Key is of String type and the Value is of String type)| Name under each Locale. The key is locale, and the value is the name under each locale. |

`defaultValue` refers to the name that should be used when the `locale` used is not specified in `i18nValue`. The `locale` format follows the **Unicode locale identifier**, such as "en_US". For more information, see [https://www.unicode.org/reports/tr35/tr35-55/tr35.html#BCP_47_Language_Tag_Conversion](https://www.unicode.org/reports/tr35/tr35-55/tr35.html#BCP_47_Language_Tag_Conversion).

Sample:

```json
{
	"defaultValue": "Turbine",
    "i18nValue": {"zh_CN": "Turbine", "en_US": "Turbine"}
}
```

The above-mentioned sample shows that, when the used `locale` is "zh_CN", the name is "Turbine"; when the used `locale` is "en_US", the name is "Turbine"; when any other `locale` is used, the name is "Turbine".


## Timezone representation

There are tow timezone representation methods available.
- Time offset relative to UTC, such as "+08:00" or "-05:00". When this representation method is used, the summer time is not supported.

- Follow the IANA TZ name, such as "America / Los_Angeles".  For more information, see [https://en.wikipedia.org/wiki/List_of_tz_database_time_zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).


## Timestamps used in API

It refers to the timestamp in the result returned by the API. It is the Unix timestamp of the UTC time zone, represented in milliseconds.

## Time parameters used in API

In the API request parameters, the time is specified in a string format, where local time and UTC time parameter formats are supported. The localtime is a date/time string, and the UTC time uses ISO8601 standard format. When the user invokes an interface, the EnOS service will automatically determine whether it is localtime or UTC time according to the agreed time format without the need to pass the time zone information.

### Date and time format adopted by localtime

|Data Type|Example Value|Description|
|----------|----------|---------------|
|String<br>YYYY-MM-DD HH:mm:ss|2019-04-17 10:30:00|   |
|String<br>YYYY-MM-DD HH:mm:ss.SSS|2019-04-17 10:30:00.000|Only when it is supported by API|

The EnOS service will convert the time information according to the time zone information configured on the asset being queried. For example, if the asset timezone is UTC+0800, then 2019-04-17 10:30:00 = 2019-04-17T10:30:00+0800 = UNIX timestamp 1555468200.

Taking into account the summer time, the invoker will judge and process it according to the timestamp in the response result set.

The platform requires additional performance overhead for timezone conversion. Especially for request queries for large amounts of data, there may be longer response time, and some interfaces would be appropriately limited, depending on performance bottlenecks.


### ISO8601 standard time format adopted by UTC time

|Data Type|Example Value|
|----------|----------|
|String<br>YYYY-MM-DD'T'HH:MM:ss'Z'|2019-04-17T02:30:00Z|

When the request format is UTC, the EnOS service will query as per UTC without time zone, i.e. 2019-04-17T02:30:00Z= UNIX timestamp 1555468200000.


## How to use tag

The EnOS service supports to use tags to manage objects, and can search for objects based on tags. The tags use the Map structure (Key is of String type and the Value is of String type).

## What is model path and how to use it

The thing models can have inheritance relationship with each other. For example, the "dual-feed turbine" thing model inherits from the "turbine" thing model. The model path is used in the API request parameters and return results to represent the inheritance relationship among models.

The data type of the model path is String. The model path starts with the "/" character and connect the individual model Ids on the inherited path with the "/" character.

For example, the thing model `model_x` inherits from `model_y`, and the `model_y` inherits from `root_model_z`.
Then, the model path for `model_x` is: "/root_model_z/model_y/model_x"
The model path for `root_model_z` is: "/root_model_z".


## `attributes` representation

There is a group of static attributes on the asset or device. In the API request parameters or return results, the static attribute group is represented as Map (Key is of String and the Value is of String, Integer, Number, Array or Object type). Where, the key is the attribute Id defined in the thing model, and the value is the value of attribute. The type of value is defined by the thing model.

## How to specify a device

There are two ways to specify a device asset in the API:
- By using `assetId`

- By using `productKey` and `deviceKey`

In the request parameters of the API, three parameters are generally provided for the user to specify a device asset. All three parameters are optional, but the user must choose one from then to specify the device:
- Specify `assetId`
- Specify both `productKey` and `deviceKey`

| Name     | Data Type        | Required or Not | Description                                                         |
|---------|--------|--------|-----------|
|assetId|String|false|Asset ID|
|productKey|String|false|Product key|
|deviceKey|String|false|Device key|


## How to get the ID of an asset tree

Each asset tree has an asset tree ID. Users can view the ID of each asset tree in the asset tree management page under Devices and Assets in the console. Users can also get all asset trees under the OU through the Search Asset Tree interface. For details about asset trees, see [Asset Trees](/docs/device-connection/en/latest/howto/asset_tree/assettree_overview.html)。