# Application Portal Service Overview

<br />

The EnOS Application Portal is a unified EnOS-based application login portal. You can get information about users, assets, and applications through the Application Portal service, and configure permissions on the EnOS Application Portal.

<br />

For more information about the EnOS Application Portal, refer to [About Application Portal](/docs/app-development/en/2.1.0/app_portal/overview.html).


## Authentication


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description   
   * - `Get Token Information <get_token_information>`__
     - Get information about the user who is currently logged-in through the access token
   * - `Log In <login>`__
     - Log in to the account
   * - `Log In Via Authorization Code <login_via_code>`__
     - Log in Application Portal via authorization code
   * - `Log Out <logout>`__
     - Log out of the account
   * - `Refresh Access Token <refresh_access_token>`__
     - Request a new access token using the refresh token
   * - `Revoke Refresh Token <revoke_refresh_token>`__
     - Revoke a user's refresh token



## User and Organization

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description   
   * - `Choose Organization <choose_organization>`__
     - Select the organization that the user needs to use after login
   * - `Get Manageable User List <get_manag_user_list>`__
     - List all users that can be managed under the current account
   * - `Get Organization List <get_organization_list>`__
     - List the organizations which the current user belongs according to the access token
   * - `Get Organization User List <get_ou_user_list>`__
     - Authorize the application to get a list of all the users under a specified organization without logging in to the Application Portal
   * - `Get App User List <get_app_user_list>`__
     - Based on the `accessKey` of an application, get the list of users who have access to the application
   * - `Get User Information <get_user_information>`__
     - Get the information of the current user
   * - `Get User Domain <get_user_domain>`__
     - Get the domain information of a user using the email address
   * - `Get User Structures <get_user_structures>`__
     - Get information of the organization structure to which a user is assigned

## Asset

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description   
   * - `Authorize Asset <authorize_asset>`__
     - Authorize the new asset created on EnOS platform to the asset creator
   * - `Check Asset Permission <check_asset_permission>`__
     - Check if the current user has the access permission for the queried asset
   * - `Get Assets by Application <get_assets_by_app>`__
     - Get all assets that the current user can access under a specified application
   * - `Get Assets by Organization <get_assets_by_ou>`__
     - Get all the assets that a specified user can access under a specified organization
   * - `Get Asset Structure <get_asset_structure>`__
     - Get the upstream organizational structure where the asset is located
   * - `Sync Asset <sync_asset>`__
     - Synchronize assets on the EnOS to the Application Portal
   * - `Get Users with Asset Access <get_privileged_users_to_asset>`__
     - Get the list of users who have access permission to a specific asset


## Application

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description   
   * - `Create Message <create_message>`__
     - Create common messages and alert messages on the Application Portal
   * - `Get App Menu and Permission <get_app_menu_and_permission>`__
     - Get the list of application menus and permissions
   * - `Get Colors of the Message Icon <get_colors_of_the_message_icon>`__
     - Get the list of colors for configuring the message icon
   * - `Get Message Ringtones <get_message_ringtones>`__
     - Get the list of ringtones for configuring the message
   * - `Get User's Applications <get_user_apps>`__
     - Get a list of applications that the current user has permission to access through the access token
   * - `Update Message <update_messages>`__
     - Update the status of the message
   * - `Get Unresolved Messages <get_unresolved_messages>`__
     - Get the list of unresolved messages that are reported for the applications


## Common Error Codes

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 200
     -
     - 成功
   * - 400
     - parameter.invalid.[参数名]
     - The [参数名]([参数值]) is invalid。 parameter.invalid.userId表示参数userId不合法
   * - 401
     - unauthenticated
     - Please authentication first 用户未登录
   * - 403
     - permission.denied
     - Permission denied无权访问或操作
   * - 404
     - [主体名].not.exist
     - The [主体名]([主体标识]) does not exist| user.not.exist表示用户不存在 organization.user.not.exist表示组织下用户不存在
   * - 408
     - [主体名].already.existed
     - The [主体名]([主体标识]) is already existed  | user.already.existed表示用户已存在,organization.user.already.existed表示组织下用户已存在
   * - 409
     - []
     - The [主体名]([主体标识]) is conflict   | 账号在另一地点登录
   * - 410
     - [主体名].expired
     - The [主体名]([主体标识/值]) is expired  | cache.token.expired表示token失效
   * - 415
     - [].out.range
     - The []([]) is out of range
   * - 429
     - [操作名.主体名].exhausted
     - Try [操作名.主体名] too many times. Please try again [时长] later. | login.ip.exhausted表示某IP登录过于频繁，用光次数
   * - 432
     - [主体名].too.many
     - Too many [主体名] | user.too.many表示存在多个用户（本应只有一个）
   * - 500
     - system.internal.error
     - System internal error  | 系统错误
   * - 504
     - timeout
     - Service timeout  | 服务超时
   * - 512
     - organization unselected
     - Please select organization first| 用户未选择组织



<!--end-->
