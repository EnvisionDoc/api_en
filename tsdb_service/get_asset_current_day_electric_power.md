# Get Asset Current Day Electric Power

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取指定设备从本地时间0点开始到当前时间已累计的电量数据。

## 请求格式

```
https://{apigw-address}/tsdb-service/v2.0/electric-power/current-day?orgId={}&modelId={}&assetIds={}&measurepoints={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    | 资产所属模型ID。[如何获取modelId信息](/docs/api/en/latest/api_faqs#modeid-modeid)                                                                                                                                                                                                                           |
| assetIds      | Query            | true     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs#assetid-assetid)                                                                                                                                                                                |
| measurepoints | Query            | true     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息](/docs/api/en/latest/api_faqs#pointid-pointid)                                                                                                                                                                           |
| accessKey     | Query            | true     | String    | 应用的服务账号，应用以`accessKey`进行鉴权以获得其被授权访问的数据。[如何获取accessKey信息](/docs/api/en/latest/api_faqs#accesskey-accesskey)                                                                     

## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| **items** | `List<Object>` | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见[items](/docs/api/en/latest/tsdb_service/get_asset_current_day_electric_power.html#id3)。

### items

例子：
```json
{
        "assetId": "4DXYH7nS", 						
        "timestamp": 1560329220000,				        
        "opentsdb_pi_point_xxx": "10.615000000000002" 
        "localtime": "2019-06-12 16:47:00"
}
```

| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| assetId       | Object    | 资产ID。                                             |
| pointId | Object    | 此参数是变量，表示测点的标识符与数据。 此处数据是电量pi的sum当天聚合。                                  |
| timestamp     | Object    | 数据时间戳，UNIX时间，精确到秒。                                    |
| localtime     | Object    | 数据本地时间标记，精确到秒。                                     |

## 错误码
有关错误码的描述，参见[通用错误码](overview#errorcode)。

## 示例

### 请求示例
```
https://{apigw-address}/tsdb-service/v2.0/electric-power/current-day?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_pi_point_xxx&accessKey=accessKey
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
        "assetId": "4DXYH7nS",
        "timestamp": 1560329220000,
        "sum(opentsdb_pi_point_xxx)": "10.615000000000002"
        "localtime": "2019-06-12 16:47:00"
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
public void getAssetsCurrentDayElectricPowerTest(){
    
    //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
    String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
    String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

    // Create a new request and pass the required parameters into the Query map.
    // The key is the parameter name and the value is the parameter value.
    Request request = new Request();
    request.setQueryParam("orgId", "o15504745674071");
    request.setQueryParam("modelId", "model_xxx");
    request.setQueryParam("assetIds","4DXYH7nS");
    request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");
    request.setQueryParam("accessKey", appKey);
    
    request.setMethod("GET");

    try {
        JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                .url("http://apim-gateway/tsdb-service/v2.0/electric-power/current-day")
                .getResponse(request, JSONObject.class);
        System.out.println(response);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
