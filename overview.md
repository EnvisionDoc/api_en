# About EnOS API

<br />

EnOS provides REST APIs that cover the core business processes of the system. Based on these APIs, developers can access resources within the system to develop various applications.

## API List

EnOS provides the following API services:

- [Connection Service](/docs/api/en/2.1.0/connect/overview.html): Provide device connectivity and device management on EnOS, including product and device creation and management.
- [Model Service](/docs/api/en/2.1.0/model/overview.html): Search and get the details of the models in an organization.
- [Asset Service](/docs/api/en/2.1.0/asset/overview.html): Create, manage, and update the assets in an organization.
- [Alert Service](/docs/api/en/2.1.0/event/overview.html): Search and manage asset alerts.
- [Asset Tree Service](/docs/api/en/2.1.0/asset_tree/overview.html): Create, manage, update, and search assets trees in an organization.
- [TSDB Data Service](/docs/api/en/2.1.0/tsdb_service/overview.html): Access to the stored asset data.
- [TSDB Policy Service](/docs/api/en/2.1.0/tsdb_policy/overview.html): Access to TSDB storage configuration information.
- [IAM Service Service](/docs/api/en/2.1.0/iam/overview.html): Manage user account lifecycles, authenticate user identities, and control the access rights to the resources in EnOS.
- [Application Portal Service](/docs/api/en/2.1.0/app_portal/overview.html): Get information about users, assets, and applications to configure permissions on the EnOS Application Portal.
- [Prediction Model Service](/docs/api/en/2.1.0/ml_service/overview.html): Get the prediction results of the deployed machine learning algorithm model.
- [Batch Processing Service](/docs/api/en/2.1.0/dataflow_service/index.html): Provide data integration, data development, data operation, and maintenance services that are required for big data analysis.
- [Data Federation Service](/docs/api/en/2.1.0/data_federation/overview.html): Provide data reading and data writing services for multi-source heterogeneous data storage systems.
- [Stream Processing Service](/docs/api/en/2.1.0/streaming/overview.html): Provide query and management of stream processing jobs.


## API Request

The EnOS API request consists of the following parts:

### Request URI

```
{URI-scheme}://{apigw-address}/{service-name}/{version}/{endpoint-URL}?{query-param=value}
```

- `URI-sheme`: The protocol, supporting HTTPS protocol.
- `apigw-address`: The gateway address of the API service in the environment where EnOS is deployed. Its paradigm is `apim-{domain-name}`, where `domain-name` is the name of the EnOS deployment environment.
- `service-name`: The service name, e.g. `asset-service`.
- `version`: The API version, e.g. `v2.0`.
- `endpoint-URL`: The resources and operations on resources, e.g. `assets/update`.
- `query-param`: The parameters and values for the target resource, e.g. `orgId=1234`. When there are multiple query parameters, they should be connected by `&`.

<br />

For example, to get the asset information in an organization, send the following API request:

```
GET
https://{apigw-address}/asset-service/v2.1/assets?action=get&orgId=1234&assetId=abcd
```

### Request Header

Any other fields required by the REST API specifications and HTTP specifications of the Request URI are bound in the request header.

<br />

The commonly used request header is `Content-Type`, which represents the data submission method. Generally, its value can be set to `application/json;charset=UTF-8`; if file uploading or other form submission is performed, the value is set to `Multipart/form-data;charset=UTF-8`.

### Request Body

The request body supplements the Request URI, enabling users to provide input parameters that are more complex. For example, the request body below contains parameters that specify the timezone, description, tags, and other attributes to update an asset:

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

An example of the EnOS API response in JSON format with its parameters explained is shown below:

```
{
  "code": 0,
  "msg": "OK",
  "requestId": "6cb7a013-7f83-4620-97c8-4695a892acdf",
  "data": {
  }
}
```

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - code
     - Integer
     - The API request status code. "0" means that the request is successful. For other status codes, refer to the public return codes and the error codes in the API documentation.
   * - msg
     - String
     - The explanation of the status codes. "OK" indicates a successful request. If the API request fails, the specific error information will be returned.
   * - requestId
     - String
     - The ID for each request. It is a unique identifier for an API request.
   * - data
     - Array or Object
     - The set of API response results. Data types include: basic data types, complex types, or arrays.


## Description of Public Parameters

The public parameters for each API service are described below. For how to get and use other common parameters, see [API FAQs](/docs/api/en/2.1.0/api_faqs.html)


### Pagination Request Struct

The Pagination parameter is used for random pagination. The default pagination value is 10.

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - pageNo
     - Mandatory
     - Integer
     - The request pages, starting from 1. (It starts from 0 for Application Portal service.)
   * - pageSize
     - Mandatory
     - Integer
     - The number of records in each page, which must be greater than 0.
   * - sorters
     - Optional
     - Sorter struct
     - The pagination sorting method. (Not supported in Application Portal service.)

<br />

**Sorter struct**

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - field
     - Mandatory
     - String
     - The pagination field name.
   * - order
     - Optional
     - String
     - + ASC (default) = ascending order
       + DESC = descending order

<br />

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

### Public Request Parameters (Connection Service, etc.)

The public request parameters for the connection service, model service, asset service, event service, and asset tree service APIs are as follows:

#### Projection Parameter

The ``projection`` parameter is used to crop the returned data result set. Its data type is String Array. Each of the string represents a result field that needs to be returned in the returned result. Any fields that are not specified in the projection would not be returned in the result set. When specifying a field, you can use:

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Symbol
     - Description
   * - ``[*]``
     - Stands for each object in an array
   * - ``*``
     - Stands for any field value
   * - ``.``
     - Stands for a sub-field

<br />

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

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - pagination
     - Pagination response struct
     - The pagination information for the current returned results.


### Public Response Codes (Connection Service, etc.)

.. note:: Only the common response codes are listed here. Refer to the specific API documentation for the specific response codes of each interface.

<br />

The public response codes for the connection service, model service, asset service, event service, and asset tree service APIs are:

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Code
     - Description
   * - **99400**
     - The request parameter is invalid. Check the request parameters.
   * - **99403**
     - Missing permissions. Make sure you have the permission to access the API and requested resources.
   * - **99404**
     - The specified object does not exist. For example, when getting, updating, or deleting a device, the specified ``deviceKey`` of the device does not exist.
   * - **99500**
     - Internal server error. Contact EnOS support.

<br />

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
    "msg": “Denied resource:  orgId o1558xxxxxxxxxx",
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

.. note:: Only the common response codes are listed here. Refer to the specific API documentation for the specific response codes of each interface.

<br />

The public response codes for the TSDB data service APIs are:

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 0
     - OK
     - API request is successful.
   * - 80400
     - Invalid param error
     - Invalid One or more parameters are invalid. For details, see the error message.
   * - 80401
     - Assset unauthorized
     - The SA does not have access permission to assets. Check the authorization to the application SA.
   * - 80500
     - Internal server error
     - Internal server error.


<!--end-->
