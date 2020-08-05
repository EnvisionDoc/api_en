# List User Organization

List the organization to which a user belongs.

## Operation Permissions

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Required Authorization
     - Required Operation Permission
   * - orgId
     - Full Access

For more information about resources and required permissions, see [Policies, Roles and Permissions>>](/docs/enos/en/2.1.0/iam/concept/access_policy.html)

## Request Format

```
POST https://{apigw-address}/enos-iam-service/v2.0/user/organization/list
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
     - The session ID (or bearer token). You can get the session ID after calling the `Log In <login>`__ API.


## Response Parameters

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - organizations
     - Organization Struct
     - The organization's information. For more information, see `Organization Struct >> <get_org#organization-struct-org>`


## Error Code

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 30401
     - The provided bearer token is not valid.
   * - 30404
     - The session information is not found.


## Sample

### Request Sample

```
url: https://{apigw-address}/enos-iam-service/v2.0/user/organization/list
method: POST
requestBody: {"id":"yourOrgId"}
headers: {
        "Authorization":"yourBearerToken"
        }
```

### Return Sample

```json
{
	"fail": false,
	"success": true,
	"organizations": [{
		"createdByUserId": "userId1",
		"resourceId": "resourceId1",
		"code": "",
		"approvalState": 1,
		"description": "",
		"type": 2,
		"ownerId": "ownerId1",
		"createTime": "2018-11-20 04:03:06.0",
		"domain": "",
		"extra": {
			"owner": "owner1",
			"property": "2",
			"approvedBy": "system",
			"scale": "0",
			"registerType": "0",
			"approvedAt": "2018-11-20 04:03:06",
			"version": "2"
		},
		"name": "Demo",
		"id": "orgId1",
		"state": 0,
		"certificationState": 1
	}, {
		"createdByUserId": "userId2",
		"resourceId": "resourceId2",
		"code": "",
		"approvalState": 1,
		"description": "",
		"type": 2,
		"ownerId": "ownerId2",
		"createTime": "2020-04-13 04:54:51.0",
		"domain": "data_o15867536917181",
		"extra": {
			"owner": "owner2",
			"approvedBy": "system",
			"scale": "0",
			"registerType": "0",
			"approvedAt": "2020-04-13 04:55:04"
		},
		"name": "data scientist",
		"id": "orgId2",
		"state": 0,
		"certificationState": 1
	}],
	"failed": false,
	"message": "",
	"status": 0,
	"successful": true
}
```
