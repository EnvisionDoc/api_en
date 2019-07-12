# About EnOS API



EnOS open the REST API interfaces that cover the core business processes of the system. Based on these interfaces, developers can access resources within the system to develop applications.

## API List

EnOS provides the following API services:

- [Connection Service](/docs/api/en/latest/connect/overview.html): The EnOS system's business capabilities in device connectivity and device management, including product and device creation and management, are opened.
- [Model Service](/docs/api/en/latest/model/overview.html): It is supported to search and get the details of the model in an organization.
- [Asset Service](/docs/api/en/latest/asset/overview.html): Provide services such as creation, management, and update of assets within an organization.
- [Alert Service](/docs/api/en/latest/event/overview.html): Provide query and management services for asset alerts. 
- [Asset Tree Service](/docs/api/en/latest/asset_tree/overview.html): Provide services such as creation, management, update and query of assets within an organization.
- [TSDB Data Service](/docs/api/en/latest/tsdb_service/overview.html): Provides the service to access to stored asset data.
- [TSDB Policy Service](/docs/api/en/latest/tsdb_policy/overview.html): Provides the service to access to TSDB storage policy configuration information.

## API Request Structure 

The EnOS API request consists of the following parts:

### Request URI

```
{URI-scheme}://{apigw-address}/{service-name}/{version}/{endpoint-URL}?{query-param=value}
```

Where:

- `URI-sheme`: protocol, where HTTPS protocol is supported.
- `apigw-address`: Address of the API service in this EnOS environment. Its paradigm is `apim-{enos-environment}.envisioniot.com`, where `enos-environment` is the name of the EnOS deployment environment.
- `service-name`: Service name, e.g.  `asset-service`.
- `version`: API version, e.g. `v2.0`.
- `endpoint-URL`: Resources and operations on resources, e.g. `assets/update`.
- `query-param`: Selection criteria for the target resource, e.g. `orgId=1234`. When there are multiple query parameters, they should be connected by using the `&` symbol.

Taking getting the information about an asset in an OU for example, the API request format is given as follows:

```
GET
https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=1234&assetId=abcd
```

### Request Header

Any other fields required by the REST API specifications and HTTP specifications of the Request URI, which are bound in the request header.

The commonly used request header is `Content-Type`, which represents the data submission method. In general, its value can be set to `application/json;charset=UTF-8`; if the file uploading or other form submission is performed , the value is set to `Multipart/form-data;charset=UTF-8`.

### Request Body

Used to supplement the Request URI to provide more complex input parameters. For example, the request body sample below contains the parameters that specify the time zone, description, tags and other attributes of the updated asset:

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

## API Response Structure

EnOS API returns the JSON structure in the following format:

```
{
  "code": 0,
  "msg": "OK",
  "requestId": "6cb7a013-7f83-4620-97c8-4695a892acdf",
  "data": {
  }
}
```

The return parameters are described in details as follows:

| Name     | Data Type        | Required or Not | Description|
| :-------- | --------------- | :------- | ------------------------------------------------------------ |
| code      | Integer         | true     | API request status code, where 0 stands for successful request. For the meanings of other status codes, refer to the public return codes and the descriptions of error codes in the API document.  |
| msg       | String          | true     | Explanation of the status codes. "OK" indicates successful request. If the API request fails, the specific error information will be returned.  |
| requestId | String          | true     | ID gotten from each request, which is used to uniquely identify an API request.                   |
| data      | Array or Object | false    | API response return result set, which includes: basic data types, complex types or arrays.  |


## Public Parameter Descriptions

The public parameters for each API service are described as follows. For how to get and use other common parameters, see [API FAQs](/docs/api/en/latest/api_faqs.html) 

### Public Request Parameters (Connection Service, etc.)

The public request parameters for the access service, model service, asset service, event service, and asset tree service API are:

#### Pagination Request Structure

The Pagination parameter stands for random pagination. The default pagination size is 10 pages.

| Name     | Data Type        | Required or Not | Description                                                         |
| -------- | ----------------- | -------- | --------------------- |
| pageNo   | Integer           | true     | Request pages, starting from 1     |
| pageSize | Integer           | true     | Number of records in each page, which must be greater than 0 |
| sorters  | Sorter Structure Array | false    | Pagination sorting method         |

**Sorter structure**

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

The Projection parameter is used to crop the returned data result set, and its data type is String Array. Each of these strings represents a result field that needs to be returned in the returned result. Any fields that are not specified in the projection would not be returned in the result set. When specifying a field, you can use:

|Symbol |Description|
|------------|--------------|
|`[*]`|	Stand for each object in an array|
|`*`  |		Stand for any field value|
|`.`	|	Stand for sub-field|


When the projection parameter is not provided, it means that the data result set is not cropped.

**Projection parameter sample**

```
{
    "projection": [
        "assetPaths”, “assets.*.assetId”
        ]
}
```

### Public Return Parameters (Connection Service, etc.)

The public return parameters for the access service, model service, asset service, event service, and asset tree service API are:

| Name     | Data Type        | Required or Not | Description                                                         |
| :--------- | -------------------- | :------- | ---------------------- |
| pagination | Pagination response structure | false    | Pagination information for the current return results |

### Public Return Codes (Connection Service, etc.)

The public return codes for the access service, model service, asset service, event service, and asset tree service API are:

| **Code**  | **Description**                                                     |
| --------- | ------------------------------------------------------------ |
| **99400** | The request parameter is illegal. Please check the request parameter.                                |
| **99403** | Missing permissions. Please check if there is the permission to access the interface and request resources.              |
| **99404** | The specified object does not exist. For example, the specified deviceKey does not exist when the specified device is gotten, updated, or deleted.  |
| **99500** | Server internal error. Please contact EnOS.                                  |

