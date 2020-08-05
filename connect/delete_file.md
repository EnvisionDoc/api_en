# Delete File

Delete a file from an asset.

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
POST https://{integration-address}/connect-service/v2.1/files?action=delete
```

.. note:: 
  {integration-address}：The gateway address of message integration service. Log in to the EnOS Management Console and find it in **Help > Environment Information** .

## Request Parameters（URI）

.. note:: Use one of the following methods to specify the asset:

   - Include ``assetId`` in the request
   - Include ``productKey`` + ``deviceKey`` in the request

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
   * - fileUri
     - Query
     - Mandatory
     - String
     - The URI of the file. Format: ``enos-connect://xxxx``
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey`` .
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey`` .



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


## Samples

### Request Sample

```json
url: https://{integration-address}/connect-service/v2.1/files?action=delete&orgId=yourOrgId&fileUri=yourFileUri&assetId=yourAssetId
method: POST
requestHeader:
{
  "apim-accesstoken": "yourAccessToken"
}
```

### Response Sample

```json
{
"code": 0,
"msg": "OK",
"requestId": "6a02a5a5-49f0-4df1-b364-496ad2079033",
"data": {}
}
```

### Java SDK Sample

```java
import com.envisioniot.enos.iot_http_integration.HttpConnection;
import com.envisioniot.enos.iot_http_integration.message.IIntegrationCallback;
import com.envisioniot.enos.iot_http_integration.message.IntegrationResponse;
import com.envisioniot.enos.iot_mqtt_sdk.core.exception.EnvisionException;
import com.envisioniot.enos.sdk.data.DeviceInfo;
import com.google.gson.GsonBuilder;

public class DeleteFileSample {
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

    public static void main(String[] args) {
        // Construct a http connection
        HttpConnection connection = new HttpConnection.Builder(
                BROKER_URL, TOKEN_SERVER_URL, APP_KEY, APP_SECRET, ORG_ID)
            .build();

        // fileUri is an enos scheme file uri
        String fileUri = "enos-connect://xxx.txt";
        DeviceInfo deviceInfo = new DeviceInfo().setAssetId(ASSET_ID);

        try {
            IntegrationResponse response = connection.deleteFile(deviceInfo, fileUri);
            System.out.println(new GsonBuilder().setPrettyPrinting().create().toJson(response));
        } catch (EnvisionException e) {
            e.printStackTrace();
        }

        // Asynchronously call the file delete request
        try {
            connection.deleteFile(deviceInfo, fileUri, new IIntegrationCallback() {
                @Override
                public void onResponse(IntegrationResponse response) {
                    System.out.println("receive response asynchronously");
                    System.out.println(new GsonBuilder().setPrettyPrinting().create().toJson(response));
                }

                @Override
                public void onFailure(Exception failure) {
                    failure.printStackTrace();
                }
            });

        } catch (EnvisionException e) {
            e.printStackTrace();
        }
    }
}
```