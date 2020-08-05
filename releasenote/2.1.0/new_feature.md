# New APIs

<br />

In EnOS 2.1 Release, we added support to the following new APIs and API services.

## Model Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Search Thing Model <../../model/searchmodel>`__
     - A new parameter ``dataDefinition`` is supported in ``ThingAttribute`` struct, ``ThingMeasurepoint`` struct, and ``ThingDatapoint`` struct to define the data type represented by the ``datatype`` parameter in the structure.

## Connection Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Apply Certificate <../../connect/apply_cert>`__
     - Apply for a new certificate and bind it to a device.
   * - `Renew Certificate <../../connect/update_cert>`__
     - Renew a certificate and bind it to a device.
   * - `Revoke Certificate <../../connect/delete_cert>`__
     - Revoke a certificate bound to a device.
   * - `List Certificate <../../connect/list_cert>`__
     - List the certificates bound to a device.
   * - `Search Command <../../connect/search_command>`__
     - Query the details of the commands.
   * - `Replace Device <../../connect/replace_device.html>`__
     - Replace the Device Key of a device without changing its asset ID (`assetId`).

## Asset Tree Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Create Asset Tree <../../asset_tree/create_asset_tree>`__
     - Create an asset tree as well as its root node.
   * - `Create Asset Tree and Associate Asset <../../asset_tree/create_asset_tree_and_associate_asset>`__
     - Create an asset tree and associate an existing asset as the root node of the asset tree.
   * - `Delete Asset Tree <../../asset_tree/delete_asset_tree>`__
     - Delete an asset tree.
   * - `Update Asset Tree <../../asset_tree/update_asset_tree>`__
     - Update the asset tree information.


## Alert Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Create Active Alerts in Batch <../../event/create_active_alerts_in_batch>`__
     - Create active alerts in batch.
   * - `Create History Alerts in Batch <../../event/create_history_alerts_in_batch>`__
     - Create history alerts in batch.
   * - `Create Alert Type <../../event/create_alert_type>`__
     - A new parameter ``parentTypeId`` is supported in ``generateType`` struct to indicate the alert type ID of the parent alert.
   * - `Update Alert Type <../../event/update_alert_type>`__
     - A new parameter ``parentTypeId`` is supported in ``generateType`` struct to indicate the alert type ID of the parent alert.
   * - `Close Active Alert <../../event/close_active_alert>`__
     - Close an active alert.
   * - `Search Alert Rule <../../event/search_alert_rule>`__
     - Search for alert rules based on the search criteria.
   * - `Batch Update Active Alert Tags <../../event/batch_update_active_alert_tags.html>`__
     - Batch update the tags for the specified alerts
   * - `Create Alert Rule <../../event/create_alert_rule.html>`__
     - Create a new alert rule
   * - `Update Alert Rule <../../event/update_alert_rule.html>`__
     - Update an alert rule
   * - `Delete Alert Rule <../../event/delete_alert_rule.html>`__
     - Delete all the rules under the organization as per the alert rule IDs
   * - `Create Alert Content <../../event/create_alert_content.html>`__
     - Create a new alert content
   * - `Update Alert Content <../../event/update_alert_content.html>`__
     - Update an alert content
   * - `Delete Alert Content <../../event/delete_alert_content.html>`__
     - Delete an alert content
   * - `Create Alert Severity <../../event/create_alert_severity.html>`__
     - Create a new alert severity
   * - `Update Alert Severity <../../event/update_alert_severity.html>`__
     - Update an alert severity
   * - `Delete Alert Severity <../../event/delete_alert_severity.html>`__
     - Delete an alert severity
   * - `Create Alert Type <../../event/create_alert_type.html>`__
     - Create a new alert type
   * - `Update Alert Type <../../event/update_alert_type.html>`__
     - Update an alert type
   * - `Delete Alert Type <../../event/delete_alert_type.html>`__
     - Delete an alert type
   * - `Create Active Alert <../../event/create_active_alert.html>`__
     - Create a new active alert
   * - `Delete Active Alert <../../event/delete_active_alert.html>`__
     - Delete a specified active alert
   * - `Create History Alert <../../event/create_history_alert.html>`__
     - Create a new history alert


## TSDB Data Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Get Asset DI Data Duration <../../tsdb_service/get_asset_di_data_durations>`__
     - Get the duration of different status (DI) data of specified devices within a certain period.

## IAM Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Get Organization <../../iam/get_org>`__
     - Get the organization's information.


