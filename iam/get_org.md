# Get Organization

Get the organization information.

## Request Format

```
POST https://{apigw-address}/iam/v1/api/open/organization/get
```

## Request Parameters (URI)

| Name | Location  | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| Authorization | Header | True | String | Bearer Token   |
| Content-Type | Header |True |application/json| The content type of the returned content|

## Request Parameters (Body)

| Name | Required or Not | Data Type | Description          |
|------------------|---------------|----------|---|
| id  | True | String | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid) |


## Response Parameters

| Name  | Data Type | Description          |
|-------------|---------|----------------|
| organization |   Organization struct |    Organization information. See [Organization Struct](get_org#organization-struct-org)。 |  


### Organization Struct <org>

| Name | Data Type | Description          |
|-------------|---------------|---------------|
| code  |String |Organization identifier, such as business licence number |
| createTime   | String    | Time of creating this organizatoin    |
| createdByUserId   | String    | User ID of whom that created the organizatoin  |
| description  |String |Description of the organizatoin |
| domain  |String |User name of EnOS  |
| id  |String | Organization ID |
| name  | String| Organization name |
| ownerId   | String    | User ID of the organizatoin owner    |




## Sample

### Request Sample

```
POST https://{apigw-address}/iam/v1/api/open/organization/get
requestBody: {"id":"yourOrgId"}
header:{
        "Authorization":"yourBearerToken",
        "Content-Type":"application/json"
        }
```

### Return Sample

```json
{
  "code": 200,
  "failed": false,
  "message": "",
  "organization": {
    "code": "",
    "createTime": "2019-05-14 08:33:18.0",
    "createdByUserId": "u15440200922941",
    "description": "",
    "domain": "db_portal_test01",
    "id": "yourOrgId",
    "name": "portal_test01",
    "ownerId": "u15578227990211"
  },
  "status": 0,
  "successful": true
}
```

## Java SDK Sample

```java
public class GetOrganization{

    public static String SESSION_ID = "yourBearerToken";

    public static final String ORGANIZATIONID = "yourOrgId";

    public static void main(String[] args) {
        System.out.println("ListOrganization Test");
        OrganizationGetRequest organizationGetRequest = new OrganizationGetRequest(SESSION_ID, ORGANIZATIONID);
        OrganizationGetResponse response = getPoseidon().getResponse(organizationGetRequest, OrganizationGetResponse.class);

        System.out.println("OrganizationGetResponse res; " + JSON.toJSONString(response));
        assertNotNull("Response should not be null", response);

    }
}
```
