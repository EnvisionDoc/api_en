# Get Points TSDB Meta Data

获取指定设备的指定测点在某段时间内原始数据的值（包括AI、DI、和通用数据类型）并进行应用开发。

## 请求格式

```
https://apigw-address/xxx/tsdb-service/v2.0/raw?orgId={}&modelId={}&assetIds={}&measurepoints={}&startTime={}&endTime={}&pageSize={}&accessKey={}
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述    |
|---------------|------------------|----------|-----------|------------------------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取`orgId`信息](api_faqs#如何获取`orgId`信息)                                                                                                                                                                                                                            |
| modelId       | Query            | false    | String    | 资产所属模型ID。[如何获取`modelId`信息](api_faqs#如何获取`modelId`信息)                                                                                                                                                                                                                           |
| assetIds      | Query            | true     | String    | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取`assetId`信息](api_faqs#如何获取`assetId`信息)>                                                                                                                                                                                  |
| Measurepoints | Query            | true     | String    | 资产测点，支持查询的（设备数*测点数）上限为3000。[如何获取`measurepoints`信息](api_faqs#如何获取measurepoints信息)>                                                                                                                                                                            |
| startTime     | Query            | true     | String    | 采样数据开始时间，支持UTC时间格式和local时间格式。 local时间格式为YYYY-MM-DD HH:MM:SS。当格式为本地时间时，应用按照设备所在地的当地时间进行查询。 UTC时间格式需要加入时区信息，例如：YYYY-MM-DDTHH:MM:SS+08:00；当格式为UTC格式时，应用对所有资产按照统一的开始时间戳和结束时间戳进行查询 |
| endTime       | Query            | true     | String    | 采样数据结束时间，格式必须与开始时间保持一致                                                                                                                                                                                                                                              |
| pageSize      | Query            | false    | Integer   | 每个设备每个测点的返回记录条数限制，默认值为1000。注：当前返回记录的限制为：（设备数 * 点数 * pagesize）≤ 640000。                                                                                                                                                                      |
| accessKey     | Query            | true     | String    | 应用的服务账号，应用以accessKey进行鉴权以获得其被授权访问的数据。[如何获取`accessKey`信息](api_faqs#如何获取`accessKey`信息)>                                                                                                            
## 请求参数（Body）
| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述    |
|------|------------------|----------|-----------|-------------|
|      |                  |          |           |             |

## 响应参数

| 名称  | 数据类型 | 描述  |
|-------|----------------|---------------------------|
| **items** | List\<Object> | 资产数据列表。单设备单点的返回数据按时间升序排列。其中的Object结构体中存储着参数，详见*item* |

### 示例

```
{
        "assetId": "4DXYH7nS",  			 //资产id
        "timestamp": 1560249312446,			 //UNIX数据时间戳
        "opentsdb_ai": "1.1236", 			 //测点标识符与测点数据
        "localtime": "2019-06-11 18:35:12"	 //数据本地时间标记
}
```

| 名称        | 数据类型 | 描述|
|---------------|-----------|-----------------|
| localtime     | String    | 数据本地时间标记，精确到秒，当入参时间格式为utc格式时，该值为null。 |
| assetId       | String    | 资产ID。                                                            |
| measurepoints | String    | 此参数是变量，表示测点的标识符。                                    |
| timestamp     | String    | 数据时间戳，UNIX时间，精确到秒。                                    |



## 示例 1

### 请求示例
Local时间格式：
```
https://apigw-address/xxx/tsdb-service/v2.0/raw?orgId=o15504722874071&modelId=&assetIds=4DXYH7nS&measurepoints=opentsdb_ai&startTime=2019-05-26%2010:00:00&endTime=2019-06-28%2023:00:00&pageSize=&accessKey=accessKey
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
        "timestamp": 1560249312446,
        "opentsdb_ai": "1.1236",
        "localtime": "2019-06-11 18:35:12"
      },
      {
        "assetId": "4DXYH7nS",
        "timestamp": 1560249332446,
        "opentsdb_ai": "1.1236",
        "localtime": "2019-06-11 18:35:32"
      }
    ]
  }
}
```


## 示例 2

### 请求示例
UTC时间格式：
```
https://apigw-address/xxx/tsdb-service/v2.0/raw?orgId=o15504722874071&accessKey=accessKey&modelId=opentsdb_model&assetIds=4DXYH7nS&measurepoints=opentsdb_di,opentsdb_ai,opentsdb_generic&startTime=2019-06-01T00:00:00%2B08:00&endTime=2019-06-11T23:00:00%2B08:00&pageSize=100
```

### 返回示例

```json
{
    "status": 0,
    "requestId": "f1ebd301ff7a4b7f8d53bcfe39ef264e",
    "msg": "success",
    "submsg": null,
    "data": {
        "data": [
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_ai": "1.1236",
                "timestamp": 1560249312446
            },
            {
                "localtime": null,
                "assetId": "4DXYH7nS",
                "opentsdb_ai": "1.1236",
                "timestamp": 1560249332446
            }
        ]
    }
}
```

## 示例代码

### EEOP
[comment]: <> (code block)

### APIM
[comment]: <> (code block)
