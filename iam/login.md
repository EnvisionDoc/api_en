# Log In

Log in to EnOS.

## Request Format

```
POST https://{apigw-address}/enos-iam-service/v2.0/login
```

## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - authType
     - Mandatory
     - Enum
     - The authentication type. 
     
       + 0: EnOS
       + 1: LDAP
   * - linkName
     - Optional (Mandatory if using LDAP ``authType``)
     - String
     - The LDAP domain name.
   * - principal
     - Mandatory
     - String
     - The account name.
   * - credentials
     - Mandatory
     - String
     - The password.
   * - keyId
     - Optional
     - String
     - The encryption key ID.
   * - captcha
     - Optional
     - String
     - The captcha, which is a reserved field.
   * - clientIp
     - Optional
     - String
     - The IP address of the client.
   * - expireInterval
     - Optional
     - Integer
     - The session expiring time, in seconds.

## Response Parameters

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - captcha
     - String
     - The captcha for verification.
   * - session
     - List<JSONObject>
     - The session information. For more information, see `Session Struct >> <login#session-struct-session>`__

### Session Struct <session>

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The session ID.
   * - expires
     - Integer
     - The session expiring time.
   * - user
     - List<JSONObject>
     - The detailed user information. For more information, see `User Struct >> <login#user-struct-user>`__
   * - residentOrganization
     - List<JSONObject>
     - The organization to which the user belongs when the user account is created.
   * - workingOrganization
     - List<JSONObject>
     - The current organizatoin.
   * - refreshTime
     - Long
     - The session refresh time.
   * - createTime
     - Long
     - The session create time.


### User Struct <user>

.. list-table::
   :widths: 30 30 40
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - id
     - String
     - The user ID.
   * - organizationId
     - String
     - The organization to which the user belongs.
   * - authType
     - Enum
     - The authentication type. 
     
       + 0: EnOS
       + 1: LDAP
   * - name
     - String
     - The user name.
   * - phone
     - String
     - The user phone number.
   * - phoneVerifiedAt
     - String
     - The time when the user phone number is verified.
   * - email
     - String
     - The user email address.
   * - emailVerifiedAt
     - String
     - The time when the user email is verified.
   * - description
     - String
     - The user description.
   * - extra
     - Map
     - Other user information.
   * - resourceId
     - String
     - The resource ID.
   * - type
     - Enum
     - The user type.
     
       + 0: user
       + 1: OU owner
       + 2: OU admin
   * - state
     - Enum
     - The user account status.
     
       + 0: Enabled
       + 1: Disabled
   * - mfaType
     - Enum
     - The multi-factor authentication type.
     
       + 0: Disabled
       + 1: By SMS
       + 2: By email
       + 3: By SMS and email
   * - passwordState
     - Enum
     - The user password status.
     
       + 0: Normal
       + 1: Requires password change
   * - passwordExpireTime
     - Long
     - The password expiring time.
   * - passwordStrength
     - Enum
     - The password strength.
     
       + 0: Medium
       + 1: Strong
       + 2: Very strong
   * - createTime
     - String
     - The time when the user account is created.
   * - createdByUserId
     - String
     - The user who created the account.


## Error Code

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Description
   * - 30400
     - The user accout or password is not correct, or the LDAP domain is missing, or the LDAP attribute mapping is not correct, or connection failed.
   * - 30404
     - The LDAP connection does not exist.
   * - 30410
     - The password has expired.
   * - 30429
     - The login failure times of the IP or account has reached the limit. Please try again later.
   * - 30511
     - The user account is disabled, or the LDAP login is disabled.

## Sample

### Request Sample

```
url: https://{apigw-address}/enos-iam-service/v2.0/login
method: POST
requestBody:
{
  "authType":0,
  "linkName":"",
  "credentials":"xxx",
  "principal":"xxxx",
  "keyId":"yyy",
  "captcha":"xxxx",
  "clientIp":"1.1.1.1",
  "expireInterval":3600
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
  "captcha":"",
  "success": true,
  "requestId": null,
  "failed": false,
  "message": "",
  "status": 0,
  "successful": true
}
```
