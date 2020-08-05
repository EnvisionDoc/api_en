# API FAQs


## How to get Organization ID (`orgId`)  <orgid>

In the left navigation bar of the EnOS Management Console, click **IAM > Organization Profile** . The **Organization ID** is the `orgld`.

## How to get model ID (`modelId`) <modelid>

1. In the left navigation bar of the EnOS Management Console, click **Asset Tree**, select the target asset tree, and search for the device name you want to query.
2. Select the device and click **View** after the model name in the summary information on the right. The model identifier is the `modelId`.


## How to get Asset ID (`assetId`) <assetid>

1. In the left navigation bar of the EnOS Management Console, click **Asset Tree**, select the target asset tree, and search for the device name you want to query.
2. Click the device and the **Asset ID** in the **Basic Information** is the `assetId`.


## How to get the measurement point ID (`pointId`) <pointid>

1. In the left navigation bar of the EnOS Management Console, click **Asset Tree**, select the target asset tree, and search for the device name you want to query.
2. Click on the device and the identifier in the **Measurement Points** is the `pointId`.

## How to get Access Key (`accessKey`) <accesskey>

`accessKey` is the service account that EnOS assigns to the application for authentication purpose. To get the information, perform the following steps:
1. Click **Application Registration** in the left navigation bar of the EnOS Management Console.
2. Select the application that needs to invoke the API and you can get the **Access Key** in the basic information.


## How to get User ID (`userId`)

1.	Click the user profile icon in the upper right corner of EnOS Management Console.
2.	In the pop-up window, find the **User ID** of the current user, for example, `u15426865866571`.


## How does `projection` crop the result set?

The `projection` parameter is used to crop the `data` result set, and its data type is `String Array`. Each of these strings represents a result field that needs to be returned in the returned result. Any fields that are not specified in the `projection` would not be returned in the result set. When specifying a field, you can use:

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Symbol
     - Description
   * - ``[*]``
     - Stand for each object in an array
   * - ``*``
     - Stand for any field value
   * - ``.``
     - Stand for sub-field



Take the following result set for example:

```json
[ {
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
    "timezone": "+00:00",
    "name": {
      "i18nValue": {
        "en_US": "venus",
        "zh_CN": "venus"
      },
      "defaultValue": "venus"
    },
    "attributes": {
      "system": "Solar System",
      "distances" : [ {
        "towards": "sun",
        "distance": "0.72 au"
      }, {
        "towards": "jupiter",
        "distance": "5.44 au"
      } ]
    },
    "modelIdPath": "/planet",
    "orgId": "o1578468179",
    "desc": null,
    "tags": {}
  },

  {
    "modelId": "planet",
    "assetId": "CZ20AFJX",
    "timezone": "+00:00",
    "name": {
      "i18nValue": {
        "en_US": "mars",
        "zh_CN": "mars"
      },
      "defaultValue": "mars"
    },
    "attributes": {
      "system": "Solar System",
      "distances" : [ {
        "towards": "sun",
        "distance": "1.58 au"
      }, {
        "towards": "venus",
        "distance": "2.28 au"
      } ]
    },
    "modelIdPath": "/planet",
    "orgId": "o1578468179",
    "desc": null,
    "tags": {}
  }
]
```

When you only want to retrieve the `defaultValue` fields of `modelId`, `assetId`, `name`, and the `towards` field from `attributes`, use the following expression to crop your response:

```json
"projection": [ "modelId", "assetId", "name.defaultValue", "attributes.distances[*].towards"]
```

The returned result set after cropping is as follows:

```json
[{
    "modelId": "planet",
    "assetId": "TZ8AOlJU",
    "name": {
      "defaultValue": "venus"
    },
    "attributes": {
      "distances": [
        {"towards": "sun"},
        {"towards": "jupiter"}
      ]
    }
 },

 {
    "modelId": "planet",
    "assetId": "CZ20AFJX",
    "name": {
      "defaultValue": "mars"
    },
    "attributes": {
     "distances": [
       {"towards": "sun"},
       {"towards": "venus"}
     ]
   }

}]
```

## How to use expression

