# Batch Processing Service Overview

<br />

EnOS Enterprise Analytics Platform is targeted for the batch processing of data at rest to obtain insights from the data. During offline data analysis, you can use the APIs provided by the Batch Processing Service to perform data integration, data development, and workflow operation tasks.

## API List

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Cancel Flow Instance <cancel_flow_instance.html>`__
     - Cancel the running of a specified workflow instance.
   * - `Create Directory <create_directory.html>`__
     - Create a directory.
   * - `Delete Flow <delete_flow.html>`__
     - Delete a specified workflow.
   * - `Disable Flow <disable_flow.html>`__
     - Stop the scheduling of a specified workflow.
   * - `Enable Flow <enable_flow.html>`__
     - Start the scheduling of a specified workflow.
   * - `Export Flow <export_flow.html>`__
     - Export a workflow configuration.
   * - `Get Current Time <get_current_time.html>`__
     - Get the current time of the server.
   * - `Get Flow <get_flow.html>`__
     - Get the information of a specified workflow.
   * - `Get Flow Instance <get_flow_instance.html>`__
     - Get the information of a specified workflow instance.
   * - `Get My Flow <get_my_flow.html>`__
     - Search workflows that meet the search criteria.
   * - `Get Task Instance Log <get_task_instance_log.html>`__
     - Get the log of a specified task instance.
   * - `Get Time Zone <get_time_zone.html>`__
     - Get the time zone where the server is located.
   * - `Import Flow <import_flow.html>`__
     - Import workflow configuration to create a workflow with the specified name under the specified directory.
   * - `List Flow Instances <list_flow_instances.html>`__
     - Search workflow instances that meet the search criteria.
   * - `List Workflow Directories <list_workflow_dirs.html>`__
     - Get all the content in the `workflow` directory of the current OU, including workflow files and sub-directories.
   * - `Load Flow For Edit <load_flow_for_edit.html>`__  
     - Load the specified workflow to a temporary workflow to get the workflow information.
   * - `Save Flow <save_flow.html>`__
     - Save the information of the current workflow.
   * - `Search Flow <search_flow.html>`__
     - Search the basic information of workflows that meet the search criteria.
   * - `Trigger Flow <trigger_flow.html>`__
     - Trigger a workflow schedule manually.
   * - `Update And Trigger Flow <update_and_trigger_flow.html>`__
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
     - Internal server exception
     - Internal server exception.

<!-- end -->
