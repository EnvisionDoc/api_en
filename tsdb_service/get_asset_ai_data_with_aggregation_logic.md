# Get Asset AI Data with Aggregation Logic

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取指定设备的指定测点在某段时间内的AI原始数据。

## 请求格式

```
https://{apigw-address}/tsdb-service/v2.0/ai-normalized?orgId={}&modelId={}&assetIds={}&measurepointsWithLogic={}&interval={}&startTime={}&endTime={}&pageSize={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    | 资产所属模型ID。[如何获取modelId信息](/docs/api/en/latest/api_faqs#modeid-modeid)                                                                                                                                                                                                                           |
| assetIds      | Query            | true     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs#assetid-assetid)                                                                                                                                                                                |
| measurepointsWithLogic | Query            | true     | String    | 测点数据聚合逻辑，支持的聚合计算方式有count, avg, sum, max, min, first, last。<br>聚合查询的时间区间为`[startTime,endTime)`，即聚合操作数包含`startTime`时刻的数据，但不包含`endTime`时刻的数据；<br>支持查询的测点数上限为3000。格式为：函数(测点标识符)，例如：sum(pointId)。[如何获取pointId信息](/docs/api/en/latest/api_faqs#pointid-pointid)|
| interval       | Query            | true     | Integer    | 聚合算法作用的时间间隔，有效值为0-1440，单位是分钟。当间隔为0，测点不能带聚合逻辑；当间隔值大于0，测点必须带聚合逻辑。|
| startTime     | Query            | true     | String    | 采样数据开始时间，支持UTC时间格式和local时间格式。 local时间格式为YYYY-MM-DD HH:MM:SS。当格式为本地时间时，应用按照设备所在地的当地时间进行查询。 UTC时间格式需要加入时区信息，例如：2019-06-01T00:00:00+08:00；当格式为UTC格式时，应用对所有资产按照统一的开始时间戳和结束时间戳进行查询。 |
| endTime       | Query            | true     | String    | 采样数据结束时间，格式必须与开始时间保持一致                                                                                                                                                                                                                                              |
| pageSize      | Query            | false    | Integer   | 单设备单测点单页返回记录条数的上限，默认为1000。对于单次查询，返回总数据量遵循约束: （设备数 * 点数 * pagesize）≤ 640000。                                                                                                                                                                      |
| accessKey     | Query            | true     | String    | 应用的服务账号，应用以`accessKey`进行鉴权以获得其被授权访问的数据。[如何获取accessKey信息](/docs/api/en/latest/api_faqs#accesskey-accesskey)                                                                                                           
## 请求参数（Body）
| 名称 | 位置（Path/Query） | 是否必须 | 数据类型 | 描述 |
|------|------------------|----------|-----------|-------------|
|      |                  |          |           |             |

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见[items](/docs/api/en/latest/tsdb_service/get_asset_ai_data_with_aggregation_logic.html#id3)。

### items

例子：

```
{
        "assetId": "4DXYH7nS",  			  //资产id
        "timestamp": 1560249312446,			  //UNIX数据时间戳
        "opentsdb_ai_point_xxx": "1.1236", 	 //测点标识符与测点数据
        "localtime": "2019-06-11 18:35:12"	 //数据本地时间标记
}
```

| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| localtime     | Object    | 数据本地时间标记，精确到秒，当入参时间格式为UTC格式时，该值为null。 |
| assetId       | Object    | 资产ID。                                                      |
| pointId | Object    | 此参数是变量，表示测点的标识符与数据                                    |
| timestamp     | Object    | 数据时间戳，UNIX时间，精确到秒。                                    |

## 错误码
有关错误码的描述，参见[通用错误码](overview#errorcode)。

## 示例 1

### 请求示例
Local时间格式：
```
https://{apigw-address}/tsdb-service/v2.0/ai-normalized?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepointsWithLogic=sum(opentsdb_ai_point_xxx)&interval=10&startTime=2019-06-01%2000:00:00&endTime=2019-06-11%2023:00:00&pageSize=&accessKey=accessKey
```

### 返回示例

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": null,
  "data": {
    "items": [
      {
        "sum(opentsdb_ai_point_xxx)": "4.4944",
        "assetId": "4DXYH7nS",
        "timestamp": 1560249300000,
        "localtime": "2019-06-11 18:35:00"
      },
      {
        "sum(opentsdb_ai_point_xxx)": "6.0",
        "assetId": "4DXYH7nS",
        "timestamp": 1560257100000,
        "localtime": "2019-06-11 20:45:00"
      }
    ]
  }
}
```


## 示例 2

### 请求示例
UTC时间格式：
```
https://{apigw-address}/tsdb-service/v2.0/ai-normalized?accessKey=accessKey&assetIds=4DXYH7nS&pageSize=5000&interval=10&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00&orgId=o15504722874071&measurepointsWithLogic=sum(opentsdb_ai_point_xxx)
```

### 返回示例

```json
{
    "status": 0,
    "requestId": "c1389544667049319ac1820517f6f501",
    "msg": "success",
    "submsg": null,
    "data": {
        "items": [
            {
                "localtime": null,
                "sum(opentsdb_ai_point_xxx)": "4.4944",
                "assetId": "4DXYH7nS",
                "timestamp": 1560249300000
            },
            {
                "localtime": null,
                "sum(opentsdb_ai_point_xxx)": "6.0",
                "assetId": "4DXYH7nS",
                "timestamp": 1560257100000
            }
        ]
    }
}
```

## Java SDK调用示例

```java
private static class Request extends PoseidonRequest{

    public void setQueryParam(String key, Object value){
        queryEncodeParams().put(key, value);
    }

    public void setMethod(String method) {
        this.method = method;
    }

    private String method;

    @Override
    public String baseUri() {
        return "";
    }

    @Override
    public String method() {
        return method;
    }
}


@Test
public void getAssetsAINormalizedDataTest(){
    
    //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
    String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    // Create a new request and pass the required parameters into the Query map.
    // The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("modelId", "opentsdb_model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepointsWithLogic", "sum(opentsdb_ai_point_xxx)"); //sum() is an aggregate function
    request.setQueryParam("interval", 10);
    request.setQueryParam("startTime", "2019-06-01 00:00:00"); //or in UTC format：2019-06-01T00:00:00+08:00
    request.setQueryParam("endTime", "2019-06-11 23:00:00");  //or in UTC format：2019-06-11T23:00:00+08:00
    request.setQueryParam("pageSize" , 10);
    request.setQueryParam("accessKey", appKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/ai-normalized")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
