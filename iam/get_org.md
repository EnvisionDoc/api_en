# Get Organization

Get the organization's information.

## Request Format

```
POST https://{apigw-address}/enos-iam-service/v2.0/organization/info
```

## Request Parameters (Header)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - Authorization
     - Mandatory
     - String
     - Session ID, in the format of bearer token. You can get the session ID after calling the `Log In <login>`__ API.
   * - Content-Type
     - Optional
     - String
     - The only accepted value is "application/json".


## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - id
     - Mandatory
     - String
     - The organization ID. `How to get organization ID>> </docs/api/en/2.1.0/api_faqs#how-to-get-organization-id-orgid-orgid>`__


## Response Parameters

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - organization
     - Organization Struct
     - The organization's information. For more information, see `Organization Struct >> <get_org#organization-struct-org>`

### Organization Struct <org>

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - code
     - String
     - The organization identifier, such as the business licence number.
   * - createTime
     - String
     - The time when this organizatoin is created.
   * - createdByUserId
     - String
     - The user ID of the person that created the organizatoin.
   * - description
     - String
     - The description of the organization.
   * - domain
     - String
     - The EnOS user name.
   * - id
     - String
     - The organization ID.
   * - name
     - String
     - The organization name.
   * - ownerId
     - String
     - The user ID of the organization owner.
   * - extra
     - List<JSONObejct>
     - Extra information of the organization.

## Sample

### Request Sample

```json
url: https://{apigw-address}/enos-iam-service/v2.0/organization/info
method: POST
headers:{
  "Authorization":"yourBearerToken",
  "Content-Type":"application/json"
}
requestBody: {"id":"yourOrgId"}

```

### Return Sample

```json
{
	"fail": false,
	"success": true,
	"organization": {
		"createdByUserId": "userId",
		"resourceId": "resourceId",
		"code": "",
		"approvalState": 1,
		"description": "",
		"type": 2,
		"ownerId": "userId",
		"createTime": "2018-11-20 04:03:06.0",
		"domain": "",
		"extra": {
			"owner": "ownerId",
			"property": "2",
			"approvedBy": "system",
			"scale": "0",
			"registerType": "0",
			"approvedAt": "2018-11-20 04:03:06",
			"version": "2"
		},
		"name": "Demo",
		"id": "orgId",
		"state": 0,
		"certificationState": 1
	},
	"failed": false,
	"message": "",
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
