# Dataflow Service Overview

<br />

EnOS Enterprise Analytics Platform is targeted for the batch processing of data at rest to obtain insights from the data. During offline data analysis, you can use the APIs provided by the Dataflow Service to perform data integration, data development, and workflow operation tasks.

## API List

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Cancel Flow Instance <cancel_flow_instance>`__
     - Cancel the running of a specified workflow instance.
   * - `Create Directory <create_directory>`__
     - Create a directory.
   * - `Delete Flow <delete_flow>`__
     - Delete a specified workflow.
   * - `Disable Flow <disable_flow>`__
     - Stop the scheduling of a specified workflow.
   * - `Enable Flow <enable_flow>`__
     - Start the scheduling of a specified workflow.
   * - `Export Flow <export_flow>`__
     - Export a workflow configuration.
   * - `Get Current Time <get_current_time>`__
     - Get the current time of the server.
   * - `Get Flow <get_flow>`__
     - Get the information of a specified workflow.
   * - `Get Flow Instance <get_flow_instance>`__
     - Get the information of a specified workflow instance.
   * - `Get My Flow <get_my_flow>`__
     - Search workflows that meet the search criteria.
   * - `Get Task Instance Log <get_task_instance_log>`__
     - Get the log of a specified task instance.
   * - `Get Time Zone <get_time_zone>`__
     - Get the time zone where the server is located.
   * - `Import Flow <import_flow>`__
     - Import workflow configuration to create a workflow with the specified name under the specified directory.
   * - `List Flow Instances <list_flow_instances>`__
     - Search workflow instances that meet the search criteria.
   * - `List Workflow Directories <list_workflow_dirs>`__
     - Get all the content in the `workflow` directory of the current OU, including workflow files and sub-directories.
   * - `Load Flow For Edit <load_flow_for_edit>`__  
     - Load the specified workflow to a temporary workflow to get the workflow information.
   * - `Save Flow <save_flow>`__
     - Save the information of the current workflow.
   * - `Search Flow <search_flow>`__
     - Search the basic information of workflows that meet the search criteria.
   * - `Trigger Flow <trigger_flow>`__
     - Trigger a workflow schedule manually.
   * - `Update And Trigger Flow <update_and_trigger_flow>`__
     - Trigger workflow scheduling with updated parameters.


## Common Error Codes

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 62101
     - userId does not exist, or it does not match to orgId.
     - The parameters ``userId`` or ``orgId`` is not valid.
   * - 62103
     - User has no privilege.
     - The user does not have access permission.
   * - 62109
     - Server internal exception
     - Server internal exception

<!-- end -->
