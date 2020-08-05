# Create Message

Create common messages and alert messages on the Application Portal.


## Prerequisites

- The associated application has been purchased by the organization.

- If this message is an alert about an asset, the asset or the parent node of the asset must have a tag value with "auth_unit: true".


## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.1/message/produce
```

## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - messages
     - Mandatory
     - MessageProduceDTO Struct
     - The message details.


### MessageProduceDTO Struct

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - messageId
     - Mandatory
     - String
     - The message ID.
   * - type
     - Optional
     - Integer
     - The message type.

       + 0: common message
       + 1: alert message
   * - orgId  
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId >> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__
   * - accessKey
     - Mandatory
     - String
     - The service account of the application. The application authenticates with ``accessKey`` to obtain the data that it is authorized to access. `How to get accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
   * - body
     - Optional
     - I18nString
     - Specify the message in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - color
     - Optional
     - Integer
     - The color to indicate the message severity.
   * - ring
     - Optional
     - Integer
     - The ringtone for the message.
   * - tags
     - Optional
     - Map 
     - Specify the tags in its respective locale's language. Note: only the first 3 tags will be displayed. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - produceTime
     - Mandatory
     - String
     - The time the message is produced. Format: "yyyy-MM-dd HH:mm:ss"
   * - state
     - Optional
     - Integer
     - The state of the message.

       + 0 = resolved
       + 1 = not resolved
   * - zoneOffset
     - Mandatory
     - String
     - The timezone, such as "+08:00".
   * - linkedAppId
     - Optional
     - String
     - The application ID associated with the alert message. (``linkedAppId``, ``linkedMenuCode``, and ``linkedStates`` constitute the redirection URL, such as ``https://{app-service-address}/portal/60d110ff-f388-48f4-916b-9e637d4886af/alarmProcessing?state=site%253DeVKqg4zr``, where, {App-service-address} is the service address that can display all alerts and "60d110ff-f388-48f4-916b-9e637d4886af" is the ``linkedAppId``)
   * - linkedMenuCode
     - Optional
     - String
     - The menu identifier within the application that is associated with the message. (``linkedAppId``, ``linkedMenuCode``, and ``linkedStates`` constitute the redirection URL, such as ``https://{app-service-address}/portal/60d110ff-f388-48f4-916b-9e637d4886af/alarmProcessing?state=site%253DeVKqg4zr``, where, {App-service-address} is the service address that can display all alerts and  "alarmProcessing" is the ``linkedMenuCode``)
   * - linkedStates
     - Optional
     - String
     - URL state associated with the message. (``linkedAppId``, ``linkedMenuCode``, and ``linkedStates`` constitute the redirection URL, such as ``https://{app-service-address}/portal/60d110ff-f388-48f4-916b-9e637d4886af/alarmProcessing?state=site%253DeVKqg4zr``, where, {App-service-address} is the service address that can display all alerts and "site%253DeVKqg4zr" is the ``linkedStates``)
   * - feature
     - Optional
     - StringI18n
     - Specify the description by the customer in its respective locale's language. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__
   * - assetId
     - Optional
     - String
     - The ID of the asset associated with the alert message. If the alert message is not related to an asset, there is no need to provide this.
   * - authUnitId
     - Mandatory
     - String
     - The asset tagged as "auth_unit:true" in the asset tree of the EnOS platform. The value can either be "assetId" or the parent node of the "assetId". It is the asset ID synchronized to the Application Portal to verify the permissions of an application.

        For example, there are several solar panels under a solar power station. Each solar panel has its own asset ID: assetId1, assetId2, and so on. The asset tree of this solar power station on the EnOS platform is tagged with "auth_unit:true". When the solar power station informaton is successfully synchronized to the Application Portal (the authUnitId is valid), if an organization has an application represented by the appId, the users who can view the solar power station in the Application Portal can receive the corresponding alert message. In this example, assetId is the ID of a solar panel and authUnitId is the solar power station ID.
   * - callbackUrl
     - Mandatory
     - String
     - The complete URL of the Application Portal callback (supporting URL Encode) after clicking the corresponding button of ``ActionName`` in the message window. This callback is a "GET" request. For example: ``https://{app-service-address}/callback?appId=accessKey&messageId=messagett0q22w1299`` or ``https%3a%2f%2f%7bapp-service-address%7d%2fcallback %3fappId%3daccessKey%26messageId%3dmessagett0q22w1299+``, where {app-service-address} is the server address that receive and process the callback request.
   * - actionName
     - Mandatory
     - StringI18n
     - Specify the customized text on the button in the message window in its respective locale's language. It is recommended to use two characters for Chinese and three characters for English, such as “确认” and “ACK”. If not provided, it will not be displayed. For more details on the structure and locales supported, see `Internationalized name struct </docs/api/en/2.1.0/api_faqs.html#internationalized-name-struct>`__


## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - null


## Samples

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.1/message/produce
method: POST
requestBody:
{
  "messages": [
    {
      "zoneOffset": "+08:00",
      "linkedMenuCode": "menucode",
      "linkedAppId": "accessKey",
      "color": 1,
      "ring": 1,
      "messageId": "yunfan01",
      "produceTime": "24/7/2019 11:22:01",
      "body": {
        "default": "This is a test3335",
        "en_US": "This is a test3335",
        "zh_CN": "这是个测试233335"
      },
      "type": 1,
      "tags": [
        {
          "default": "Severe",
          "en_US": "Severe",
          "zh_CN": "严重"
        },
        {
          "default": "Performance Alarm",
          "en_US": "Performance Alarm",
          "zh_CN": "性能告警"
        },
        {
          "default": "Inverter",
          "en_US": "Inverter",
          "zh_CN": "逆变器"
        }
      ],
      "orgId": "yourOrgId",
      "authUnitId": "7Uq6uP77",
      "feature": {
        "default": "This is a feature test3343",
        "en_US": "This is a feature test3343",
        "zh_CN": "这是个特征测试1"
      },
      "assetId": "7Uq6uP77",
      "accessKey": "yourAccessKey",
      "state": 0,
      "linkedStates": "states",
      "callbackUrl":"https://{app-service-address}/app-portal/test/v1/callback?appId=accessKey&messageId=messagett0q22w1299",
      "actionName":
        {
         "en_US":"ACK",
         "zh_CN":"确认"
        }
    }
  ]
}
```

### Return Sample

```json
{
  "code": 200,
  "message": "",
  "data": null
}
```
