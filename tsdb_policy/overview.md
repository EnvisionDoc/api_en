# TSDB policy

基于TSDB的资产数据服务。资产指模型实例化后的对象，资产数据指资产的测点上送的数据。目前EnOS的TSDB数据库会存储资产的：
- AI测点原始数据
- AI测点分钟级归一化数据
- 设备状态（DI）数据
- 通用类型数据

有关TSDB存储的详细信息，参见时序数据管理。
针对以上数据类型，TSDB服务提供以下配套的接口供开发者调用获取数据并进行应用开发。

## API列表

| 操作名称                                                                     | 描述                                                                         |
|:-----------------------------------------------------------------------------|:-----------------------------------------------------------------------------|
| [Get Asset Raw Data By Time Range](get_asset_ai_raw_data)                    | 获取指定设备的指定测点在某段时间内原始数据的值（包括AI、DI、和通用数据类型） |
| [Get Asset AI Raw Data](get_asset_ai_raw_data)                               | 获取指定设备的指定测点在某段时间内的AI原始数据                               |
| [Get Asset AI Normalized Data](get_asset_ai_normalized_data)                 | 获取指定设备的指定测点在某段时间内的AI原始数据                               |
| [Get Asset Status Data](get_asset_status_data)                               | 获取指定设备在某段时间内的状态（DI）数据                                     |
| [Get Asset Generic Data](get_asset_generic_data)                             | 获取指定设备的指定测点在某段时间内通用类型的数据                             |
| [Get Asset Latest Data](get_asset_latest_data)                               | 获取指定设备所有测点的最新数据                                               |
| [Filter Asset atest Data](filter_asset_latest_data)                          | 过滤查询多个设备单个测点的最新数据。支持查询的数据类型为Numeric和String      |
| [Get Asset Current Day Electric Power](get_asset_current_day_electric_power) | 获取指定设备从本地时间0点开始到当前时间已累计的电量数据                      |
| [Get Asset Electric Power Data](get_asset_electric_power_data)               | 获取指定设备在某段时间内的电量数据                                           |

## 通用错误码

| 代码 | 数据类型 | 错误信息                                                                                            | 描述                                                                                                                |
|:-----|:---------|:----------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------|
| 0    | Integer  | Success                                                                                             | 成功                                                                                                                |
|      |          | You do not have permission for the following assets                                                 | 当前App对以下设备没有权限                                                                                           |
| 400  | Integer  | Exception: Invalid param accessKey                                                                  | 参数`accessKey`错误                                                                                                 |
|      |          | xxx is required                                                                                     | xxx参数不能为空                                                                                                     |
|      |          | All asset authentication failed                                                                     | 当前App对查询的所有设备都没有权限                                                                                   |
|      |          | Invalid Argument                                                                                    | 参数无效或缺失                                                                                                      |
|      |          | [modelId] permission denied!                                                                        | modelId无效或不存在                                                                                                 |
| 430  | Integer  |                                                                                                     | 结果集过大，服务调用失败                                                                                            |
| 701  | Integer  |                                                                                                     | 服务出错                                                                                                            |
| 702  | Integer  | Params startTime[] or endTime[] is invalid, and date format of them should be consistent            | 时间格式错误，local时间格式为YYYY-MM-DD HH:MM:SS；<br> UTC时间格式需要加入时区信息，例如：2019-06-01T00:00:00+08:00 |
|      |          | xxx cannot be null or negative                                                                      | 参数xxx不可为空或者为负数                                                                                           |
|      |          | xxx is empty                                                                                        | 参数xxx不可为空                                                                                                     |
|      |          | only one xxx is allowed                                                                             | 参数xxx至多一个                                                                                                     |
|      |          | assetIds size* measurepoints size* pageSize is too large to query, result size may exceed RPC limit | 单次查询结果集过大                                                                                                  |
|      |          | param xxx is invalid                                                                                | 参数xxx无效                                                                                                         |
|      |          | endTime should not be later than startTime                                                          | 查询结束时间应比开始时间晚                                                                                          |
|      |          | is not a valid integer                                                                              | 参数不是一个有效的整数类型                                                                                          |
|      |          | assetIds or measurepoint does not match the model                                                   | 设备或测点与模型不匹配                                                                                              |
|      |          | Please config/check storage group for org[] and model[]                                             | 未配置存储策略或`modelId`有误                                                                                       |
