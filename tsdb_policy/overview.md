# TSDB Policy Service Overview



## API List

|Operation Name                                                       | Description |
|---------------------------------------------------------------|------|
| [Get Points TSDB Meta Data](get_points_tsdb_meta_data)   |Get the TSDB storage policy corresponding to the model measurement point. A measurement point can have multiple storage policies, depending on its data type and usage. This API returns all the TSDB storage policy metadata in the current OU for the specified measurement point.|


## Common Error Codes <errorcode>

| Code | Error Information                      | Description                       |
|------|---------------------------------|-----------------------------------|
| 0    | Success                         | Success                              |
|      | xxx is required                 | Parameter xxx is required                       |
|      | All asset authentication failed | The current application does not have the access permissions for all queried devices |
|      | Invalid Argument                | Invalid or missing parameters                    |
|      | [modelId] permission denied!    | Invalid or missing modelId               |
| 430  |                                 | The result set is too large and the service invocation failed           |
| 701  |                                 | Service error                          |
| 702  | xxx cannot be null or negative  | Parameter xxx cannot be null or negative         |
|      | xxx is empty                    | Parameter xxx cannot be null                   |
|      | only one xxx is allowed         | At most one parameter xxx is allowed                   |
|      | param xxx is invalid            | Parameter xxx is invalid                       |
|      | is not a valid integer          | Parameter is not a valid integer        |