## Application Portal Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Get User's Applications <../../app_portal/get_user_apps>`__
     - Get a list of applications that the current user has permission to access through Access Token.
   * - `Authorize Asset <../../app_portal/authorize_asset>`__
     - Authorize the new asset created on EnOS platform to the asset creator
   * - `Check Asset Permission <../../app_portal/check_asset_permission>`__
     - Check if the current user has the access permission of the requested asset
   * - `Choose Organization <../../app_portal/choose_organization>`__
     - Select the organization that the user needs to use after login
   * - `Create Message <../../app_portal/create_message>`__
     - Create common messages and alert message on the Application Portal
   * - `Get App Menu and Permission <../../app_portal/get_app_menu_and_permission>`__
     - Get the list of application menu and permission
   * - `Get Assets by Application <../../app_portal/get_assets_by_app>`__
     - Get all assets that the current user can access under a specified application
   * - `Get Assets by Organization <../../app_portal/get_assets_by_ou>`__
     - Get all the assets that a specified user can access under a specified organization
   * - `Get Asset Structure <../../app_portal/get_asset_structure>`__
     - Get the upstream organizational structure of the organizational structure in which the asset is located
   * - `Get Colors of the Message Icon <../../app_portal/get_colors_of_the_message_icon>`__
     - Get the collection of colors that the message icon can be configured
   * - `Get Manageable User List <../../app_portal/get_manag_user_list>`__
     - Get a list of all users that can be managed under the current account
   * - `Get Message Ringtones <../../app_portal/get_message_ringtones>`__
     - Get the collection of ringtones that the message can be configured
   * - `Get Organization List <../../app_portal/get_organization_list>`__
     - List the organizations which the current user belongs according to the Access Token
   * - `Get Organization User List <../../app_portal/get_ou_user_list>`__
     - Authorize the application to get a list of all users under a specified organization without logging in the Application Portal
   * - `Get Token Information <../../app_portal/get_token_information>`__
     - Get information about the currently logged-in user according to the Access Token
   * - `Get User Information <../../app_portal/get_user_information>`__
     - Get the information of the current user
   * - `Log In <../../app_portal/login>`__
     - Log in the account
   * - `Log Out <../../app_portal/logout>`__
     - Log out the account
   * - `Refresh Access Token <../../app_portal/refresh_access_token>`__
     - Request a new Access Token with the Refresh Token
   * - `Revoke Refresh Token <../../app_portal/revoke_refresh_token>`__
     - Revoke user’s Refresh Token
   * - `Sync Asset <../../app_portal/sync_asset>`__
     - Synchronize assets with specified tags on the EnOS to the Application Portal
   * - `Update Message <../../app_portal/update_messages>`__
     - Update the status of the message


## Prediction Model Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Machine Learning Forecast <../../ml_service/machine_learning_forecast>`__
     - Get the predition results of the deployed machine learning algorithm model.


## Dataflow Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Cancel Flow Instance <../../dataflow_service/cancel_flow_instance>`__
     - Cancel the running of a specific workflow instance.
   * - `Create Directory <../../dataflow_service/create_directory>`__
     - Create a directory of workflows.
   * - `Delete Flow <../../dataflow_service/delete_flow>`__
     - Delete a specific workflow.
   * - `Disable Flow <../../dataflow_service/disable_flow>`__
     - Disable the scheduling of a specific workflow.
   * - `Enable Flow <../../dataflow_service/enable_flow>`__
     - Enable the scheduling of a specific workflow.
   * - `Export Flow <../../dataflow_service/export_flow>`__
     - Export the configuration of a workflow.
   * - `Get Current Time <../../dataflow_service/get_current_time>`__
     - Get the current time of the server.
   * - `Get Flow <../../dataflow_service/get_flow>`__
     - Get the detailed information of a specific workflow.
   * - `Get Flow Instance <../../dataflow_service/get_flow_instance>`__
     - Get the detailed information of a specific workflow instance.
   * - `Get My Flow <../../dataflow_service/get_my_flow>`__
     - Query the detailed information of workflows by specific conditions.
   * - `Get Task Instance Log <../../dataflow_service/get_task_instance_log>`__
     - Get the logs of a specific work instance.
   * - `Get Time Zone <../../dataflow_service/get_time_zone>`__
     - Get the time zone of the location of the server.
   * - `Import Flow <../../dataflow_service/import_flow>`__
     - Import workflow configuration to create a workflow and save the workflow in a specific directory.
   * - `List Flow Instances <../../dataflow_service/list_flow_instances>`__
     - Query workflow instances by specific conditions.
   * - `List Workflow Directories <../../dataflow_service/list_workflow_dirs>`__
     - List the `workflow` directory information (including sub-directories and workflow files) of the current OU.
   * - `Load Flow For Edit <../../dataflow_service/load_flow_for_edit>`__  
     - Load the information a specific workflow to a temporary workflow for editing.
   * - `Save Flow <../../dataflow_service/save_flow>`__
     - Save the configuration of the current workflow.
   * - `Search Flow <../../dataflow_service/search_flow>`__
     - Search workflows by specific conditions and list the workflows by pages.
   * - `Trigger Flow <../../dataflow_service/trigger_flow>`__
     - Trigger the scheduling of a specific workflow manually.
   * - `Update And Trigger Flow <../../dataflow_service/update_and_trigger_flow>`__
     - Trigger the scheduling of a specific workflow with new parameters (generating a workflow instance without changing the workflow information).


<!--end-->
