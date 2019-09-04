# About EnOS API

EnOS provides REST APIs that cover the core business processes of the system. Based on these APIs, developers can access resources within the system to develop various applications.

## API List

EnOS provides the following API services:

- [Connection Service](/docs/api/en/latest/connect/overview.html): Provide device connectivity and device management on EnOS, including product and device creation and management.
- [Model Service](/docs/api/en/latest/model/overview.html): Search and get the details of the models in an organization.
- [Asset Service](/docs/api/en/latest/asset/overview.html): Create, manage, and update the assets in an organization.
- [Alert Service](/docs/api/en/latest/event/overview.html): Search and manage asset alerts. 
- [Asset Tree Service](/docs/api/en/latest/asset_tree/overview.html): Create, manage, update, and search assets trees in an organization.
- [TSDB Data Service](/docs/api/en/latest/tsdb_service/overview.html): Access to the stored asset data.
- [TSDB Policy Service](/docs/api/en/latest/tsdb_policy/overview.html): Access to TSDB storage configuration information.
- [IAM Service Overview](/docs/api/en/latest/iam/overview.html): Manage user account lifecycle, authenticate user identities, and control the access rights to the resources in EnOS.
- [Common File Service](/docs/api/en/latest/common_file/overview.html): To access the Common File Service API documentation, click **Back to Previous Version of EnOS API** on the top-right, and select **Common File Service** from the left navigation bar.

## API Request

The EnOS API request consists of the following parts:

### Request URI

```
{URI-scheme}://{apigw-address}/{service-name}/{version}/{endpoint-URL}?{query-param=value}
```

Where:

- `URI-sheme`: protocol, supporting HTTPS protocol.
- `apigw-address`: Gateway address of the API service in the environment where EnOS is deployed. Its paradigm is `apim-{enos-environment}.{abc}.com`, where `enos-environment` is the name of the EnOS deployment environment.
- `service-name`: Service name, e.g. `asset-service`.
- `version`: API version, e.g. `v2.0`.
- `endpoint-URL`: Resources and operations on resources, e.g. `assets/update`.
- `query-param`: Parameters and values for the target resource, e.g. `orgId=1234`. When there are multiple query parameters, they should be connected by `&`.

For example, to get the asset information in an organization, send the following API request:

```
GET
https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=1234&assetId=abcd
```

### Request Header

Any other fields required by the REST API specifications and HTTP specifications of the Request URI are bound in the request header.

The commonly used request header is `Content-Type`, which represents the data submission method. Generally, its value can be set to `application/json;charset=UTF-8`; if the file uploading or other form submission is performed, the value is set to `Multipart/form-data;charset=UTF-8`.

### Request Body

Request body is used to supplement the Request URI to provide more complex input parameters. For example, the request body below contains the parameters that specify the timezone, description, tags and other attributes to update an asset:

```
POST
https://{apigw-address}/asset-service/v2.1/assets?action=update&orgId=1234&isPatchUpdate=fasle
{
  "asset": {
    "modelId": "testModel",
    "assetId": "123",
    "timezone": "+08:00",
    "description": "hahdesc",
    "tags": {
      "site": "Shanghai",
      "producer": "ABC"
    }
  }
}
```

## API Response

The response of EnOS APIs is in JSON format as follows:

```
{
  "code": 0,
  "msg": "OK",
  "requestId": "6cb7a013-7f83-4620-97c8-4695a892acdf",
  "data": {
  }
}
```

The returned parameters are described as follows:

| Name     | Data Type        | Required or Not | Description|
| :-------- | --------------- | :------- | ------------------------------------------------------------ |
| code      | Integer         | true     | API request status code. 0 stands for successful request. For other status codes, refer to the public return codes and the error codes in the API documentation. |
| msg       | String          | true     | Explanation of the status codes. "OK" indicates successful request. If the API request fails, the specific error information will be returned.  |
| requestId | String          | true     | ID for each request. It is a unique identifier for an API request.                   |
| data      | Array or Object | false    | The set of API response result. Data types include: basic data types, complex types or arrays.  |


## Description of Public Parameters

The public parameters for each API service are described as follows. For how to get and use other common parameters, see [API FAQs](/docs/api/en/latest/api_faqs.html) 

### Public Request Parameters (Connection Service, etc.)

The public request parameters for the connection service, model service, asset service, event service, and asset tree service APIs are as follows:

#### Pagination Request Struct

The Pagination parameter is used for random pagination. The default pagination value is 10.

| Name     | Data Type        | Required or Not | Description                                                         |
| -------- | ----------------- | -------- | --------------------- |
| pageNo   | Integer           | true     | Request pages, starting from 1     |
| pageSize | Integer           | true     | Number of records in each page, which must be greater than 0 |
| sorters | Sorter struct | false | Pagination sorting method |
**Sorter struct**

