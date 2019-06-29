# Get Points TSDB Meta Data

*Note: This documentation is in the progress of translation. Thanks for your visit!*

获取模型测点对应的TSDB存储策略，一个测点根据其数据类型及用途可有多条存储策略，该API返回指定测点在当前OU内的所有TSDB存储策略元数据。

## 请求格式

```
https://{apigw-address}/tsdb-service/v2.0/policies?orgId={}&modelIds={}&assetIds={}&measurepoints={}&startTime={}&endTime={}&pageSize={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)|
| modelIds       | Query            | false    | String    | 资产所属模型ID。支持多model查询，多个modelId之间用英文逗号隔开。[如何获取modelId信息](/docs/api/en/latest/api_faqs#modeid-modeid)|
| measurepoints | Query            | true     | String    | 资产测点，支持多测点查询，各个测点间用逗号隔开；支持查询的（设备数*测点数）上限为3000。[如何获取测点（pointId）信息](/docs/api/en/latest/api_faqs#pointid-pointid)                                                                                                                                                                           |
                                              


## 响应参数

| 名称  | 数据类型      | 描述               |
|-------|----------------|---------------------------|
| data | `List<Object>` | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见[items](/docs/api/en/latest/tsdb_policy/get_points_tsdb_meta_data.html#id3)。|


### items


| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| modelId     | String    | 模型ID |
| tsdb_metadata   |  `List<Object>`    | 模型测点存储策略集合，详见[policy](/docs/api/en/latest/tsdb_policy/get_points_tsdb_meta_data.html#id4)。 |

### policy

以下示例展示了一个测点opentsdb_ai_point_xxx具有AI_RAW（AI原始数据）与AI_NORMALIZED（AI分钟级归一化数据）的存储策略：

```
"opentsdb_ai_point_xxx": [                        				
          "AI_RAW", 									
          "AI_NORMALIZED"
        ]
```
| 名称        | 数据类型 | 描述                           |
|---------------|-----------|--------------------------------------|
| pointId     | Object    | 测点存储策略，一个测点可以有多个存储策略，策略用数组存储 |

## 错误码
有关错误码的描述，参见[通用错误码](overview#errorcode)。

## 示例 1

### 请求示例
不指定测点：
```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=o15504722874071&modelIds=opentsdb_model_xxx&measurepoints=
```

### 返回示例

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": "success",
  "data": [
    {
      "tsdb_metadata": {
        "opentsdb_di_point_xxx": [
          "DI"
        ],
        "opentsdb_pi_point_xxx": [
          "PI"
        ],
        "opentsdb_ai_point_xxx": [
          "AI_RAW",
          "AI_NORMALIZED"
        ],
        "opentsdb_generic_point_xxx": [
          "GENERIC"
        ]
      },
      "modelId": "opentsdb_model_xxx"
    }
  ]
}
```


## 示例 2

### 请求示例
指定测点：
```
https://{apigw-address}/tsdb-policy/v2.0/policies?orgId=o15504722874071&modelIds=opentsdb_model_xxx&measurepoints=opentsdb_di_point_xxx
```

### 返回示例

```json
{
  "status": 0,
  "requestId": null,
  "msg": "success",
  "submsg": "success",
  "data": [
    {
      "tsdb_metadata": {
        "opentsdb_di_point_xxx": [
          "DI"
        ]
      },
      "modelId": "opentsdb_model_xxx"
    }
  ]
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
  public void getPointsTSDBMetaDataTest(){
      
      //appKey and appSecret correspond to AccessKey and SecretKey in EnOS
      String appKey = "29b8d283-dddd-4c31f0e3a356-0f80-4fdf";
      String appSecret = "f0e3a856-0fc0-4fdf-b1e5-b34da152879c";

      // Create a new request and pass the required parameters into the Query map.
      // The key is the parameter name and the value is the parameter value.
      Request request = new Request();
      request.setQueryParam("orgId", "o15504745674071");
      request.setQueryParam("modelIds", "model_xxx");
      request.setQueryParam("measurepoints", "opentsdb_pi_point_xxx");

      request.setMethod("GET");

      try {
          JSONObject response =  Poseidon.config(PConfig.init().appKey(appKey).appSecret(appSecret).debug())
                  .url("http://apim-gateway/tsdb-policy/v2.0/policies")
                  .getResponse(request, JSONObject.class);
          System.out.println(response);
      } catch (Exception e) {
          e.printStackTrace();
      }
  }
```
