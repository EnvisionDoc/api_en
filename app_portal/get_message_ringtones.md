# Get Message Ringtones

Get the list of ringtones for configuring the message.

## Request Format

```
GET https://{apigw-address}/app-portal-service/v2.0/message/enum/ringtones
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
     - The list of ringtones for the message.


### Data Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - ringings
     - Ringing Struct
     - The details of the ringtones for the message.


### Ringing Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - Integer
     - The ringtone ID.
   * - name
     - StringI18n
     - Specify the ringtone name in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__


## Samples

### Request Sample

```
url: https://{apigw-address}/app-portal-service/v2.0/message/enum/ringtones
method: GET
```

### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": {
    "ringings": [
      {
        "id": 0,
        "name": {
          "default": "No Sound",
          "en_US": "No Sound",
          "zh_CN": "无声音"
        }
      },
      {
        "id": 1,
        "name": {
          "default": "Alarm Sound",
          "en_US": "Alarm Sound",
          "zh_CN": "警报声"
        }
      }
    ]
  }
}
```