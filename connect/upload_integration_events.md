# Upload Events

Upload the event data of a device or logic asset, including file-type data.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Write

## Request Format

```json
POST https://{apigw-address}/connect-service/v2.1/integration?action=postEvent
```

.. note:: 
  {integration-address}：The gateway address of message integration service. Log in to the EnOS Management Console and find it in **Help > Environment Information** .

## Request Parameters (URI)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_



## Request Parameters (Header)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - apim-accesstoken
     - Mandatory
     - String
     - The access token obtained via token authentication. For more information, see `Get Access Token <../token/get_access_token>`_


## Request Parameters (Body)

The format of the request body is multipart/form-data, consisting of multiple form-data sections. For a request body:

- There must only be one request message. The request message takes up the space of one form-data and its format is "request form-data". The header and body of the "request form-data" are shown in the tables below.
- There can be one or multiple file form-data. If a request body contains file data, one file takes up the space of one file form-data. Its format is "file form-data". The header of a "file form-data" is shown in the table below. If the body does not contain any file data, the body does not have to contain any file form-data.

.. list-table:: Header of the request form-data
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Content-Disposition	
     - Mandatory
     - Content-Disposition: form-data; name="enos-message"
     - ``name`` is a constant indicating the name of the request message


.. list-table:: Body of the request form-data
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - method
     - Mandatory
     - String
     - The request method.
   * - id
     - Mandatory
     - Integer
     - The request message ID.
   * - version
     - Mandatory
     - String
     - The version number.
   * - params	
     - Mandatory
     - Array of Event Structs
     - An array of Event Structs. See the table below for the structure of an Event Struct.
   * - files	
     - Mandatory
     - Map
     - The mapping between files and asset attributes. Its value is a key-value pair ``File Name`` : ``File Mapping Struct`` . See the table below for the structure of a File Mapping Struct.

.. note:: Use one of the following methods to specify the device:

   - Include the ``assetId`` in the Request 
   - Include both ``productKey`` + ``deviceKey`` in the Request 

.. list-table:: Event Struct
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - assetId 
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__
   * - productKey
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey``.
   * - deviceKey
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey``.
   * - time
     - Mandatory
     - Long
     - The timestamp of the event data.
   * - events
     - Mandatory
     - Map
     - The format is a key-value pair ``Event ID`` : ``Value``. If the ``Event ID`` is a file-type, its value would be ``local://filename``. ``local://`` is the fixed header. ``filename`` is the file name.

.. list-table:: File Mapping Struct
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - featureId
     - Mandatory
     - String
     - The event ID.
   * - assetId
     - Optional
     - String
     - The asset ID.
   * - productKey
     - Optional
     - String
     - The product key of the asset.
   * - deviceKey
     - Optional
     - String
     - The device key of the asset.
   * - md5
     - Optional
     - String
     - The MD5 of the file.

.. list-table:: Header of the file form-data
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Content-Disposition
     - Mandatory
     - Content-Disposition: form-data; name="enos-file"; filename="yourFileName"
     - Fixed parameter in the file form-data. Fields are separated by a semicolon (;). ``name`` is ``enos-file``. ``filename`` indicates file name.
   * - Content-Length
     - Mandatory
     - Long
     - The size of the file in byte.

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - code
     - Integer
     - Return code of a request.
       + ``0`` indicates success.
       + non-zero values indicates failure.
   * - msg
     - String
     - The explanation to the return code. Its value is ``OK`` if the request is successful.
   * - requestId
     - String
     - A unique ID to identify a request.





## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/integration?action=postEvent&orgId=yourOrgId
method: POST
requestHeader: 
{
  "apim-accesstoken":"yourAccessToken"
}

requestBody:
Request message form-data
Content-Disposition: form-data; name="enos-message"
{
"method": "integration.event.post",
"id": "123",
"version": "1.1",
"params":[
       {
            "productKey": "productKey1",
            "deviceKey": "deviceKey1",
            "time": 1579580182824,
            "events": {
                    "eventId1":{
                           "intParam1": 123,
                           "fileParam1":"local://filename1"
                    }
              }
       },
       {
           "assetId": "assetId2",
            "time": 1579580182824,
            "events": {                  
                     "eventId2":{
                           "intParam2": 123,
                           "fileParam2":"local://filename2"
                    } 
               }
        }
   ],
"files": {
            "filename1": {
                      "featureId": "eventId1",
                      "produckKey": "productKey1",
                      "deviceKey": "deviceKey1",
                      "md5": "0e202f9b67323d11df8a79b319a3d4f6",
              },
           "filename2": {
                      "featureId": "eventId2",
                      "assetId": "assetId2",
                      "md5": "aa8ea05bdbcbadfcda7300c65c40859f",
              }
     }
}