.. note:: All supported expression syntaxes are listed here. Each API can support different fields and syntaxes in the query expression. Please follow the instructions of each API request parameter.

The API interface supports specifying the query criteria in the way of SQL-like conditional statements. This type of statement is called a query expression.
The query expression supports the following syntax:

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Query Criterion
     - Expression Sample
     - Description
   * - For map type variables, determine whether the value of a key is the specified value, which filters key-value pairs with the specified value.
     - ``tags.{key}={value}'``
     - Use tag key-value pairs to precisely search for objects with a specified tag.
   * - Determine whether a key exists in a tag, filtering the tags with this specified key.
     - ``exists(tags.k1)``
     - There is a key of "k1" in the tags, which matches the tag whose tag key is "k1". The tag value is not considered.
   * - Determine whether a key does NOT exist in a tag, filtering the tags without this specified key.
     - ``not exists(tags.k2)``
     - The key of "k2" does not exist in the tags. It matches the tag whose tag key is NOT "k2". The tag value is not considered.
   * - Determine whether a field is equal to a value.
     - ``modelId = 'planet'``
     - The value of the ``modelId`` field is "planet".
   * - Determine whether the value of a field is one of a set of values.
     - ``modelId in ('planet', 'orbit')``
     - The value of the ``modelId`` field is "planet" or "orbit".
   * - Determine whether a field is not equal to a value.
     - ``state != 3``
     - The value of the ``state`` field is not equal to "3".
   * - Determine whether an internationalized name field fuzzy matches with a value.
     - ``name like 'inverter'``
     - The value of the ``name`` field fuzzy matches with "inverter". Both "PV Inverter" and "Inverter 2A" are considered to be a fuzzy match of "inverter".
   * - \
     - ``name.en_US like 'capacity'``
     - The value of the name field fuzzy matches with "capacity" under the en_US locale.
   * - If the ``and`` keyword is used to link multiple query expressions, it indicates that multiple criteria need to be met at the same time.
     - ``modelId = 'planet' and state = 2``
     - The value of the ``modelId`` field is "planet" and the value of the ``state`` field is "2".
   * - If the ``or`` keyword is used to link multiple query expressions, it indicates that at least one of multiple criteria needs to be met.
     - ``modelId = 'planet' or state = 2``
     - The value of the ``modelId`` field is "planet" or the value of the ``state`` field is "2".


## Internationalized name representation

In the request parameters and return results, the internationalized name structure is used to represent internationalized names.

### Internationalized name struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - defaultValue
     - String
     - Default name
   * - i18nValue
     - Map (Key is of String type and the Value is of String type)
     - The name for each locale. The key is the locale, and the value is the name for each locale.



