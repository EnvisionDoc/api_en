# Get Session Information

Get the login session information after logging in to EnOS.


## Request Format

```
POST https://{apigw-address}/enos-iam-service/v2.0/session/info
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
   * - session
     - List<JSONObject>
     - The session information. For more information, see `Session Struct >> <login#session-struct-session>`__

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
url: https://{apigw-address}/enos-iam-service/v2.0/session/info
method: POST
header: {
        "Authorization":"yourBearerToken",
        "Content-Type":"application/json"
        }
```

### Return Sample

```json
{
  "fail": false,
  "session": {
    "workingOrganization": {
      "domain": "db_portal_test01",
      "name": "portal_test01",
      "id": "o15578227985571"
    },
    "expires": 7200,
    "createTime": 1562849746,
    "residentOrganization": {
      "domain": null,
      "name": "portal_test01",
      "id": "o15578227985571"
    },
    "refreshTime": 1562850052,
    "id": "IAM_S_HbH8y6sP77T5uUDgqLfzGCZkrz9x5Pyr3VMVARBBQRK8YDbAnsU9YWdUQAMkBu7g4fQKUXmPjakeSmqpFVWsANXKdrBJKUxrLxZC9MvCVHqTc5HyqTcnANz3M8HMhnTb",
    "user": {
      "guestOrganizations": null,
      "createdByUserId": "u15440200922941",
      "resourceId": "r15578227990212",
      "phoneVerified": false,
      "description": "",
      "type": 2,
      "organizationId": "o15578227985571",
      "createdAt": null,
      "emailVerified": true,
      "phoneVerifiedAt": null,
      "phone": "",
      "createTime": "2019-05-14 08:33:19.0",
      "emailVerifiedAt": null,
      "mfaType": null,
      "password_strength": "MEDIUM",
      "password_state": 0.0,
      "password_expire_time": 1.601192046E12,
      "extra": null,
      "organization": null,
      "name": "portal_test01",
      "phoneArea": "",
      "id": "u15578227990211",
      "state": 0,
      "authType": 0,
      "email": "congcong1.chen@envision-digital.com"
    }
  },
  "success": true,
  "requestId": null,
  "failed": false,
  "message": "",
  "status": 0,
  "successful": true
}
```
