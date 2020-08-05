# Batch Update Active Alert Tags

Batch update the tag data for the specified alerts in the current alert library. The returned structure will indicate the updated results of each alert. When an update error occurs for an alert, the error information will be recorded and the remaining update process will continue.

## Request Format

```json
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=batchUpdateTags
```

## Request Parameters (URI)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the asset belongs to. `How to get orgId>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`_
   * - isPatchUpdate
     - Query
     - Mandatory
     - Boolean
     - + true (default) = Only the fields specified in the parameters are updated. The values of those fields not specified will be retained.
       + false = The fields specified in the parameters are updated. Those fields not specified will have their existing values (if any) deleted.




## Request Parameters (Body)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - eventIds
     - Mandatory
     - String Array
     - A list of the alert IDs.
   * - tags
     - Mandatory
     - Map
     - The user-defined tags to be modified. (The Key and Value are of String type.) For details, see `How to use tags>> </docs/api/en/2.1.0/api_faqs.html#how-to-use-tag>`_




## Response Parameters

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Array of EnosBatchEachData Struct
     - The list of success or failure messages. For the details of an enosBatchEachData struct, see the table below.
   * - successSize
     - Integer
     - The number of successfully updated active alerts.
   * - totalSize
     - Integer
     - The total number of active alerts to be updated.

### EnosBatchEachData Struct
| Name | Data Type     | Description          |
|-------|----------------|---------------------------|
| code | Int | Failed or succeeded to update an alert. 0: succeeded, -1: failed |
| msg | String | The message will return "OK" if successful. Otherwise it will return the error message. |
| data | null | Null |


### EnosBatchEachData Struct

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - code
     - Integer
     - Failed or succeeded to update an alert. 
        + 0: succeeded, 
        + -1: failed.
   * - msg
     - String
     - The message will return "OK" if successful. Otherwise it will return the error message.



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=batchUpdateTags&orgId=yourOrgId&isPatchUpdate=false
method: POST 
requestBody: 
{
	"eventIds":[
		"yourEventId1",
		"yourEventId2"
	],
	"tags":{
		"Tag999":"999"
	},
	"action":"batchUpdate"
}
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"4873095e-621d-4cfd-bc2c-edb520f574ea",
	"data":[
		{
			"code":0,
			"msg":"OK",
			"data":null
		},
		{
			"code":0,
			"msg":"OK",
			"data":null
		},
		{
			"code":0,
			"msg":"OK",
			"data":null
		}
	],
	"successSize":3,
	"totalSize":3
}
```

### Java SDK Sample

```java
public void testBatchUpdateActiveAlertTags() {
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";
    String orgId = "yourOrgId";
    String url = "https://{apigw-address}";
    BatchUpdateActiveAlertTagsRequest request = new BatchUpdateActiveAlertTagsRequest();
    request.setOrgId(orgId);
    List < String > list = new LinkedList < > ();
    list.add("20191105f64a4c904e59c84c9daa92da6112c7aa");
    request.setEventIds(list);

    Map < String, String > map = new HashMap < > ();
    map.put("yourTagKey", "yourTagValue");
    request.setTags(map);
    request.setIsPatchUpdate(false);
    try {
        BatchUpdateActiveAlertTagsResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, BatchUpdateActiveAlertTagsResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