The `defaultValue` refers to the name that should be used when the `locale` is not specified in `i18nValue`. The `locale` format follows the **Unicode locale identifier**, such as "en_US". For more information, see [https://www.unicode.org/reports/tr35/tr35-55/tr35.html#BCP_47_Language_Tag_Conversion](https://www.unicode.org/reports/tr35/tr35-55/tr35.html#BCP_47_Language_Tag_Conversion).
The current supported locales are zh_CN and en_US.

Sample:

```json
{
   "defaultValue": "Turbine",
   "i18nValue": {"zh_CN": "Turbine 1", "en_US": "Turbine A"}
}
```

The above-mentioned sample shows that when the `locale` is "zh_CN", the name is "Turbine 1"; when the `locale` is "en_US", the name is "Turbine A"; when any other `locale` is used, the name is "Turbine".


## Timezone representation

There are two timezone representation methods available.
- Time offset relative to UTC, such as "+08:00" or "-05:00". The Daylight Saving Time (DST) is not observed for this representation method.

- Follow the IANA TZ name, such as "America / Los_Angeles". For more information, see [https://en.wikipedia.org/wiki/List_of_tz_database_time_zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).


## Timestamps used in API

It refers to the timestamp in the result returned by the API. It is the Unix timestamp of the UTC timezone, represented in milliseconds.

## Time parameters used in API

In the API request parameters, the time is specified in a string format, where local time and UTC time parameter formats are supported. The localtime is a date/time string, and the UTC time uses the ISO8601 standard format. When the user invokes an interface, the EnOS service will automatically determine whether it is localtime or UTC time according to the agreed time format without the need to pass the time zone information.

### Date and time format adopted by localtime

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Data Type
     - Example Value
     - Description
   * - String
     - 2019-04-17 10:30:00
     - Format: YYYY-MM-DD HH:mm:ss
   * - String
     - 2019-04-17 10:30:00.000
     - Only when it is supported by the API. Format: YYYY-MM-DD HH:mm:ss.SSS


The EnOS service will convert the time information according to the time zone information configured on the asset being queried. For example, if the asset timezone is UTC+0800, then 2019-04-17 10:30:00 = 2019-04-17T10:30:00+0800 = UNIX timestamp 1555468200. The invoker will judge and process the DST according to the timestamp in the response result set.

The platform requires additional performance overhead for timezone conversion. Especially for request queries for large amounts of data, there may be longer response time, and some interfaces would be appropriately limited, depending on performance bottlenecks.


### ISO8601 standard time format adopted by UTC time

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Data Type
     - Example Value
     - Description
   * - String
     - 2019-04-17T02:30:00Z
     - Format: YYYY-MM-DD'T'HH:MM:ss'Z'


When the request format is UTC, the EnOS service will query as per UTC without time zone, i.e. 2019-04-17T02:30:00Z= UNIX timestamp 1555468200000.


## How to use tag

The EnOS service supports tags to manage objects, where tags can be used to search for objects. The tags use the Map struct (Both the Key and Value are of String type).

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Item
     - Descripton
   * - Key
     -
       + Use only letters, numbers, underlines, hyphens (-), and slashes (/)
       + Must be less than 50 characters
   * - Value
     -
       + Cannot start or end with space
       + Must be less than 200 characters



When updating the tags, they must be updated as a whole part. For example, an asset already has a tag "abc:123". To add a new tag "bcd:234", these 2 tags need to be passed together: {abc:123, bcd:234}.

## What is model path and how to use it

The thing models can have inheritance relationship with each other. For example, the "dual-feed turbine" thing model inherits from the "turbine" thing model. The model path is used in the API request parameters and return results to represent the inheritance relationship among models.

The data type of the model path is String. The model path starts with the "/" character and connects the individual model IDs on the inherited path with the "/" character.

For example, the thing model `model_x` inherits from `model_y`, and the `model_y` inherits from `root_model_z`.
The model path for `model_x` would therefore be: "/root_model_z/model_y/model_x"
and the model path for `root_model_z` would be: "/root_model_z".


## `attributes` representation

There is a group of static attributes on the asset or device. In the API request parameters or return results, the static attribute group is represented as Map (the Key is of String type and the Value is of String, Integer, Number, Array or Object type). The key is the attribute ID defined in the thing model, and the value is the value of the attribute. The type of the value is defined by the thing model.

## How to specify a device

In the request parameters of the API, three parameters are generally provided for the user to specify a device asset. All three parameters are optional, but the user must use one of the two ways shown below to specify the device:
- Using `assetId`
- Using `productKey` + `deviceKey`

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Mandatory/Optional
     - Description
   * - assetId
     - String
     - Optional
     - The asset ID.
   * - productKey
     - String
     - Optional
     - The product key. To be used with ``deviceKey``.
   * - deviceKey
     - String
     - Optional
     - The device key. To be used with ``productKey``.


## How to get the ID of an asset tree

Each asset tree has a Tree ID. Users can view the ID of each asset tree in the **Asset Tree** page in the console. Users can also get all asset trees under the organization through the Search Asset Tree interface. For more information on asset trees, see [Asset Trees](/docs/device-connection/en/2.1.0/howto/asset_tree/assettree_overview.html).



## How to use dataDefinition <datadef>

``dataDefinition`` is the data definition of the ``datatype`` in the structure. For example, when the ``datatype`` is "STRING", the ``dataDefinition`` defines the string length; when the ``datatype`` is "ENUM", the ``dataDefinition`` defines the value and description.


### ENUM

When the ``datatype`` is ``ENUM``, an ``enumDesc`` struct is defined in ``dataDefinition``. The key in ``enumDesc`` is the valid value of the enumeration, and the value is the internationalized description of the valid value. The ``enumType`` data type is enumeration, and can only be "INT" or "STRING" in value.

Sample

```json
{
  "enumDesc": {
    "1": {
      "defaultValue": "one",
      "i18nValue": {
        "en_US": "one",
        "zh_CN": "一"
      }
    },
    "2": {
      "defaultValue": "two",
      "i18nValue": {
        "en_US": "two",
        "zh_CN": "二"
      }
    }
  },
  "enumType": "INT",
  "defaultValue":1
}
```

### BOOL

When the ``datatype`` is ``BOOL``, a ``boolDesc`` structure is defined in ``dataDefinition``.

Sample

```json
{
"boolDesc":{
"true": "enabled",
"false": "disabled"
},
"defaultValue":true
}
```

### STRING

When the ``datatype`` is ``STRING``, a ``maxLength`` is defined in ``dataDefinition`` to specify the maximum length of the string. The maximum length of the string is 1024 bits.

Sample

```json
{
"maxLength": 1024
}
```

### STRUCT

When the ``datatype`` is ``STRUCT``, the ``dataDefinition`` defines each member in the ``struct`` as ``items``.

``items`` are separated by braces ({}) and defined with ``identifier``, ``name``, ``dataType``, ``dataDefinition``, ``unit``, and ``required``.
The ``dataType`` of the ``items`` can be any type other than ``struct``.

Sample

```json
{
"items":[
      {
        "identifier": "delta",
        "name": {
                  "defaultValue": "delta",
                  "i18nValue": {
                      "en_US": "delta"
                  }
        },
        "dataType": "INT",
        "dataDefinition":{
        },
        "unit": "rpm",
        "required":true
      }
]
}
```

### ARRAY

When the ``dataType`` is ``ARRAY``, the ``dataDefinition`` defines the data type of the array element with ``itemType``.

``itemType`` can only be "INT", "FLOAT", "DOUBLE", or "STRING".

Sample

```json
{
"itemType":"INT"
}
```

### Others

When the ``dataType`` is INT/FLOAT/DOUBLE/TIMESTAMP/DATA/FILE, ``dataDefinition`` is "null".


## Item Format Example

In TSDB Data Service APIs, you can use the ``itemFormat`` parameter to specify the displaying format of the returned device data. Available options are 0, 1, and 2. The following examples show the displaying format of the each options:

### itemFormat=0

```
{
  "code": 0,
  "msg": "OK",
  "data": {
    "items": [
      {
        "assetId": "4DXYH7nS",
        "localtime": "2019-06-11T18:35:12.123+08:00",
        "timestamp": 1560249312446,
        "power": "1.1236",
        "dataQuality": "1.1236"
      },
      {
        "assetId": "4DXYH7nS",
        "localtime": "2019-06-11T18:35:12.123+08:00",
        "timestamp": 1560249332446,
        "windspeed": "1.1236",      
        "dataQuality": "1.1236"
      }
    ]
  }
}
```

### itemFormat=1

```
{
  "code": 0,
  "msg": "OK",
  "data": {
    "items": [
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312446,
        "localtime": "2019-06-11T18:35:12.123+08:00",
        "windspeed": "1.1236",
        "power": "1.1236"
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312446,
        "localtime": "2019-06-11T18:35:12.123+08:00",
        "windspeed": "1.1236",
        "power": "1.1236"
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249312444,
        "localtime": "2019-06-11T18:35:12.123+08:00",
        "windspeed": "1.1236"
      }
    ]
  }
}
```

### itemFormat=2

```
{
   "code": 0,
   "msg": "OK",
   "submsg": " ",
   "data": {
      "items": [
         {
            "assetId": "xxx",
            "pointId": "power",
            "localTime": [
               "2020-03-09T20:29:45.222 +08:00",
               "2020-03-09T20:29:45.222 +08:00"
            ],
            "timestamp": [
               1583756985399,
               1583756985399
            ],
            "value": [
               "12.3",
               "17.8"
            ],
            "dataQuality": [
               0,
               1"
            ]
         }
      ]
   }
}
```

<!-- end -->