File form-data
Content-Disposition: form-data; name="enos-file"; filename="filename1"; 
Content-Length: 1024000
<Content of file filename1>

File form-data
Content-Disposition: form-data; name="enos-file"; filename="filename2"; 
Content-Length: 1024000
<Content of file filename2>
```

### Response Sample

```json
{
    "code":200,
    "msg":"OK",
    "requestId":"0b754708-5661-482e-8a9a-bc5916326d18",
    "data":{}
}
```

### Java SDK Sample

```java
import com.envisioniot.enos.iot_http_integration.HttpConnection;
import com.envisioniot.enos.iot_http_integration.message.IIntegrationCallback;
import com.envisioniot.enos.iot_http_integration.message.IntegrationEventPostRequest;
import com.envisioniot.enos.iot_http_integration.message.IntegrationResponse;
import com.envisioniot.enos.iot_mqtt_sdk.core.exception.EnvisionException;
import com.envisioniot.enos.sdk.data.DeviceInfo;
import com.google.common.collect.Maps;
import com.google.gson.GsonBuilder;

import java.io.File;
import java.io.IOException;
import java.util.Map;

public class EventIntegrationSample {
    // EnOS Token Server URL and HTTP Broker URL, which can be obtained from Environment Information page in EnOS Console
    static final String TOKEN_SERVER_URL = "http://token_server_url";
    static final String BROKER_URL = "http://broker_url";

    // EnOS Application AccessKey and SecretKey, which can be obtain in Application Registration page in EnOS Console
    static final String APP_KEY = "appKey";
    static final String APP_SECRET = "appSecret";

    // Device credentials, which can be obtained from Device Details page in EnOS Console
    static final String ORG_ID = "orgId";
    static final String ASSET_ID = "assetId";
    static final String PRODUCT_KEY = "productKey";
    static final String DEVICE_KEY = "deviceKey";

    private static IntegrationEventPostRequest buildEventPostRequest() {
        DeviceInfo deviceInfo1 = new DeviceInfo().setAssetId(ASSET_ID);
        DeviceInfo deviceInfo2 = new DeviceInfo().setKey(PRODUCT_KEY, DEVICE_KEY);

        // Events are defined in ThingModel
        Map<String, Map<String, Object>> hashMap = Maps.newHashMap();

        Map<String, Object> structMap = Maps.newHashMap();
        structMap.put("struct1", new File("sample1.txt"));
        structMap.put("struct2", 1234);

        hashMap.put("IntEvent1", structMap);
        return IntegrationEventPostRequest.builder()
                .addEvent(deviceInfo1, System.currentTimeMillis(), hashMap)
                .addEvent(deviceInfo2, System.currentTimeMillis(), hashMap)
                .build();
    }

    public static void main(String[] args) {
        // Construct a http connection
        HttpConnection connection = new HttpConnection.Builder(
                BROKER_URL, TOKEN_SERVER_URL, APP_KEY, APP_SECRET, ORG_ID)
                .build();

        IntegrationEventPostRequest request = buildEventPostRequest();

        try {
            IntegrationResponse response = connection.publish(request,  (bytes, length) ->
                    System.out.println(String.format("Progress: %.2f %%", (float) bytes / length * 100.0)));
            System.out.println(new GsonBuilder().setPrettyPrinting().create().toJson(response));
        } catch (EnvisionException | IOException e) {
            e.printStackTrace();
        }

        // Asynchronously call the event post with file
        request = buildEventPostRequest();

        try {
            connection.publish(request, new IIntegrationCallback() {
                        @Override
                        public void onResponse(IntegrationResponse response) {
                            System.out.println("receive response asynchronously");
                            System.out.println(new GsonBuilder().setPrettyPrinting().create().toJson(response));
                        }

                        @Override
                        public void onFailure(Exception failure) {
                            failure.printStackTrace();
                        }
                    }, (bytes, length) ->
                            System.out.println(String.format("Progress: %.2f %%", (float) bytes / length * 100.0))
            );
        } catch (IOException | EnvisionException e) {
            e.printStackTrace();
        }
    }
}
```
