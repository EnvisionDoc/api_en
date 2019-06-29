# TSDB策略服务概述

*Note: This documentation is in the progress of translation. Thanks for your visit!*

## API列表

| 操作名称                                                       | 描述 |
|---------------------------------------------------------------|------|
| [Get Points TSDB Meta Data](get_points_tsdb_meta_data)   |获取模型测点对应的TSDB存储策略，一个测点根据其数据类型及用途可有多条存储策略，该API返回指定测点在当前OU内的所有TSDB存储策略元数据|


## 通用错误码<errorcode>

| 代码 | 错误信息                      | 描述                       |
|------|---------------------------------|-----------------------------------|
| 0    | Success                         | 成功                              |
|      | xxx is required                 | 需要xxx参数                       |
|      | All asset authentication failed | 当前App对查询的所有设备都没有权限 |
|      | Invalid Argument                | 参数无效或缺失                    |
|      | [modelId] permission denied!    | modelId无效或不存在               |
| 430  |                                 | 结果集过大,服务调用失败           |
| 701  |                                 | 服务出错                          |
| 702  | xxx cannot be null or negative  | 参数xxx不可为空或者为负数         |
|      | xxx is empty                    | 参数xxx不可为空                   |
|      | only one xxx is allowed         | 参数xxx至多一个                   |
|      | param xxx is invalid            | 参数xxx无效                       |
|      | is not a valid integer          | 参数不是一个有效的整数类型        |


