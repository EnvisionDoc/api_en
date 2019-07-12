# TSDB Policy Service Overview



## API List

|Operation Name                                                       | Description |
|---------------------------------------------------------------|------|
| [Get Points TSDB Meta Data](get_points_tsdb_meta_data)   |Get the TSDB storage policy corresponding to the model measurepoint. A measurepoint may have multiple storage policies, depending on its data type and usage. This API returns all the TSDB storage policy metadata in the current OU for the specified measurepoint.|


## Common Error Codes <errorcode>

| Code | Error Information                      | Description                       |
|------|---------------------------------|-----------------------------------|
| 0    | Success                         | Success                              |
|      | xxx is required                 | The parameter xxx is required                       |
|      | All asset authentication failed | The current application does not have permissions for all devices that are queried. |
|      | Invalid Argument                | Invalid or missing parameters                    |
|      | [modelId] permission denied!    | Invalid or missing modelId               |
| 430  |                                 | The result set is too large and the service invocation failed           |
| 701  |                                 | Service error                          |
| 702  | xxx cannot be null or negative  | The parameter xxx cannot be null or negative         |
|      | xxx is empty                    | The parameter xxx cannot be null                   |
|      | only one xxx is allowed         | At most one parameter xxx is allowed                   |
|      | param xxx is invalid            | The parameter xxx is invalid                       |
|      | is not a valid integer          | The parameter is not a valid integer        |


