# Search Device Log

This page is under translation. Thanks for your patience.

Query the device activity log. You can also use the filtering options to limit the results to be displayed.

<!--
## Operation Permissions





.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - 
     - 
-->

## Request Format


<!--方法是POST？-->


```json
POST https://{apigw-address}/connect-service/v2.1/device-logs?action=search
```

## Request Parameters（URI）

.. list-table:: Request Parameters（URI）
   :widths: auto
   :header-rows: 1

   * - Name
     - Location（Path/Query）
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#id-orgid-orgid)
   * - startTime
     - Query
     - Mandatory
     - Timestamp
     - The lower limit of the time range of the log entries to show
   * - endTime	
     - Query
     - Mandatory
     - Timestamp
     - The upper limit of the time range of the log entries to show




## Request Parameters（Body）

<!--
1. expression不填就返回所有日志？
-->

.. list-table:: Request Parameters（Body）
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - expression
     - Optional
     - String
     - The query expression, which supports sql-like query. The fields that are supported include: ``productKey``, ``deviceKey`` and ``assetId``. The logical operators supported include ``and`` and ``or`` . Other operators supported include ``=`` and ``in`` . The [How to use expression>>](/docs/api/en/2.1.0/api_faqs.html#how-to-use-expression)
   * - pagination	
     - Optional
     - Pagination Request struct
     - Lists the paging requirements in a request. When not specified, the results are sorted in descending order by ``createTime`` by default with a pagination size of 100 pages. For more details, see `Pagination Request Struct>> </docs/api/en/2.1.0/overview.html#pagination-request-struct>`_
   * - projection
     - Optional
     - Projection Struct
     - Enables you to crop the data result set returned in the request if needed. Only the specified fields will be returned in the data result set if this parameter is used. Otherwise all fields are returned. For more details, see `How does projection crop the result set>> </docs/api/en/2.1.0/api_faqs.html#how-does-projection-crop-the-result-set>`_


## Response Parameters

.. list-table:: Response Parameters
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of deviceLog structs 
     - For the definition of a deviceLog struct, see the table below.

## DeviceLog Struct

<!--
1. content字段的内容是否需要枚举？
2. 设备行为日志结构体的英文表达是否可以用deviceLog？
-->

.. list-table:: DeviceLog Struct
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - orgId
     - String
     - The organization ID which the asset belongs to.
   * - productKey	
     - String
     - Product key of the asset
   * - deviceKey
     - String
     - Device key of the asset
   * - assetId
     - String
     - Asset ID
   * - createTime	
     - Timestamp
     - The time when the log was created
   * - code
     - Integer
     - Error code
   * - content
     - String
     - The content of the log. For example, login failure, connection lost...
   * - reason
     - String
     - Reason why the log was created. For example, login failure because the device does not exist


## Error Codes

<!--
1. 771为什么有一个说明为空白的错误码？

-->


.. list-table:: Error codes
   :widths: auto
   :header-rows: 1

   * - Name
     - Type
     - Description
   * - 200
     - success
     - Request succeeded.
   * - 719
     - Device is in mirror
     - Connection attempt failed because the device is a mirror image. 
   * - 723
     - Device is disable
     - Connection attempt failed because the device is disabled.
   * - 740
     - sub device not belong the gateway
     - Connection was rejected because the device is not connected to this gateway.
   * - 741
     - sub-device not allowed to login using direct way
     - The sub-device cannot get connected to EnOS directly without a gateway.
   * - 742
     - sign check failed
     - The device information for signing in failed to be authenticated.
   * - 745
     - the device cert is invalid
     - The device certificate is invalid.
   * - 746
     - the device must login by ssl
     - The device must get connected over SSL.
   * - 771
     - device cannot activate again
     - The device cannot be activated because it has already been activated.
   * - 770
     - dynamic activate is not allowed
     - Dynamic activation is not supported for the device.
   * - 791
     - gateway not allowed to login using in-direct way
     - A gateway device cannot be connected to EnOS Cloud as the sub-device of another gateway device.




## Samples

### Request Sample

```json
url: https://{apigw-address}/connect-service/v2.1/device-logs?action=search&startTime=1581234010022&endTime=1583826010022&orgId=o15475450989191
method: POST
requestBody:
{
    "expression":"productKey in ('H3aPZ0gd')",
    "pagination":{
        "pageNo":1,
        "pageSize":5
    }
}
```

### Response Sample

```json
{
    "code":0,
    "msg":"OK",
    "requestId":"21e4f294-824b-4eb5-913d-2ca92a230a71",
    "data":[
        {
            "orgId":"o15475450989191",
            "productKey":"H3aPZ0gd",
            "deviceKey":"SwnkrZjJ1T",
            "assetId":"JNmqyarT",
            "createTime":1583763755608,
            "code":200,
            "content":"connection lost",
            "reason":"device closed connection"
        },
        {
            "orgId":"o15475450989191",
            "productKey":"H3aPZ0gd",
            "deviceKey":"SwnkrZjJ1T",
            "assetId":"JNmqyarT",
            "createTime":1583763752780,
            "code":200,
            "content":"device login succeeded",
            "reason":"device connected"
        },
        {
            "orgId":"o15475450989191",
            "productKey":"H3aPZ0gd",
            "deviceKey":"SwnkrZjJ1T",
            "assetId":"JNmqyarT",
            "createTime":1583763730543,
            "code":200,
            "content":"connection lost",
            "reason":"device closed connection"
        },
        {
            "orgId":"o15475450989191",
            "productKey":"H3aPZ0gd",
            "deviceKey":"SwnkrZjJ1T",
            "assetId":"JNmqyarT",
            "createTime":1583763712159,
            "code":200,
            "content":"device login succeeded",
            "reason":"device connected"
        },
        {
            "orgId":"o15475450989191",
            "productKey":"H3aPZ0gd",
            "deviceKey":"SwnkrZjJ1T",
            "assetId":"JNmqyarT",
            "createTime":1583763616367,
            "code":200,
            "content":"connection lost",
            "reason":"device closed connection"
        }
    ],
    "pagination":{
        "pageNo":1,
        "pageSize":5,
        "totalSize":6
    }
}
```

## Java SDK Sample

```java
public class DeviceLogTest {
 
    private static final String appKey = "yourAppKey";
    private static final String appSecret = "yourAppSecret";
 
    private static final String serverUrl = "yourServerUrl";
 
    private static final String orgId = "yourOrgId";
 
 
    private static final Poseidon client;
 
    static {
        client = Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug()).url(serverUrl);
    }
 
    public static void main(String[] args) {
        SearchDeviceLogRequest request = new SearchDeviceLogRequest();
        request.setOrgId(orgId);
        final long now = System.currentTimeMillis();
        request.setStartTime(now - 1000L * 60 * 60 * 24 * 30);
        request.setEndTime(now);
        request.setExpression("productKey in ('H3aPZ0gd')");
        Pagination pagination = new Pagination();
        pagination.setPageSize(5);
        pagination.setPageNo(1);
        request.setPagination(pagination);
        Projection projection = new Projection();
        projection.add("assetId");
        projection.add("content");
        projection.add("code");
        projection.add("reason");
        request.setProjection(projection);
        SearchDeviceLogResponse rsp = client.getResponse(request, SearchDeviceLogResponse.class);
        System.out.println(rsp);
    }
}
```