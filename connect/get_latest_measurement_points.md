# Get Latest Measurement Points

Obtain the latest measurement point data uploaded from a device, including raw data, mirrored data, excluding data calculated by StreamSet or from offline message integration.

The latest measurement point data can be uploaded over HTTP, MQTT, CoAP. Data uploaded by using the API of the older version (/connectService/products/{productKey}/devices/measurepoints) can also be obtained by using this API.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - Device Management
     - Read

## Request Format

```
POST https://{apigw-address}/connect-service/v2.1/measurepoints?action=queryLatest
```

## Request Parameters (URI)

.. note:: Use one of the following methods to specify the device:

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
   * - assetId
     - Query
     - Optional (See **Note** above)
     - String
     - The asset ID. `How to get assetId>> </docs/api/en/2.1.0/api_faqs.html#how-to-get-asset-id-assetid-assetid>`_
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

## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - measurepointIds
     - Optional
     - String Array
     - An array that consists of measurement point IDs, used to specify the measurement points to be included in the response. If not specified, the latest value of all measurement points will be returned.

## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of MeasurepointStatus Structs
     - Details of the measurement point data. See the table below for the structure of MeasurepointStatus struct.


### MeasurepointStatus Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The measurement point ID.
   * - time
     - String
     - The time when the measurement point is updated.
   * - value
     - Depending on the definition of the measurement point
     - The value of the measurement point.



## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/measurepoints?action=queryLatest&orgId=yourOrgId&assetId=yourAssetId
method: POST
requestBody:
{
	"measurepointIds":[
		"temp"
	]
}
```
### Response Sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "5c48cad3-3e33-4e0e-be43-9ca628ba3ae5",
    "data": [
        {
            "id": "temp",
            "time": "1579590343468",
            "value": 0.3084426
        }
    ]
}

```

### Java SDK Sample

```java
package com.envisioniot.enos.api.sample.connect_service.device;

import com.envision.apim.poseidon.config.PConfig;
import com.envision.apim.poseidon.core.Poseidon;
import com.envisioniot.enos.connect_service.v2_1.measurepoints.QueryLatestMeasurepointsRequest;
import com.envisioniot.enos.connect_service.v2_1.measurepoints.QueryLatestMeasurepointsResponse;
import com.google.common.collect.ImmutableList;

public class GetLatestMeasurementPoints {

    public static void main(String[] args) {
        String appKey = "yourAppKey";
        String appSecret = "yourAppSecret";
        String serverUrl = "yourServerUrl";

        String orgId = "yourOrgId";
        String assetId = "yourAssetId";

        QueryLatestMeasurepointsRequest request = new QueryLatestMeasurepointsRequest();
        request.setOrgId(orgId);
        request.setAssetId(assetId);
        request.setMeasurepointIds(ImmutableList.of("temp"));
        QueryLatestMeasurepointsResponse response = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url(serverUrl)
                .getResponse(request, QueryLatestMeasurepointsResponse.class);
    }
}
```