Sample:

```
99400 error sample: missing parameter
{
    "code": 99400,
    "msg": "Invalid Argument action:action is missing",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}

99400 error sample: parameter error
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

99500 error sample: internal error of server
{
    "code": 99500,
    "msg": " Internal Server Error",
    "requestId": "4d4bfd4d-b5c5-4b9c-b452-833516153b49",
    "data": null
}
```

### Public Return Codes (TSDB Data Service)

The public return code for the TSDB data service API is:

| Code | Msg / submsg                                                 | Description                                                         |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 400  | You do not have permission for the   following assets        |  The current application does not have permissions to the following devices                                    |
| 400  | Exception:  Invalid param accessKey                           | Error occurs with the parameter `accessKey`                                             |
| 400  | xxx is required                                              | The parameter xxx cannot be null                                              |
| 400  | All asset authentication failed                              | The current application does not have permissions for all devices that are queried.                             |
| 400  | Invalid Argument                                             | Invalid or missing parameters                                                |
| 400  | [modelId] permission denied                                  | [modelId] is invalid or there is no access permission                                    |
| 430  |                                                              | The request exceeds the maximum limit of network traffic within the service                                     |
| 701  |                                                              | Service error                                                     |
| 702  | Params startTime or endTime is   invalid, and date format of them should be consistent | Time format error. The local time format is YYYY-MM-DD HH:MM:SS; Timezone information is required for UTC time format, e.g. 2019-06-01T00:00:00+08:00|
| 702  | xxx cannot be null or negative  | The parameter xxx cannot be null or negative         |
| 702  | xxx is empty                                                 | The parameter xxx cannot be null                                            |
| 702  | only one xxx is allowed                                      | At most one parameter xxx is allowed                                               |
| 702  | assetIds size * measurepoints size *   pageSize is too large to query, result size may exceed RPC limit | The result set of a single query is too large, and the calculation result by using the formula "Number of Devices\*Number of Measurepoints\*pageSize" shall not be greater than 640000                                          |
| 702  | param xxx is invalid                                         | The parameter xxx is invalid                                                  |
| 702  | endTime should not be later than   startTime                 | The query end time should be later than the start time                                   |
| 702  | is not a valid integer                                       | The parameter is not a valid integer                                   |
| 702  | assetIds or measurepoint does not   match the model          | Device or measurepoint does not match with the model                                       |
| 702  | Please config/check storage group for   org[] and model[]    |  The storage policy is not configured or the `modelId` is incorrect                                  |

## API Authentication

With regard to EnOS API authentication, the service account SA (service account) is taken as the identity of an application or a developer. In the REST API request, the SA is sent to the EnOS service, which then authenticates the user and performs the required authorized access. 

### Get the Service Account

The service account SA consists of the application's `AccessKey` and `SecretKey`, which need to be generated by registering the application in the EnOS console. The specific steps are given as follows:

1. Log into the EnOS console and select **Application Registration** in the left navigation bar.
2. Click the **Create Application** button, enter the details of the new application, and click **OK**.
3. After the application registration is completed, click the application name in the **Organization Application ** tab to open the **Application Details** page to view the application's `AccessKey` and `SecretKey`.

### Authorizing Service Accounts

Only after a service account is authorized can applications be allowed to access the authorized resources on EnOS. For detailed steps on how to authorize the service accounts, see [Managing Service Accounts](/docs/iam/en/latest/howto/service_account/managing_service_account.html).

### API Operation Permissions

Before authorizing a service account, you need to create a corresponding permission policy. The resources that need to be accessed by each API interface and the corresponding operation permissions are given as follows:

| Interface Name | Required Authorization | Required Operation Permissions |
| ------------------------------ | --------------------- | ------------ |
| Get Electric Power             | Asset                 | read         |
| Get Current Day Electric Power | Asset                 | read         |
| Filter Latest Data             | Asset                 | read         |
| Get Latest Data                | Asset                 | read         |
| Get Generic Data               | Asset                 | read         |
| Get DI Data                    | Asset                 | read         |
| Get AI Normalized Data         | Asset                 | read         |
| Get AI Data                    | Asset                 | read         |
| Get Raw Data                   | Asset                 | read         |
| Get TSDB Storage Policy        | Asset                 | read         |
| UpdateAsset                    | Asset                 | Write        |
| AssociateAssetNode             | Asset Tree Management | Full-Access  |
| DeleteAssetNode                | Asset Tree Management | Full-Access  |
| CreateAssetNode                | Asset Tree Management | Full-Access  |
| Cancel Command                 | Device Management     | Full-Access  |
| Set Measurepoint               | Asset                 | Control      |
| Invoke Service                 | Asset                 | Control      |
| Create Product                 | Device Management     | Full-Access  |
| Update Product                 | Device Management     | Full-Access  |
| Delete Product                 | Device Management     | Full-Access  |
| Disable Device                 | Device Management     | Full-Access  |
| Enable Device                  | Device Management     | Full-Access  |
| Delete Device                  | Device Management     | Full-Access  |
| Create Device                  | Device Management     | Full-Access  |
| Update Device                  | Device Management     | Full-Access  |
| Add Sub-device                 | Device Management     | Full-Access  |
| Remove Sub-device              | Device Management     | Full-Access  |

For detailed steps to create a permission policy, see [Creating and Managing Policies](/docs/iam/en/latest/howto/managing_policies.html)。