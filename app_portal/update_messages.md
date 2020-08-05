# Update Messages

Update the status of the message.

## Prerequisite

The associated application has been purchased by the organization.

## Request Format

```
POST https://{apigw-address}/app-portal-service/v2.1/message/update
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
     - MessageUpdateDTO Struct
     - The list of the messages that needs to be updated. 


### MessageUpdateDTO Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - messageId
     - Mandatory
     - String
     - The message ID.
   * - accessKey
     - Mandatory
     - String
     - The service account of the application. The application authenticates with ``accessKey`` to obtain the data that it is authorized to access. `How to get accessKey>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-access-key-accesskey-accesskey>`__
   * - state
     - Mandatory
     - Integer
     - The message status. 
     
       + 0: Not processed
       + 1: Processed 



## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Data Struct
     - (null)



## Sample

### Request Sample

```json
url: https://{apigw-address}/app-portal-service/v2.1/message/update
method: POST
requestBody:
{
  "messages": [
    {
      "accessKey": "yourAccessKey",
      "messageId": "TestMessage0150000927",
      "state": 1
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