# Close Active Alert

Close an active alert. A closed active alert will become a history alert.


## Request Format

```
POST https://{apigw-address}/event-service/v2.1/active-alerts?action=close
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Mandatory/Optional | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | Mandatory     | String    | The organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid)           |


## Request Parameters (Body)
| Name            | Mandatory/Optional | Data Type | Description |
|------|-----------------|-----------|-------------|
| eventId  | Mandatory | String  | The alert ID. |
| recoverTime      | Mandatory         | Long         | The recovery time in UTC format. For time formats, see [ISO8601 Standard Time Formats Used by UTC](/docs/api/en/2.1.0/api_faqs.html#iso8601-standard-time-format-adopted-by-utc-time).|
| localRecoverTime | Optional        | String       | The recovery time in local format. For time formats, see [Data and Time Formats Used by Localtime](/docs/api/en/2.1.0/api_faqs.html#date-and-time-format-adopted-by-localtime).|
| recoverReason    | Optional        | String       | The recovery reason.|



## Samples

### Request Sample

```json
url: https://{apigw-address}/event-service/v2.1/active-alerts?action=close&orgId=yourOrgId
method: POST 
requestBody:
{
  "eventId": "2019060135b6df70b2de6aa2f2eb1d09e9aa1ae7",
  "recoverTime": 1559304899404,
  "localRecoverTime": "2019-06-01 02:14:59",
  "recoverReason": "Reason",
  "action": "close"
}
```

### Return Sample

```json
{
	"code": 0,
	"msg": "OK",
	"requestId": "4873095e-621d-4cfd-bc2c-edb520f574ea",
  "data": null
}
```

### Java SDK Sample

```java
public void testCloseActiveActiveAlert() {
    String accessKey = "yourAppAccessKey";
    String secretKey = "yourAppSecretKey";
    String orgId = "yourOrgId";
    String url = "https://{apigw-address}";
    CloseActiveAlertRequest request = new CloseActiveAlertRequest();
    request.setEventId("yourEventId");
    request.setLocalRecoverTime("2019-08-19 00:00:00");
    request.setRecoverTime(System.currentTimeMillis());
    request.setOrgId(orgId);
    request.setRecoverReason("yourRecoverReason");
    try {
        CloseActiveAlertResponse response = Poseidon.config(PConfig.init().appKey(accessKey).appSecret(secretKey).debug())
            .url(url)
            .getResponse(request, CloseActiveAlertResponse.class);
        System.out.println(response);
    } catch (Exception e) {
        System.out.print(e);
    }
}
```
