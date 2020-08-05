# Get Colors of the Message Icon

Get the list of colors for configuring the message icon.


## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.0/message/enum/colors
```

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - The list of colors.

### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - colors
     - Color Struct
     - The details of the colors.


### Color Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - Integer
     - The color ID.
   * - name
     - StringI18n
     - Specify the color name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__



## Sample

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/message/enum/colors
method: GET
```

### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": {
    "colors": [
      {
        "id": 0,
        "name": {
          "default": "red",
          "en_US": "red",
          "zh_CN": "红色"
        }
      },
      {
        "id": 1,
        "name": {
          "default": "Yellow ",
          "en_US": "Yellow ",
          "zh_CN": "黄色"
        }
      },
      {
        "id": 2,
        "name": {
          "default": "Gray",
          "en_US": "Gray",
          "zh_CN": "灰色"
        }
      }
    ]
  }
}
```
