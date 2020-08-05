# Download File

Download a file from an asset.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Asset
     - Read

## Request Format

```json
GET https://{integration-address}/connect-service/v2.1/files?action=download
```

.. note:: 
  {integration-address}：The gateway address of message integration service. Log in to the EnOS Management Console and find it in **Help > Environment Information** .


## Request Parameters (URI)

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
   * - category
     - Query
     - Mandatory
     - String
     - The type of the file to be downloaded. The value ``feature`` stands for model definition and ``ota`` for OTA-related resources.
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetID>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`__
   * - productKey
     - Query
     - Optional (See **Note** above)
     - String
     - The product key. To be used with ``deviceKey``.
   * - deviceKey
     - Query
     - Optional (See **Note** above)
     - String
     - The device key. To be used with ``productKey``.



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




## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - The binary data stream of the file
     - output stream
     - The response will return an output stream of the returned file with the content dependent on the file.




## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/files?action=download&orgId=yourOrgId&fileUri=yourFileUri&assetId=yourAssetId&category=feature 
method: GET
requestHeader: 
{
  "apim-accesstoken":"yourAccessToken"
}
```

### Java SDK Sample

```java
import com.envisioniot.enos.iot_http_integration.FileCategory;
import com.envisioniot.enos.iot_http_integration.HttpConnection;
import com.envisioniot.enos.iot_http_integration.message.IFileCallback;
import com.envisioniot.enos.iot_mqtt_sdk.core.exception.EnvisionException;
import com.envisioniot.enos.sdk.data.DeviceInfo;

import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;

public class DownloadFileSample {
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

        DeviceInfo deviceInfo = new DeviceInfo().setAssetId(ASSET_ID);
        // fileUri is an enos scheme file uri
        String fileUri = "enos-connect://xxx.txt";

        try (ByteArrayOutputStream outputStream = new ByteArrayOutputStream()) {
            InputStream inputStream = connection.downloadFile(deviceInfo, fileUri, FileCategory.FEATURE);
            byte[] buffer = new byte[1024];
            int len;
            while ((len = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, len);
            }
            byte[] data = outputStream.toByteArray();
            System.out.println(new String(data));
        } catch (EnvisionException | IOException e) {
            e.printStackTrace();
        }

        // Asynchronously call the file download request
        try {
            connection.downloadFile(deviceInfo, fileUri, FileCategory.FEATURE, new IFileCallback() {
                @Override
                public void onResponse(InputStream inputStream) throws IOException {
                    System.out.println("download file asynchronously");
                    ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
                    byte[] buffer = new byte[1024];
                    int len;
                    while ((len = inputStream.read(buffer)) != -1) {
                        outputStream.write(buffer, 0, len);
                    }
                    byte[] data = outputStream.toByteArray();
                    System.out.println(new String(data));
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