| Name     | Data Type        | Required or Not | Description                                                         |
| ----- | -------- | -------- | --------------------------------------------- |
| field | String   | true     | Pagination field name                                  |
| order | String   | false    | ASC means ascending order, DESC means descending order, which is set as ASC by default |

**Pagination parameter sample**

```
{
    "pagination": {
        "pageNo": 2,
        "pageSize": 100,
        "sorters": [{
            "field": "assetId",
            "order": "ASC"
        }]
    }
}
```

#### Projection Parameter

The Projection parameter is used to crop the returned data result set. Its data type is String Array. Each of the string represents a result field that needs to be returned in the returned result. Any fields that are not specified in the projection would not be returned in the result set. When specifying a field, you can use:

|Symbol |Description|
|------------|--------------|
|`[*]`|	Stands for each object in an array|
|`*`  |		Stands for any field value|
|`.`	|	Stands for sub-field|


When the projection parameter is not provided, the data result set is not cropped.

**Projection parameter sample**

```
{
    "projection": [
        "assetPaths”, “assets.*.assetId”
        ]
}
```

### Public Response Parameters (Connection Service, etc.)

The public response parameters for the connection service, model service, asset service, event service, and asset tree service APIs are:

| Name     | Data Type        | Required or Not | Description                                                         |
| :--------- | -------------------- | :------- | ---------------------- |
| pagination | Pagination response struct | false    | Pagination information for the current returned results |

### Public Response Codes (Connection Service, etc.)

The public response codes for the connection service, model service, asset service, event service, and asset tree service APIs are:

| Code | Description                                                     |
| --------- | ------------------------------------------------------------ |
| **99400** | The request parameter is invalid. Check the request parameters.                     |
| **99403** | Missing permissions. Make sure you have the permission to access the API and requested resources.            |
| **99404** | The specified object does not exist. For example, when getting, updating, or deleting a device, the specified deviceKey of the device does not exist. |
| **99500** | Server internal error. Contact EnOS support.                          |

Sample:

```
99400 error sample: missing parameter
{
    "code": 99400,
    "msg": "Invalid Argument action:action is missing",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99400 error sample: Invalid parameter
{
    "code": 99400,
    "msg": "Invalid Argument orgId:  orgId does not exist",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99403 error sample: missing permissions 
{
    "code": 99403,
    "msg": “Denied resource:  orgId o15589291276361",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99500 error sample: internal server error
{
    "code": 99500,
    "msg": " Internal Server Error",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}
```

### Public Response Codes (TSDB Data Service)

The public response codes for the TSDB data service APIs are:

| Code | Message                                                      | Description                                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 400  | You do not have permission for the following assets          | The current application does not have permissions to the following assets. |
| 400  | Exception:  Invalid param accessKey                          | Invalid parameter `accessKey`.                               |
| 400  | xxx is required                                              | The value of parameter xxx cannot be null.                   |
| 400  | All asset authentication failed                              | The current application does not have permissions for all devices that are queried. |
| 400  | Invalid Argument                                             | Invalid or missing parameters.                               |
| 400  | [modelId] permission denied                                  | [modelId] is invalid or has no access permission.            |
| 430  |                                                              | The request exceeds the maximum limit of network traffic within the service. |
| 701  |                                                              | Service error.                                               |
| 702  | Params startTime or endTime is   invalid, and date format of them should be consistent | Time format error. The local time format is YYYY-MM-DD HH:MM:SS; Timezone information is required for UTC time format, e.g. 2019-06-01T00:00:00+08:00. |
| 702  | xxx cannot be null or negative                               | The value of parameter xxx cannot be null or negative.       |
| 702  | xxx is empty                                                 | The value of parameter xxx cannot be null or negative.       |
| 702  | only one xxx is allowed                                      | At most one parameter xxx is allowed.                        |
| 702  | assetIds size * measurement points size * pageSize is too large to query, result size may exceed RPC limit | The result set of a single query is too large. The calculation result by using the formula "Number of Devices\*Number of Measuring points\*pageSize" cannot be greater than 640,000. |
| 702  | param xxx is invalid                                         | The parameter xxx is invalid.                                |
| 702  | endTime should not be later than   startTime                 | The query end time should be later than the start time.      |
| 702  | is not a valid integer                                       | The parameter is not a valid integer.                        |
| 702  | assetIds or measurement point does not   match the model     | Device or measuring point does not match with the model.     |
| 702  | Please config/check storage group for   org[] and model[]    | The storage policy is not configured or the `modelId` is incorrect. |

