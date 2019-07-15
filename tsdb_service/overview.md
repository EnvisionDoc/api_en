# TSDB Data Service Overview



TSDB-based asset data service. The asset refers to the object after the model is instantiated. The asset data refers to the data sent by the measurement point of the asset. Currently, EnOS TSDB database can store the following asset data:
- Original data of AI measurement points
- Minute-level normalization data of AI measurement points
- Device status (DI) data
- Common data
- Power consumption data

For more information about TSDB storage, see [Managing Time Series Data](/docs/data-asset/en/latest/howto/storage/index.html).

For the above data types, the TSDB service provides the following interfaces for developers to invoke for data and application development.

## API List

|Operation Name                                                       | Description |
|---------------------------------------------------------------|------|
| [Get Asset Raw Data By Time Range](get_asset_raw_data_by_time_range)   |Get the original data of a specified measurement point of a specified device within a certain period (covering AI, DI and common data types)      |
| [Get Asset AI Raw Data](get_asset_ai_raw_data)   |Get the original AI data of a specified measurement point of a specified device within a certain period|
| [Get Asset AI Data with Aggregation Logic](get_asset_ai_data_with_aggregation_logic)  |Get the original AI data of a specified measurement point of a specified device within a certain period|
| [Get Asset DI Data](get_asset_di_data)  |Get the status (DI) data of a specified device within a certain period|
| [Get Asset Generic Data](get_asset_generic_data)  |Get the common data of a specified measurement point of a specified device within a certain period |
| [Get Asset Latest Data](get_asset_latest_data)           |Get the latest data of all measurement points of a specified device|
| [Filter Asset Latest Data](filter_asset_latest_data)   |Filter and query the latest data for a single measurement point on multiple devices. Numeric and String supported as the data types for query  |
| [Get Asset Current Day Electric Power](get_asset_current_day_electric_power) |Get the accumulated power consumption data of a specified device from 00:00 (local time) to current time|
| [Get Asset Electric Power Data](get_asset_electric_power_data)  |Get the status (DI) data of a specified device within a certain period      |

## Common Error Codes <errorcode>

| Code | Data Type | Error Information                                                                                              | Description                                        |
|------|-----------|---------------------------------------------------------------------------------------------------------|----------------------------------------------------|
| 0    | Integer   | Success                                                                                                 | Success                                               |
|      |           | You do not have permission for the following assets                                                     | The current application does not have access permissions to the following devices                          |
| 400  | Integer   | Exception:  Invalid param accessKey                                                                      | Error occurs with the parameter `accessKey`                                  |
|      |           | xxx is required                                                                                         | The parameter xxx cannot be null                                    |
|      |           | All asset authentication failed                                                                         | The current application does not have access permissions for all queried devices                  |
|      |           | Invalid Argument                                                                                        | Invalid or missing parameters                                     |
|      |           | [modelId] permission denied!                                                                            | Invalid or missing modelId                                |
| 430  | Integer   |                                                                                                         | The result set is too large. Failed to call the service|
| 701  | Integer   |                                                                                                         | Service error                                          |
| 702  | Integer   | Params startTime[] or endTime[] is invalid, and date format of them should be consistent                | Time format error. The local time format is YYYY-MM-DD HH:MM:SS; <br> Timezone information is required for UTC time format, e.g. 2019-06-01T00:00:00+08:00|
|      |           | xxx cannot be null or negative                                                                          | The parameter xxx cannot be null or negative                          |
|      |           | xxx is empty                                                                                            |  The parameter xxx cannot be null                                    |
|      |           | only one xxx is allowed                                                                                 | At most one parameter xxx is allowed                                    |
|      |           | assetIds size* measurement points size* pageSize is too large to query, result size may exceed RPC limit | The result set of a single query is too large                                 |
|      |           | param xxx is invalid                                                                                    |  The parameter xxx is invalid                                        |
|      |           | endTime should not be later than startTime                                                              | The query end time should be later than the start time                         |
|      |           | is not a valid integer                                                                                  | The parameter is not a valid integer                         |
|      |           | assetIds or measurement point does not match the model                                                       | Device or measurement point does not match with the model                             |
|      |           | Please config/check storage group for org[] and model[]                                                       | The storage policy is not configured or the `modelId` is incorrect                             |
